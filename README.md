# Un'applicazione Web per la vendita e la gestione di biglietti da visita digitali all'interno di card NFC: Digilink.cards - Il futuro del networking


## Funzionalità dell’ applicazione Web:

**Gestione delle cards:**

- Ogni card NFC è univoca ha un nome, una descrizione e un prezzo.
- Le card possono essere di diverse tipologie.
- Ogni card può avere una o più immagini associate per la visualizzazione.
- Ogni card è associata ad un’azione modificabile dall’utente.

**Gestione degli Utenti:**

- Gli utenti possono registrare un account con nome, indirizzo email e password crittografata.
- Gli utenti possono effettuare il login per accedere all'area personale.
- Gli utenti registrati possono salvare cards nel carrello e vedere lo storico degli ordini.
- Gli utenti possono caricare la propria grafica personalizzata da utilizzare sulla card NFC.
- Nel caso in cui gli utenti non dispongano di una grafica personalizzata, possono richiedere l'intervento di un grafico GWEB per creare una grafica adatta.

**Gestione delle grafiche:**

- Gli utenti possono realizzare una grafica personalizzata avendo a disposizione un mock-up per rendere più semplice la realizzazione.
- Ogni grafica è associata ad ogni singola card
- Il file di ogni grafica avrà come nome l’id della card associata
- Generazione delle grafiche

**Gestione degli Ordini:**

- Gli utenti possono creare ordini, selezionando uno o più cards nel carrello.
- Ogni ordine ha un numero di ordine univoco, una data e un totale.
- Ogni ordine contiene dettagli sulle cards incluse, come quantità e prezzo unitario.

**Gestione delle Transazioni:**

- Le transazioni rappresentano i pagamenti effettuati dagli utenti per confermare gli ordini.
- Ogni transazione ha un ID univoco, una data e l'importo del pagamento.
- Le informazioni sulla carta di credito/debito dell'utente non vengono memorizzate nel database per motivi di sicurezza.

**Interazione con il gestionale aziendale:**

- Gli utenti che effettueranno un acquisto verranno aggiunti alla lista “Aziende” presente all’interno del gestionale aziendale “Teamleader”.
- Le fatture generate conseguentemente ad una transazione andata a buon fine, verranno inserite all’interno della lista “Fatture” del gestionale aziendale “Teamleader”.

## Struttura del database

**Tabella “Cards":**

Colonne: *IDcard (PK),Nome, Descrizione, Prezzo, IDTipologia (FK), Immagini.*

- Gestione dell'Inventario: La tabella “Cards" tiene traccia di tutte le cards disponibili. Per ogni card, viene registrato il nome, la descrizione, il prezzo e altre informazioni rilevanti.
- Catalogazione: Ogni card è associato a una tipologia tramite la colonna IDTipologia. Questo aiuta gli utenti a navigare nel catalogo in base alle loro preferenze e interessi.
- Prezzo e Costi: La colonna "Prezzo" indica ilcosto del card per gli acquirenti.

**Tabella “Tipologie":**

Colonne: *IDTipologia (PK),Nome Tipologia.*

- Organizzazione delle cards: La tabella Tipologie serve a organizzare e categorizzare le cards nel negozio.
- Nomenclatura Strutturata: Il nome della tipologia fornisce una descrizione breve del tipo di cards contenuti in quella categoria. Questo aiuta gli utenti a capire a cosa si riferisce ogni tipologia.
- Facilita la Navigazione: Gli utenti possono esplorare le cards per tipologia, semplificando la ricerca delle cards che soddisfano le loro esigenze e preferenze specifiche.
- Ricerca e Filtraggio: Le tipologie possono essere utilizzate come opzioni di filtraggio per aiutare gli utenti a restringere la selezione delle cards. Ad esempio, un utente può selezionare la categoria “Metal" per visualizzare solo le cards in metallo.

**Tabella “Promozioni”**

Colonne: *IdPromo(PK), IDTipologia(FK),Codice_sconto, Percentuale, Data_Inizio, Data\_Fine,Singolo_Multiplo, Attivo*

- Generazione codici sconto: La tabella promozioni contiene le informazioni riguardo i codici sconto utilizzabili al momento del checkout.
- Controllo durata: Grazie alle colonne “Data_inizio”e “Data_fine” si può limitare il periodo in cui un codice sconto è utilizzabile.

**Tabella "Utenti":**

Colonne: *IDUtente (PK),Nome, Email, Password.*

- Registrazione degli Utenti: La tabella "Utenti" registra le informazioni di base di ciascun utente che si registra nel sistema di e-commerce. Questo include il loro nome, indirizzo email e password e dati anagrafici.
- Accesso Utente: L'indirizzo email e la password sono utilizzati per consentire agli utenti registrati di accedere al sistema. Il confronto della password crittografata assicura l'autenticità dell'utente.
- Gestione dei Profili:Le informazioni nella tabella "Utenti" possono includere dettagli sul profilo dell'utente, come nome e email. Questi dettagli possono essere visualizzati e modificati dall'utente tramite l'area personale del sito.
- Sicurezza delle Informazioni: La password deve essere crittografata prima di essere salvata nel database per garantire la sicurezza delle credenziali dell'utente.
- Creazione degli Ordini: Gli utenti registrati possono generare ordini e associarli al loro profilo. Ciò consente loro di tenere traccia delle transazioni e dello storico degli acquisti.
- Comunicazioni con l'Utente: L'indirizzo email nella tabella "Utenti" può essere utilizzato per comunicazioni legate all'account, come conferma di ordini, promozioni e aggiornamenti.

**Tabella “Indirizzi”:**

Colonne: *Id Indirizzo (PK),IDUtente (FK),Tipo, Città, Cap, Via,Stato, Regione, Provincia, Civico*

- Tipologie di indirizzo: In fase di registrazione o modifica del profilo utente, nella tabella indirizzi verranno archiviati i dati relativi agli indirizzi dei clienti che possono variare in base alla tipologia (residenza e fatturazione)

**Tabella “Personalizzazioni”**

Colonne: *IDGrafica(PK), IDUtente(FK), Data_creazione, File,Note*

- Upload file: L’utente può eseguire l’upload di una grafica personalizzata
- Note: L’utente può specificare info aggiuntive per arricchire la sua personalizzazione.

**Tabella "Carrello":**

Colonne: *IDCarrello (PK),IDUtente (FK),IDCard (FK),IDGrafica (FK), Quantità*

- Aggiunta di Cards al Carrello: Quando un utente seleziona un prodotto per l'acquisto, un nuovo record viene inserito nella tabella “Cards Nel Carrello". Questo record contiene informazioni come l'ID del carrello, l'ID della cards selezionata e la quantità desiderata.
- Quantità di Cards: La colonna "Quantità" tiene traccia del numero di copie della card che l'utente desidera acquistare. Se l'utente modifica la quantità nel carrello, questa colonna viene aggiornata di conseguenza.
- Corrispondenza con il Carrello dell'Utente: L'IDCarrello collega ogni riga del carrello all'utente che l'ha creato. In questo modo, le righe del carrello sono associate all'utente corretto.
- Associazione con le Cards: L'IDCard collega ciascuna riga del carrello al prodotto specifico che l'utente ha selezionato. Ciò consente di accedere alle informazioni dettagliate della card come il nome, la descrizione e il prezzo.
- Creazione degli Ordini: Quando l'utente decide di procedere al checkout, le informazioni dalle righe del carrello vengono utilizzate per creare gli ordini. Questo comporta la creazione di nuovi record nella tabella "Ordini" e "Dettagli Ordine”.

**Tabella "Gestione Cards”:**

Colonne: *ID(PK),ID_Card (FK),ID_Utente(FK),ID_Grafica(FK), URL_Associato, Data\_modifica, Tipo_Rendirizzamento*

- Archiviazione dello Storico: La tabella conserva uno storico di tutte le modifiche apportate alle card NFC,consentendo di visualizzare le modifiche precedenti e la cronologia delle modifiche nel tempo.
- Tracciamento dell'Utente: Utilizzando la chiave esterna "ID_Utente",è possibile identificare l'utente che ha effettuato ogni modifica, tenendo conto della responsabilità delle modifiche.
- Recupero dell'Ultima Modifica: Per ottenere l'ultima modifica effettuata su una card NFC,è possibile eseguire una query che ordina i record in base alla "Data_modifica"in ordine decrescente e quindi seleziona il primo risultato.
- Registrazione dei Dettagli delle Modifiche: La tabella registra i dettagli delle modifiche, inclusi l'URL_associato, il tipo di reindirizzamento e la data e l'ora della modifica, consentendo di avere una visione completa di ciascuna modifica.
- Chiavi Esterne: Le chiavi esterne "ID_Card" e "ID\_Utente"assicurano che le modifiche siano sempre associate a una card specifica e a un utente specifico, mantenendo l'integrità dei dati.

**Tabella "Ordini":**

Colonne: *IDOrdine (PK),Numero Ordine, Data, IDUtente (FK),IDGrafica (FK),Totale.*

- Creazione di NuoviOrdini: Quando un utente completa il processo di checkout, un nuovo record viene creato nella tabella "Ordini". Questo record rappresenta l'ordine effettuato dall'utente.
- Associazione con l'Utente: L'ID_Utente collega l'ordine all'utente che ha effettuato l'acquisto. Questo permette agli utenti di accedere al loro storico degli ordini e alle informazioni relative agli acquisti precedenti.
- Tracciamento dell'Ordine: La colonna "Data" tiene traccia della data e dell'ora in cui l'ordine è stato effettuato. Queste informazioni sono utili per il monitoraggio e la gestione degli ordini.
- Calcolo del Totale: La colonna "Totale" rappresenta l'importo totale dell'ordine. Questo valore viene calcolato sommando i costi delle cards, le spese di spedizione e altre eventuali spese aggiuntive.
- Gestione degli Ordini: L'amministratore del sistema può utilizzare la tabella "Ordini" per monitorare e gestire gli ordini. Questo include l'elaborazione degli ordini, l'aggiornamento dello stato dell'ordine e l'invio di conferme agli utenti.
- Storico degli Acquisti: Gli utenti possono consultare la loro cronologia degli ordini per tenere traccia dei prodotti acquistati in passato, delle date di acquisto e dei dettagli finanziari.
- Supporto alle Operazioni Post-Vendita: Le informazioni presenti nella tabella "Ordini"sono utili per gestire il supporto clienti, la restituzione di prodotti e la risoluzione di eventuali problemi post-vendita.

**Tabella "Dettagli Ordine":**

Colonne: *IDDettaglio (PK),IDOrdine (FK),IDcard (FK),IDGrafica (FK),Quantità, Prezzo Unitario.*

- Registro delle Cards nell'Ordine: Quando un utente effettua un ordine, un record viene creato nella tabella "Dettagli Ordine" per ogni card inclusa nell'ordine. Questo record rappresenta un dettaglio dell'ordine che specifica quali cards sono state ordinate e in quale quantità.
- Corrispondenza con l'Ordine: L'IDOrdine collega ogni dettaglio dell'ordine all'ordine globale a cui appartiene. Ciò permette di raggruppare tutti i dettagli relativi a un ordine specifico.
- Associazione con le Cards: L'IDCard collega ciascun dettaglio dell'ordine al prodotto specifico incluso in quel dettaglio. Ciò permette di accedere alle informazioni della card come ilnome, la descrizione e il prezzo.
- Calcolo del Totale per il Dettaglio: La colonna "Totale" rappresenta l'importo totale per la card nell'ambito del dettaglio dell'ordine. Questo valore viene calcolato moltiplicando la quantità per il prezzo unitario.
- Supporto al Calcolo del Totale dell'Ordine: La somma dei totali dei dettagli dell'ordine può essere utilizzata per calcolare l'importo totale dell'ordine complessivo.
- Dettagli delle Cards per l'Utente: Gli utenti possono consultare i dettagli specifici delle cards incluse in ciascun ordine per ottenere una visione dettagliata delle loro selezioni.

**Tabella "Transazioni":**

Colonne: *IDTransazione (PK),Data, Importo, IDUtente (FK).*

- Registrazione delle Transazioni: La tabella "Transazioni" tiene traccia di ogni transazione finanziaria nel sistema di e-commerce, inclusi pagamenti, rimborsi e altre operazioni finanziarie correlate agli ordini.
- Tipi di Transazione: La colonna "Tipo" indica il tipo di transazione, fornendo informazioni su ciò che ha causato la transazione, ad esempio il pagamento di un ordine o un rimborso.
- Importo Finanziario: La colonna "Importo" rappresenta l'importo monetario associato alla transazione. Questo può includere il totale dell'ordine, le spese di spedizione, le tasse o qualsiasi altro importo finanziario pertinente.
- Data della Transazione: La colonna "Data" registra la data e l'ora in cui è avvenuta la transazione. Queste informazioni sono utili per il monitoraggio e la gestione delle transazioni nel tempo.
- Stato delle Transazioni: La colonna "Stato" indica lo stato attuale della transazione, come "Completata" se è andata a buon fine, "In sospeso" se è in attesa di elaborazione o "Annullata" se è stata annullata.

**Tabella "Fatture":**

Colonne: *IDFattura (PK),Id Transazione (FK),id\_teamleader,iva inclusa, iva esclusa, iva, scadenza, stato, creata\_il, emessa\_il, url\_teamleader,numero\_fattura, pagata, inviata*

- Creazione ed emissione fattura: Dopo aver eseguito il checkout, e successivamente all’approvazione della transazione viene creato un record all’interno della tabella “Fatture”.
- Sincronizzazione con Teamleader: Possibilità di interagire con il gestionale dell’azienda “Teamleader”.

## Schema ER

![Schema_ER](/schema_er.jpg)

### Schema ER in formato testuale (con attributi)

```text
Entità e Relazioni:

Entità: 
- Cards (ID_card [PK], Nome, Descrizione, Prezzo, ID_Tipologia [FK], Immagini)

- Tipologie (ID_Tipologia [PK], Nome_Tipologia)

- Promozioni (ID_Promo [PK], ID_Tipologia [FK], Codice_sconto, Percentuale, Data_Inizio, Data_Fine, Singolo_Multiplo, Attivo)

- Utenti (ID_Utente [PK], Nome, Email, Password)

- Indirizzi (Id_Indirizzo [PK], ID_Utente [FK], Tipo, Città, Cap, Via, Stato, Regione, Provincia, Civico)

- Personalizzazioni (Id_Grafica [PK], ID_Utente [FK], Data_creazione, File, Note)

- Carrello (ID_Carrello [PK], ID_Utente [FK], ID_Card [FK], ID_Grafica [FK], Quantità)

- Gestione_Cards (ID [PK], ID_Card [FK], ID_Utente [FK], ID_Grafica [FK], URL_Associato, Data_modifica, Tipo_Rendirizzamento)

- Ordini (ID_Ordine [PK], Numero_Ordine, Data, ID_Utente [FK], ID_Grafica [FK], Totale)

- Dettagli_Ordine (ID_Dettaglio [PK], ID_Ordine [FK], ID_Card [FK], ID_Grafica [FK], Quantità, Prezzo_Unitario)

- Transazioni (ID_Transazione [PK], Data, Importo, ID_Utente [FK])

- Fatture (ID_Fattura [PK], Id_Transazione [FK], id_teamleader, iva_inclusa, iva_esclusa, iva, scadenza, stato, creata_il, emessa_il, url_teamleader, numero_fattura, pagata, inviata)

Relazioni:
- Cards -> Tipologie (FK: ID_Tipologia)
- Tipologie -> Cards (FK: ID_Tipologia)
- Promozioni -> Tipologie (FK: ID_Tipologia)
- Utenti -> Indirizzi (FK: ID_Utente)
- Utenti -> Personalizzazioni (FK: ID_Utente)
- Carrello -> Utenti (FK: ID_Utente)
- Carrello -> Cards (FK: ID_Card)
- Carrello -> Personalizzazioni (FK: ID_Grafica)
- Gestione_Cards -> Cards (FK: ID_Card)
- Gestione_Cards -> Utenti (FK: ID_Utente)
- Gestione_Cards -> Personalizzazioni (FK: ID_Grafica)
- Ordini -> Utenti (FK: ID_Utente)
- Ordini -> Personalizzazioni (FK: ID_Grafica)
- Dettagli_Ordine -> Ordini (FK: ID_Ordine)
- Dettagli_Ordine -> Cards (FK: ID_Card)
- Dettagli_Ordine -> Personalizzazioni (FK: ID_Grafica)
- Transazioni -> Utenti (FK: ID_Utente)
- Fatture -> Transazioni (FK: Id_Transazione)
- Fatture -> Utenti (FK: ID_Utente)
```

## Query SQL

```sql
-- Crea il database "G-Cards" se non esiste già
CREATE DATABASE IF NOT EXISTS G_Cards;

-- Seleziona il database "G-Cards"
USE G_Cards;

-- Crea la tabella "Cards"
CREATE TABLE Cards (
  ID_Card INT AUTO_INCREMENT PRIMARY KEY,
  Nome VARCHAR(255),
  Descrizione TEXT,
  Prezzo DECIMAL(10, 2),
  ID_Tipologia INT,
  Immagini BLOB,
  FOREIGN KEY (ID_Tipologia) REFERENCES Tipologie(ID_Tipologia)
);

-- Crea la tabella "Tipologie"
CREATE TABLE Tipologie (
  ID_Tipologia INT AUTO_INCREMENT PRIMARY KEY,
  Nome_Tipologia VARCHAR(255)
);

-- Crea la tabella "Promozioni"
CREATE TABLE Promozioni (
  ID_Promo INT AUTO_INCREMENT PRIMARY KEY,
  ID_Tipologia INT,
  Codice_Sconto VARCHAR(50),
  Percentuale DECIMAL(5, 2),
  Data_Inizio DATE,
  Data_Fine DATE,
  Singolo_Multiplo ENUM('Singolo', 'Multiplo'),
  Attivo BOOLEAN,
  FOREIGN KEY (ID_Tipologia) REFERENCES Tipologie(ID_Tipologia)
);

-- Crea la tabella "Utenti"
CREATE TABLE Utenti (
  ID_Utente INT AUTO_INCREMENT PRIMARY KEY,
  Nome VARCHAR(255),
  Email VARCHAR(255),
  Password VARCHAR(255)
);

-- Crea la tabella "Indirizzi"
CREATE TABLE Indirizzi (
  ID_Indirizzo INT AUTO_INCREMENT PRIMARY KEY,
  ID_Utente INT,
  Tipo VARCHAR(50),
  Città VARCHAR(255),
  Cap VARCHAR(10),
  Via VARCHAR(255),
  Stato VARCHAR(255),
  Regione VARCHAR(255),
  Provincia VARCHAR(255),
  Civico VARCHAR(10),
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente)
);

-- Crea la tabella "Personalizzazioni"
CREATE TABLE Personalizzazioni (
  ID_Grafica INT AUTO_INCREMENT PRIMARY KEY,
  ID_Utente INT,
  Data_Creazione TIMESTAMP,
  File BLOB,
  Note TEXT,
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente)
);

-- Crea la tabella "Carrello"
CREATE TABLE Carrello (
  ID_Carrello INT AUTO_INCREMENT PRIMARY KEY,
  ID_Utente INT,
  ID_Card INT,
  ID_Grafica INT,
  Quantità INT,
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente),
  FOREIGN KEY (ID_Card) REFERENCES Cards(ID_Card),
  FOREIGN KEY (ID_Grafica) REFERENCES Personalizzazioni(ID_Grafica)
);

-- Crea la tabella "Gestione Cards"
CREATE TABLE Gestione_Cards (
  ID INT AUTO_INCREMENT PRIMARY KEY,
  ID_Card INT,
  ID_Utente INT,
  ID_Grafica INT,
  URL_Associato VARCHAR(255),
  Data_Modifica TIMESTAMP,
  Tipo_Rendirizzamento VARCHAR(255),
  FOREIGN KEY (ID_Card) REFERENCES Cards(ID_Card),
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente),
  FOREIGN KEY (ID_Grafica) REFERENCES Personalizzazioni(ID_Grafica)
);

-- Crea la tabella "Ordini"
CREATE TABLE Ordini (
  ID_Ordine INT AUTO_INCREMENT PRIMARY KEY,
  Numero_Ordine VARCHAR(50),
  Data TIMESTAMP,
  ID_Utente INT,
  ID_Grafica INT,
  Totale DECIMAL(10, 2),
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente),
  FOREIGN KEY (ID_Grafica) REFERENCES Personalizzazioni(ID_Grafica)
);

-- Crea la tabella "Dettagli Ordine"
CREATE TABLE Dettagli_Ordine (
  ID_Dettaglio INT AUTO_INCREMENT PRIMARY KEY,
  ID_Ordine INT,
  ID_Card INT,
  ID_Grafica INT,
  Quantità INT,
  Prezzo_Unitario DECIMAL(10, 2),
  FOREIGN KEY (ID_Ordine) REFERENCES Ordini(ID_Ordine),
  FOREIGN KEY (ID_Card) REFERENCES Cards(ID_Card),
  FOREIGN KEY (ID_Grafica) REFERENCES Personalizzazioni(ID_Grafica)
);

-- Crea la tabella "Transazioni"
CREATE TABLE Transazioni (
  ID_Transazione INT AUTO_INCREMENT PRIMARY KEY,
  Data TIMESTAMP,
  Importo DECIMAL(10, 2),
  ID_Utente INT,
  FOREIGN KEY (ID_Utente) REFERENCES Utenti(ID_Utente)
);

-- Crea la tabella "Fatture"
CREATE TABLE Fatture (
  ID_Fattura INT AUTO_INCREMENT PRIMARY KEY,
  ID_Transazione INT,
  ID_Teamleader INT,
  Iva_Inclusa DECIMAL(10, 2),
  Iva_Esclusa DECIMAL(10, 2),
  Iva DECIMAL(10, 2),
  Scadenza DATE,
  Stato VARCHAR(50),
  Creata_Il TIMESTAMP,
  Emessa_Il DATE,
  URL_Teamleader VARCHAR(255),
  Numero_Fattura VARCHAR(50),
  Pagata BOOLEAN,
  Inviata BOOLEAN,
  FOREIGN KEY (ID_Transazione) REFERENCES Transazioni(ID_Transazione),
  FOREIGN KEY (ID_Teamleader) REFERENCES Utenti(ID_Utente)
);
```

## Proposta tema:

http://minia.php.themesbrand.com/index.html

