## Sistema Informatico di Consolidamento (SInC)
E' un sistema per la gestione del processo di Consolidamento dei Bilanci realizzato dalla Cooperativa EDP La Traccia per la Regione Basilicata.

**Versione corrente: 2.0** (Oracle Database 19c, Oracle APEX 24.1). La versione 1.0 resta disponibile nel tag [`v1.0`](https://github.com/RegioneBasilicata/SistemaInformaticoConsolidamento/tree/v1.0).

## Descrizione
Il sistema consente il consolidamento dei Bilanci dell'Ente capogruppo con partecipate, controllate ed enti strumentali dal caricamento dei dati di bilancio e delle partite infragruppo da file esterni (fogli elettronici strutturati).

## Framework, tecnologie e linguaggi utilizzati
 - Oracle Database 19c e superiori
 - Oracle APEX (Application Express) 24.1 e superiori
 - Oracle REST Data Services (ORDS)
 - PL/SQL
 - Java
 - Javascript
 - Jasper Report
 - JQuery

## Requisiti di installazione
|Requisito| Versione |Descrizione|
|-----------|-----------|---------|
| [Oracle Database](https://www.oracle.com/database/) | 19c o superiore | Base dati |
| [Oracle APEX](https://apex.oracle.com/) | 24.1 o superiore | Ambiente applicativo |
| [Oracle REST Data Services](https://www.oracle.com/database/technologies/appdev/rest.html) | compatibile con la release APEX | Listener web per APEX |
| [JasperReports](https://community.jaspersoft.com) | - | Motore per la reportistica ufficiale (sorgenti `.jrxml` nella cartella `Report`) |

## Contenuto del repository
| Percorso | Contenuto |
|----------|-----------|
| `SQL/SInC_DB_DDL.sql` | Script di creazione degli oggetti di database (tabelle, viste, indici, sequence, package, procedure, funzioni, trigger) |
| `SQL/SInC_Application.sql` | Export dell'applicazione APEX (applicazione 511 - CONSOLIDATO) |
| `Report/` | Sorgenti dei report Jasper |
| `Documenti/` | Manuale utente |
| `SInC DB Documentation/` | Dizionario dati |

## Installazione
1. **Schema.** Creare uno schema dedicato (ad esempio `SINC`) con i privilegi `CREATE TABLE`, `CREATE VIEW`, `CREATE SEQUENCE`, `CREATE PROCEDURE`, `CREATE TRIGGER`, `CREATE TYPE`, `CREATE SYNONYM` e quota sul proprio tablespace di default.
2. **Oggetti di database.** Collegati con SQLcl o SQL*Plus allo schema creato, eseguire:
   ```
   @SQL/SInC_DB_DDL.sql
   ```
   Gli oggetti vengono creati nello schema corrente e nel suo tablespace di default. Al termine ricompilare gli oggetti non validi:
   ```
   exec DBMS_UTILITY.compile_schema(schema => USER, compile_all => FALSE);
   ```
3. **Workspace APEX.** Creare un workspace APEX associato allo schema.
4. **Applicazione.** Importare `SQL/SInC_Application.sql` dal workspace (App Builder > Import), oppure da SQLcl impostando prima workspace, schema e ID applicazione:
   ```sql
   begin
     apex_application_install.set_workspace('NOME_WORKSPACE');
     apex_application_install.set_schema('SINC');
     apex_application_install.generate_application_id;
     apex_application_install.generate_offset;
   end;
   /
   @SQL/SInC_Application.sql
   ```
5. **Report.** Pubblicare i report della cartella `Report` sul server Jasper e valorizzare l'URL del server nella tabella `APPLICATION_PARAMETER`.

### Integrazioni specifiche dell'installazione della Regione Basilicata
Lo script contiene alcuni oggetti che nell'installazione originale collegano il SInC ad altri sistemi della Regione. In una nuova installazione possono essere ignorati, oppure ricondotti ai sistemi contabili dell'ente:
- **sinonimi `*_FIN_T_DATI_GENERALI`, `*_NB_PIACEE_IMPORTI`, `GIUNTA_T_NB_MASTRINI_TP`**: puntano alle contabilità degli enti strumentali tramite il database link `SIC11` (schema `GAT2`), non incluso nello script;
- **sinonimi `PRO_REPOSITORY`, `PRO_CRIPTO_ALLEGATI` e il `GRANT` verso `REGBAS_STORAGE`**: riguardano lo schema di archiviazione documentale della Regione.

Se questi sistemi non esistono, i relativi `GRANT` danno errore e gli oggetti che li usano restano non validi senza effetti sulle altre funzioni.

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
Generazione Tabelle da allegare alla Nota Integrativa
Generazione file in formato xbrl per invio alla Banca Dati Amministrazioni Pubbliche (BDAP)

**Caratteristiche Funzionali**
Il sistema è rilasciato in ambiente Web ed è utilizzabile con un semplice browser (compatibile con tutti i più diffusi browser).

## Documenti
Di seguito i documenti che accompagnano il codice

 1. Manuale di Gestione dell'Applicazione
 2. [Manuale Utente](Documenti/Manuale%20Utente%20SInC.pdf)
 3. [Script SQL per la creazione degli oggetti di Data Base](SQL/SInC_DB_DDL.sql)
 4. [File sorgente APEX dell'applicazione](SQL/SInC_Application.sql)
 5. [Dizionario dati DB](SInC%20DB%20Documentation)

## Licenza
Il software è rilasciato con licenza EUPL-1.2 (vedi [LICENSE.txt](LICENSE.txt)).
