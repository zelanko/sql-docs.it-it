---
title: Esecuzione della Console SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cbdd0a1394114e3fdef0511c7ed14658f7dd9b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126304"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Esecuzione della console SSMA (SybaseToSQL)
Microsoft offre un solido set di script di comandi del file per eseguire e controllare le attività SSMA. Le sezioni che seguono in modo dettagliato lo stesso.  
  
## <a name="script-file-commands"></a>Comandi di file di script  
L'applicazione console utilizza alcuni comandi di file di script standard come enumerate in questa sezione.  
  
## <a name="project-commands"></a>Comandi di progetto  
I comandi di progetto di gestire la creazione di progetti, apertura, salvataggio e chiusura di progetti.  
  
### <a name="create-new-project"></a>create-new-project  
Questo comando crea un nuovo progetto SSMA.  
  
-   `project-folder` indica la cartella del progetto di creazione.  
  
-   `project-name` indica il nome del progetto. {string}  
  
-   `overwrite-if-exists`Attributo facoltativo indica se è necessario sovrascrivere un progetto esistente. {boolean}  
  
-   `project-type:`Attributo facoltativo. Indica il tipo di progetto, che è progetto "sql-server-2005" o "sql-server-2008" progetto o progetto "sql-server-2012" o "sql-server-2014" progetto o un progetto "sql-azure". Valore predefinito è "sql server 2008."  
  
**Esempio di sintassi:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
Attributo 'Sovrascrivi-if-exists' è **false** per impostazione predefinita.  
  
Attributo 'project-type' è **sql Server°2008** per impostazione predefinita.  
  
### <a name="open-project"></a>Apri progetto  
Questo comando apre il progetto.

-   `project-folder` indica la cartella del progetto di creazione. Il comando ha esito negativo se la cartella specificata non esiste.  {string}  
  
-   `project-name` indica il nome del progetto. Il comando ha esito negativo se il progetto specificato non esiste.  {string}  
  
**Esempio di sintassi:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA per l'applicazione Console di SAP ASE supporta la compatibilità con le versioni precedenti. È possibile usarlo per aprire i progetti creati dalla versione precedente di SSMA.  
  
### <a name="save-project"></a>Salva progetto  
Questo comando Salva il progetto di migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>Chiudi progetto  
Questo comando chiude il progetto di migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
Attributo 'if-modificata' è facoltativo, **ignorare** per impostazione predefinita.  
  
## <a name="database-connection-commands"></a>Comandi di connessione di database  
I comandi di connessione al Database consentono di connettersi al database.  
  
> [!NOTE]  
> - Il **esplorare** funzionalità dell'interfaccia utente non è supportata nella console.  
> - Per altre informazioni su 'Crea file di Script', vedere [creazione di file di Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>database di origine connessione  
Questo comando esegue la connessione al database di origine e carica i metadati di alto livello di database di origine, ma non tutti i metadati.
  
Se non viene stabilita la connessione all'origine, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.
  
La definizione del server viene recuperata dall'attributo del nome definito per ogni connessione nella sezione server di file di connessione del server o il file di script.  
  
**Esempio di sintassi:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>Force-carico-origine/destinazione-database  
Questo comando Carica i metadati di origine, ed è utile per l'uso nel progetto di migrazione offline.  
  
Se non viene stabilita la connessione di origine/destinazione, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
Questo comando richiede uno o più nodi di metabase come parametro della riga di comando.  
  
**Esempio di sintassi:**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>reconnect-source-database  
Questo comando ristabilisce la connessione al database di origine ma non può caricare i metadati a differenza del comando di database di origine di connect.  
  
Se (ri) connessione con l'origine non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>connect-target-database  
Questo comando si connette al database di SQL Server di destinazione e carica interamente i metadati di alto livello del database di destinazione, ma non i metadati.  
  
Se non viene stabilita la connessione alla destinazione, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
La definizione del server viene recuperata dall'attributo del nome definito per ogni connessione nella sezione server di file di connessione del server o il file di script.  
  
**Esempio di sintassi:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
Questo comando ristabilisce la connessione al database di destinazione ma non può caricare i metadati, a differenza del comando di database di destinazione connect.  
  
Se (ri) connessione alla destinazione non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Comandi del report  
I comandi di Report generano i report sulle prestazioni di varie attività di Console SSMA.  
  
### <a name="generate-assessment-report"></a>generate-assessment-report  
  
Questo comando genera i report di valutazione nel database di origine.  
  
Se la connessione di database di origine non viene eseguita prima di eseguire questo comando, viene generato un errore e l'applicazione console viene chiusa.  
  
Errore di connessione al server di database di origine durante l'esecuzione del comando, comporta anche terminare l'applicazione console.  
  
-   `conversion-report-folder:` Specifica la cartella in cui possono essere archiviati i report di valutazione. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti considerati per la generazione di report di valutazione (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto chiamato nell'attributo nome di oggetto (se viene specificato, categoria dell'oggetto tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **AssessmentReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report è suddivisi ulteriormente:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oppure  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>Comandi di migrazione  
I comandi di migrazione convertire lo schema del database di destinazione per lo schema di origine e la migrazione dei dati al server di destinazione.  
  
### <a name="convert-schema"></a>convert-schema  
Questo comando esegue la conversione dello schema di origine allo schema di destinazione.  
  
Se la connessione di database di origine o di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di origine o di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
-   `conversion-report-folder:` Specifica una cartella in cui possono essere archiviati i report di valutazione. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la conversione dello schema (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto chiamato nell'attributo nome di oggetto (se viene specificato, categoria dell'oggetto tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **SchemaConversionReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report è suddivisi ulteriormente:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>migrate-data  
Questo comando esegue la migrazione dei dati di origine alla destinazione.  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la migrazione dei dati (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto chiamato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **DataMigrationReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report è suddivisi ulteriormente:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
oppure  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Comando di preparazione alla migrazione  
Mapping dello schema tra i database di origine e di destinazione viene iniziata dal comando la preparazione della migrazione.  
  
> [!NOTE]  
> L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
### <a name="map-schema"></a>map-schema  
Questo comando fornisce il mapping dello schema del database di origine allo schema di destinazione.  
  
-   `source-schema` Specifica lo schema di origine per eseguire la migrazione.  
  
-   `sql-server-schema` Specifica lo schema di destinazione a cui verrà eseguita la migrazione dello schema di origine.  
  
**Esempio di sintassi:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Comandi di gestibilità  
I comandi di facilità di gestione consentono di sincronizzare gli oggetti di database di destinazione con il database di origine.  
  
> [!NOTE]  
> L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
### <a name="synchronize-target"></a>synchronize-target  
Questo comando consente di sincronizzare gli oggetti di destinazione con il database di destinazione.  
 
Se questo comando viene eseguito sul database di origine, viene rilevato un errore.  
  
Se la connessione di database di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
-   `object-name:` Specifica gli oggetti di destinazione considerati per la sincronizzazione con database di destinazione (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto chiamato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `on-error:` Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Specifica percorso del report di errore per l'operazione di sincronizzazione (attributo facoltativo). Se viene fornito percorso della cartella, solo file in base al nome **TargetSynchronizationReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
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
  
### <a name="refresh-from-database"></a>aggiornamento da database  
Questo comando Aggiorna gli oggetti di origine dal database.  
  
Se questo comando viene eseguito sul database di destinazione, viene generato un errore.  
  
Questo comando richiede uno o più nodi di metabase come parametro della riga di comando.  
  
-   `object-name:` Specifica gli oggetti origine considerati per l'aggiornamento dal database di origine (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `on-error:` Specifica se chiamare l'aggiornamento degli errori come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Specifica percorso del report di errore per l'operazione di aggiornamento (attributo facoltativo). Se viene fornito percorso della cartella, solo file in base al nome **SourceDBRefreshReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
oppure  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Comandi di generazione script  
I comandi di generazione dello Script eseguono due attività: consentono di salvare l'output in un file di script della console e registrano l'output di T-SQL per la console o un file basato sul parametro specificato.  
  
### <a name="save-as-script"></a>save-as-script  
Questo comando viene utilizzato per salvare gli script degli oggetti in un file indicato quando metabase target. Si tratta di un'alternativa al comando di sincronizzazione in quanto è ottenere gli script ed eseguire lo stesso nel database di destinazione.  
  
Questo comando richiede uno o più nodi di metabase come parametro della riga di comando.  
  
-   `object-name:` Specifica gli oggetti il cui script devono essere salvati (nomi di singoli oggetti supporta o un nome di oggetto gruppo).  
  
-   `object-type:` Specifica il tipo dell'oggetto chiamato nell'attributo nome di oggetto (se viene specificato, categoria dell'oggetto tipo di oggetto sarà "category").  
  
-   `metabase:` Specifica se è l'origine o destinazione della metabase.  
  
-   `destination:` Specifica il percorso o la cartella in cui deve essere salvato lo script. Se il nome del file non viene specificato, verrà fornito un nome di file in. Out il formato (valore dell'attributo object_name).
  
-   `overwrite:` Se true, lo sovrascrive lo stesso nome file se esiste. Può avere i valori (true/false).  
  
**Esempio di sintassi:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
o Gestione configurazione  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql-statement
Questo comando Converte l'istruzione SQL.  
  
-   `context` Specifica il nome dello schema.  
  
-   `destination` Specifica se l'output deve essere archiviato in un file.  
  
    Se questo attributo viene omesso, l'istruzione T-SQL convertita viene visualizzato nella console. (l'attributo facoltativo)  
  
-   `conversion-report-folder` Specifica la cartella in cui possono essere archiviati i report di valutazione. (l'attributo facoltativo)  
  
-   `conversion-report-overwrite` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-converted-sql-to` Specifica il percorso della cartella file (o) per cui devono essere archiviati convertito T-SQL. Quando viene specificato un percorso di cartella con il `sql-files` , ogni file di origine e presenta una destinazione corrispondente file T-SQL creato nella cartella specificata. Quando viene specificato un percorso di cartella con il `sql` attributo, l'istruzione T-SQL convertito viene scritto in un file denominato Result.out sotto la cartella specificata.  
  
-   `sql` Specifica le istruzioni sql Sybase da convertire, una o più istruzioni possono essere separate con un ";"  
  
-   `sql-files` Specifica il percorso dei file sql che deve essere convertito in codice T-SQL.  
  
-   `write-summary-report-to` Specifica il percorso in cui verrà generato il report di riepilogo. Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **ConvertSQLReport.XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report di riepilogo ha altre possono essere suddivisi, vale a dire:  
  
    -   report-errors (= "true/false", con impostazione predefinita come "false" (attributi facoltativi)).  
  
    -   verbose (= "true/false", con impostazione predefinita come "false" (attributi facoltativi)).  
  
Questo comando richiede uno o più nodi di metabase come parametro della riga di comando.  
  
**Esempio di sintassi:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
o Gestione configurazione  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
oppure  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>Passaggi successivi  
Per informazioni sulle opzioni della riga di comando, vedere [opzioni della riga di comando nella Console SSMA (AccessToSQL)](../access/command-line-options-in-ssma-console-accesstosql.md).  
  
Per informazioni su un file di script di esempio console, vedere [funziona con i file di Script di esempio Console &#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
Il passaggio successivo dipende dai requisiti progetto:  
  
-   Per specificare una password o l'esportazione / importazione per le password, vedere [la gestione delle password &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Per la generazione di report, vedere [generazione di report &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Per risolvere i problemi nella console, vedere [Troubleshooting &#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
