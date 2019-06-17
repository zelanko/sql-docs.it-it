---
title: Esecuzione della Console SSMA (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6750e17b694086cf716e32629fcf3b3f3b48f486
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453382"
---
# <a name="executing-the-ssma-console-db2tosql"></a>Esecuzione della Console SSMA (DB2ToSQL)
Microsoft offre un solido set di script di comandi del file per eseguire e controllare le attività SSMA. Le sezioni che seguono in modo dettagliato lo stesso. L'applicazione console utilizza alcuni comandi di file di script standard come enumerate in questa sezione.  
  
## <a name="project-script-file-commands"></a>Comandi di File di progetto Script  
I comandi di progetto di gestire la creazione di progetti, apertura, salvataggio e chiusura di progetti.  
  
**Command**  
  
create-new-project  
  
Crea un nuovo progetto SSMA.  
  
**Script**  
  
-   `project-folder` indica la cartella del progetto di creazione.  
  
-   `project-name` indica il nome del progetto. {string}  
  
-   `overwrite-if-exists`Attributo facoltativo indica se un progetto esistente deve essere sovrascritti. {boolean}  
  
-   `project-type:`Attributo facoltativo. Indica il tipo di progetto, ad esempio "sql-server-2005" progetto o il progetto "sql-server-2008" o "sql-server-2012" progetto o progetto "sql-server-2014" o "sql-azure". Valore predefinito è "sql-server-2014".  
  
**Esempio:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
Attributo 'Sovrascrivi-if-exists' è **false** per impostazione predefinita.  
  
Attributo 'project-type' è **sql Server°2008** per impostazione predefinita.  
  
**Command**  
  
Apri progetto  
  
Apre un progetto esistente.  
  
**Script**  
  
-   `project-folder` indica la cartella del progetto di creazione. Il comando ha esito negativo se la cartella specificata non esiste.  {string}  
  
-   `project-name` indica il nome del progetto. Il comando ha esito negativo se il progetto specificato non esiste.  {string}  
  
**Esempio di sintassi:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
SSMA per l'applicazione Console DB2 supporta la compatibilità con le versioni precedenti. Sarà in grado di aprire progetti creati dalla versione precedente di SSMA.  
  
**Command**  
  
Salva progetto  
  
Salva il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Chiudi progetto  
  
Chiude il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>Comandi di File Script di database connessione  
I comandi di connessione al Database consentono di connettersi al database.  
  
-   Il **esplorare** funzionalità dell'interfaccia utente non è supportata nella console.  
  
-   Per altre informazioni su 'Crea file di Script', vedere [creazione di file di Script &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md).  
  
**Command**  
  
database di origine connessione  
  
-   Esegue la connessione al database di origine e carica i metadati a livello elevato di database di origine ma non tutti i metadati.  
  
-   Se non viene stabilita la connessione all'origine, viene generato un errore e l'applicazione console ferma l'ulteriore esecuzione  
  
**Script**  
  
Definizione del server viene recuperato dall'attributo del nome definito per ogni connessione nella sezione server di file di connessione del server o il file di script.  
  
**Esempio di sintassi:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
Force-carico-origine/destinazione-database  
  
-   Carica i metadati di origine.  
  
-   È utile per l'uso nel progetto di migrazione offline.  
  
-   Se non viene stabilita la connessione di origine/destinazione, viene generato un errore e l'applicazione console ferma l'ulteriore esecuzione  
  
**Script**  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
**Esempio di sintassi:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
o Gestione configurazione  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
-   Ristabilisce la connessione al database di origine, ma non carica tutti i metadati a differenza del comando di database di origine di connect.  
  
-   Se (ri) connessione con l'origine non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
-   Si connette al database di SQL Server di destinazione e carica interamente elevato metadati a livello di database di destinazione, ma non nei metadati.  
  
-   Se non viene stabilita la connessione alla destinazione, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
Definizione del server viene recuperato dall'attributo del nome definito per ogni connessione nella sezione server di file di connessione del server o il file di script  
  
**Esempio di sintassi:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   Ristabilisce la connessione al database di destinazione, ma non carica i metadati, a differenza del comando di database di destinazione connect.  
  
-   Se (ri) connessione alla destinazione non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandi di File di Script di report  
I comandi di Report generano i report sulle prestazioni di varie attività di Console SSMA.  
  
**Command**  
  
generate-assessment-report  
  
-   Genera report di valutazione nel database di origine.  
  
-   Se la connessione di database di origine non viene eseguita prima di eseguire questo comando, viene generato un errore e l'applicazione console viene chiusa.  
  
-   Errore di connessione al server di database di origine durante l'esecuzione del comando, comporta anche terminare l'applicazione console.  
  
**Script**  
  
-   `conversion-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti considerati per la generazione di report di valutazione (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **AssessmentReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandi di File di Script di migrazione  
I comandi di migrazione convertire lo schema di database di destinazione per lo schema di origine e la migrazione dei dati al server di destinazione. L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
convert-schema  
  
-   Esegue la conversione dello schema di origine allo schema di destinazione.  
  
-   Se la connessione di database di origine o di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di origine o di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
-   `conversion-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la conversione dello schema (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **SchemaConversionReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oppure  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
eseguire la migrazione di dati: Esegue la migrazione dei dati di origine alla destinazione.  
  
**Script**  
  
-   `conversion-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la migrazione dei dati (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **DataMigrationReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
o Gestione configurazione  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandi File Script di preparazione alla migrazione  
Mapping dello schema tra i database di origine e di destinazione viene iniziata dal comando la preparazione della migrazione.  
  
**Command**  
  
map-schema  
  
Mapping dello schema del database di origine allo schema di destinazione.  
  
**Script**  
  
-   `source-schema` Specifica lo schema di origine che si intende eseguire la migrazione.  
  
-   `sql-server-schema` Specifica lo schema di destinazione in cui desideriamo venga eseguita la migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
**Command**  
  
map-schema  
  
Mapping dello schema del database di origine allo schema di destinazione.  
  
**Script**  
  
`source-schema` Specifica lo schema di origine che si intende eseguire la migrazione.  
  
`sql-server-schema` Specifica lo schema di destinazione in cui desideriamo venga eseguita la migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandi di File di Script di gestibilità  
I comandi di facilità di gestione consentono di sincronizzare gli oggetti di database di destinazione con il database di origine.  
  
L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
synchronize-target  
  
-   Sincronizza gli oggetti di destinazione con il database di destinazione.  
  
-   Se questo comando viene eseguito sul database di origine, viene rilevato un errore.  
  
-   Se la connessione di database di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
-   `object-name:` Specifica gli oggetti di destinazione considerati per la sincronizzazione con database di destinazione (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `on-error:` Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di sincronizzazione (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **TargetSynchronizationReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
o Gestione configurazione  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Command**  
  
aggiornamento da database  
  
-   Aggiorna gli oggetti di origine dal database.  
  
-   Se questo comando viene eseguito sul database di destinazione, viene generato un errore.  
  
**Script**  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
-   `object-name:` Specifica gli oggetti origine considerati per l'aggiornamento dal database di origine (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `on-error:` Specifica se occorre indicare errori di aggiornamento come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di aggiornamento (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **SourceDBRefreshReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
o Gestione configurazione  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandi File Script di generazione script  
I comandi di generazione dello Script seguire due attività: Consentono di salvare la console di output in un file di script. e registrare l'output di T-SQL per la console o un file basato sul parametro specificato.  
  
**Command**  
  
save-as-script  
  
Consente di salvare gli script degli oggetti in un file indicato quando metabase target, si tratta di un'alternativa al comando di sincronizzazione in cui in si ottenere gli script ed eseguire lo stesso nel database di destinazione.  
  
**Script**  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
-   `object-name:` Specifica gli oggetti il cui script devono essere salvati. (Può avere un nome di oggetto gruppo o nomi di oggetto singolo)  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `metabase:` Specifica se è l'origine o destinazione della metabase.  
  
-   `destination:` Specifica il percorso o la cartella in cui lo script deve essere salvato, se il nome del file non viene specificato quindi un nome di file in. Out il formato (valore dell'attributo object_name)  
  
-   `overwrite:` Se true sovrascrive se stesso nome di file esiste. Può avere i valori (true/false).  
  
**Esempio di sintassi:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
convert-sql-statement  
  
-   `context` Specifica il nome dello schema.  
  
-   `destination` Specifica se l'output deve essere archiviato in un file.  
  
    Se questo attributo viene omesso, l'istruzione T-SQL convertita viene visualizzato nella console. (l'attributo facoltativo)  
  
-   `conversion-report-folder` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
-   `conversion-report-overwrite` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-converted-sql-to` Specifica il percorso della cartella in cui viene archiviato il codice T-SQL convertito file (o). Quando viene specificato un percorso di cartella con il `sql-files` attributo, ogni file di origine avrà una destinazione corrispondente file T-SQL creato nella cartella specificata. Quando viene specificato un percorso di cartella con il `sql` attributo, viene scritto il codice T-SQL convertito in un file denominato **Result.out** nella cartella specificata.  
  
-   `sql` Specifica le istruzioni di DB2 sql per la conversione, una o più istruzioni possono essere separate con un ";"  
  
-   `sql-files` Specifica il percorso dei file sql che deve essere convertito in codice T-SQL.  
  
-   `write-summary-report-to` Specifica il percorso in cui verrà generato il report. Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **ConvertSQLReport.XML** viene creato. (l'attributo facoltativo)  
  
    La creazione ha 2 ulteriormente le sottocategorie, una visualizzazione dei report..,:  
  
    -   report-errors (= "true/false", con impostazione predefinita come "false" (attributi facoltativi)).  
  
    -   verbose (= "true/false", con impostazione predefinita come "false" (attributi facoltativi)).  
  
**Script**  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
**Esempio di sintassi:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
o Gestione configurazione  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
oppure  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>Passaggio successivo  
Per informazioni sulle opzioni della riga di comando, vedere [opzioni della riga di comando nella Console SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) .  
  
Per informazioni sui file di script di esempio console, vedere [funziona con i file di Script di esempio Console &#40;DB2ToSQL&#41;](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md)  
  
Il passaggio successivo dipende dai requisiti progetto:  
  
-   Per specificare una password o l'esportazione / importazione per le password, vedere [la gestione delle password &#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md).  
  
-   Per la generazione di report, vedere [generazione di report &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
-   Per risolvere i problemi nella console, vedere [Troubleshooting &#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md).  
  
