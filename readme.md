

## Sistema Informatico di Consolidamento (SInC)
E' un sistema per la gestione del processo di Consolidamento dei Bilanci realizzato dalla Cooperativa EDP La Traccia per la Regione Basilicata.

## Descrizione
Il sistema consente il consolidamento dei Bilanci dell’Ente capogruppo con partecipate, controllate ed enti strumentali dal caricamento dei dati di bilancio e delle partite infragruppo da file esterni (fogli elettronici strutturati). 

## Framework, tecnologie e linguaggi utilizzati
 - Oracle DataBase vers. 11 e superiori
 - Oracle Application Express vers. 4.0 e superiori
 - PL/SQL
 - Java
 - Javascript
 - Jasper Report
 - JQuery

## Requisiti di installazione
|Requisito| Versione |Descrizione|
|-----------|-----------|---------|
| [Oracle Database](https://www.oracle.com/it/database/) | >10 |Base dati (qualsiasi release)
|[Oracle Application Express](https://apex.oracle.com/)|4|Ambiente di sviluppo
|[Tomcat](https://tomcat.apache.org) (o altri Apex compliant)|-|Application server 
|[JasperSoft Studio](https://community.jaspersoft.com)|>5|Report builder

## Installazione
Per tutti i dettagli circa le modalità di installazione del SIC leggere e seguire le istruzioni di [installazione](www.latraccia.it).

## Principali funzionalità

**Definizione e gestione Gruppo Amministrazione Pubblica (GAP):**
Gestione anagrafiche
Gestione dettagli partecipazione/controllo (importo, %, ecc.).

**Importazione dati contabili:**
Import bilanci
Import partite infragruppo 

**Gestione Infragruppo:**
Immissione manuale partite infragruppo
Gestione rettifiche partite Infragruppo

**Gestione Rettifiche di coerenza e di consolidamento:**
Inserimento e gestione rettifiche di coerenza
Rilevamento automatico differenze di consolidamento e inserimento automatico rettifiche di consolidamento
Verifica quadrature rettifiche

**Gestione Consolidamento:**
Funzione di generazione Bilancio Aggregato (pre Consolidamento)
Funzione di generazione Bilancio Consolidamento
Report Interattivi per analisi aggregate e di dettaglio

**Reportistica Ufficiale:**
Generazione Tabelle da allagare alla Nota Integrativa
Generazione file in formato xbrl per invio alla Banca Dati Amministrazioni Pubbliche (BDAP)
Caratteristiche Funzionali
Il sistema è rilasciato in ambiente Web. Ed è utilizzabile con il semplice utilizzo di un browser (compatibile con tutti i più diffusi browser).

## Documenti
Di seguito i documenti che accompagnano il codice

 1. Manuale di Gestione dell'Applicazione
 2. Manuale Utente
 3. [Scripts SQL per la creazione degli oggetti di Data Base](https://github.com/RegioneBasilicata/SistemaInformaticoConsolidamento/blob/master/SQL/SInC_DB_DDL.sql)
 4. [File sorgente Apex dell'applicazione](https://github.com/RegioneBasilicata/SistemaInformaticoConsolidamento/blob/master/SQL/SInC_Application.sql)
 5. [Dizionario dati DB](https://github.com/RegioneBasilicata/SistemaInformaticoConsolidamento/tree/master/SInC%20DB%20Documentation)
