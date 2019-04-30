---
title: Esecuzione della Console SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 761cb5368c0b586b63f92952f3938d8708daaf86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183062"
---
# <a name="executing-the-ssma-console-mysqltosql"></a>Esecuzione della console SSMA (MySQLToSQL)
Microsoft offre un solido set di script di comandi del file per eseguire e controllare le attività SSMA.  
  
L'applicazione console utilizza alcuni comandi di file di script standard come enumerate in questa sezione.  
  
## <a name="project--script-file-commands"></a>Comandi di File di progetto Script  
**Command**  
  
create-new-project:   
                   Crea un nuovo progetto SSMA.  
  
I comandi di progetto di gestire la creazione di progetti, apertura, salvataggio e chiusura di progetti.  
  
**Script**  
  
1.  `project-folder` indica la cartella del progetto di creazione.  
  
2.  `project-name` indica il nome del progetto. {string}  
  
3.  `overwrite-if-exists`Attributo facoltativo indica se un progetto esistente deve essere sovrascritti. {boolean}  
  
4.  `project-type:`Attributo facoltativo. Indica il tipo di progetto, ad esempio "sql-server-2005" progetto o il progetto "sql-server-2008" o "sql-server-2012" o "sql-server-2014" progetto o progetto "sql-azure". Valore predefinito è "sql-server-2008".  
  
**Esempio di sintassi:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type=="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"   (optional)  
  
/>  
```  
Attributo 'Sovrascrivi-if-exists' è **false** per impostazione predefinita.  
  
Attributo 'project-type' è **sql Server°2008** per impostazione predefinita.  
  
**Command**  
  
Open-progetto:   
                  Apre un progetto esistente.  
  
**Script**  
  
1.  `project-folder` indica la cartella del progetto di creazione. Il comando ha esito negativo se la cartella specificata non esiste.  {string}  
  
2.  `project-name` indica il nome del progetto. Il comando ha esito negativo se il progetto specificato non esiste.  {string}  
  
**Esempio di sintassi:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> SSMA per MySQL Console applicazione supporta la compatibilità con le versioni precedenti. Sarà in grado di aprire progetti creati dalla versione precedente di SSMA.  
  
**Command**  
  
Save-progetto: Salva il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Chiudi progetto  
                  : Chiude il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Chiudi progetto  
                  : Chiude il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
Attributo 'if-modificata' è facoltativo, **ignorare** per impostazione predefinita.  
  
## <a name="database-connection-script-file-commands"></a>Comandi di File Script di database connessione  
I comandi di connessione al Database consentono di connettersi al database.  
  
1.  Il **esplorare** funzionalità dell'interfaccia utente non è supportata nella console.  
  
2.  Il **l'autenticazione di windows** e **porta** parametri non sono applicabili quando ci si connette a SQL Azure.  
  
3.  Per altre informazioni su 'Crea file di Script', vedere [creazione di file di Script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
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
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
1.  Ristabilisce la connessione al database di origine, ma non carica tutti i metadati a differenza del comando di database di origine di connect.  
  
2.  Se (ri) connessione con l'origine non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
1.  Si connette al database di SQL Server o SQL Azure di destinazione e carica interamente elevato metadati a livello di database di destinazione, ma non nei metadati.  
  
2.  Se non viene stabilita la connessione alla destinazione, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
Definizione del server viene recuperato dall'attributo del nome definito per ogni connessione nella sezione server di file di connessione del server o il file di script  
  
**Esempio di sintassi:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
1.  Ristabilisce la connessione al database di destinazione, ma non carica i metadati, a differenza del comando di database di destinazione connect.  
  
2.  Se (ri) connessione alla destinazione non viene stabilita, viene generato un errore e l'applicazione console ulteriormente interrompe l'esecuzione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandi di File di Script di report  
I comandi di Report generano i report sulle prestazioni di varie attività di Console SSMA.  
  
**Command**  
  
generate-assessment-report  
  
1.  Genera report di valutazione nel database di origine.  
  
2.  Se la connessione di database di origine non viene eseguita prima di eseguire questo comando, viene generato un errore e l'applicazione console viene chiusa.  
  
3.  Errore di connessione al server di database di origine durante l'esecuzione del comando, comporta anche terminare l'applicazione console.  
  
**Script**  
  
1.  `assessment-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
2.  `object-name:` Specifica gli oggetti considerati per la generazione di report di valutazione (può avere un nome di oggetto gruppo o nomi di oggetto singolo).  
  
3.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
4.  `assessment-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
5.  `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **AssessmentReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
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
  
## <a name="migration--script-file-commands"></a>Comandi di File di Script di migrazione  
I comandi di migrazione convertire lo schema di database di destinazione per lo schema di origine e la migrazione dei dati al server di destinazione.  
  
L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
convert-schema  
  
1.  Esegue la conversione dello schema di origine allo schema di destinazione.  
  
2.  Se la connessione di database di origine o di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di origine o di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
1.  `conversion-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
2.  `object-name:` Specifica gli oggetti considerati per la conversione dello schema (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
3.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
4.  `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
5.  `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **SchemaConversionReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report di riepilogo ha due altre categorie secondarie:  
  
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
o Gestione configurazione  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
migrate-data  
  
1.  Esegue la migrazione dei dati di origine alla destinazione.  
  
**Script**  
  
1.  `object-name:` Specifica gli oggetti di origine considerati per la migrazione dei dati (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `write-summary-report-to:` Specifica il percorso in cui verrà generato il report di riepilogo.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **DataMigrationReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="true" verbose="true">  
  
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
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>Comando File Script di preparazione alla migrazione  
Mapping dello schema tra i database di origine e di destinazione viene iniziata dal comando la preparazione della migrazione.  
  
**Command**  
  
map-schema  
  
Mapping dello schema del database di origine allo schema di destinazione.  
  
**Script**  
  
1.  `source-schema` Specifica lo schema di origine che si intende eseguire la migrazione.  
  
2.  `sql-server-schema` Specifica lo schema di destinazione in cui desideriamo venga eseguita la migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandi di File di Script di gestibilità  
I comandi di facilità di gestione consentono di sincronizzare gli oggetti di database di destinazione con il database di origine.  
  
> [!NOTE]  
> L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
synchronize-target  
  
1.  Sincronizza gli oggetti di destinazione con il database di destinazione.  
  
2.  Se questo comando viene eseguito sul database di origine, viene rilevato un errore.  
  
3.  Se la connessione di database di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
1.  `object-name:` Specifica gli oggetti considerati per la sincronizzazione con database di destinazione (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `on-error:` Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di sincronizzazione (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **TargetSynchronizationReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
  
1.  Aggiorna gli oggetti di origine dal database.  
  
2.  Se questo comando viene eseguito sul database di destinazione, viene generato un errore.  
  
**Script**  
  
1.  `object-name:` Specifica gli oggetti origine considerati per l'aggiornamento dal database di origine (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `on-error:` Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di sincronizzazione (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **SourceDBRefreshReport.XML** viene creato.  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
**Esempio di sintassi:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
  
1.  `object-name:` Specifica gli oggetti il cui script devono essere salvati. (Può avere un nome di oggetto gruppo o nomi di oggetto individuali)  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `metabase:` Specifica se è l'origine o destinazione della metabase.  
  
4.  `destination:` Specifica il percorso o la cartella in cui lo script deve essere salvato, se il nome del file non viene specificato quindi un nome di file in. Out il formato (valore dell'attributo object_name)  
  
5.  `overwrite:` Se true sovrascrive se stesso nome di file esiste. Può avere i valori (true/false).  
  
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
**Command**  
  
convert-sql-statement  
  
1.  `context` Specifica il nome dello schema.  
  
2.  `destination` Specifica se l'output deve essere archiviato in un file.  
  
    Se questo attributo viene omesso, l'istruzione T-SQL convertita viene visualizzato nella console. (l'attributo facoltativo)  
  
3.  `conversion-report-folder` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
4.  `conversion-report-overwrite` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
5.  `write-converted-sql-to` Specifica il percorso della cartella in cui viene archiviato il codice T-SQL convertito file (o). Quando viene specificato un percorso di cartella con il `sql-files` attributo, ogni file di origine avrà una destinazione corrispondente file T-SQL creato nella cartella specificata. Quando viene specificato un percorso di cartella con il `sql` attributo, l'istruzione T-SQL convertito viene scritto in un file denominato Result.out sotto la cartella specificata.  
  
6.  `sql` Specifica le istruzioni sql MySQL da convertire, una o più istruzioni possono essere separati usando un ";"  
  
7.  `sql-files` Specifica il percorso dei file sql che deve essere convertito in codice T-SQL.  
  
8.  `write-summary-report-to` Specifica il percorso in cui verrà generato il report di riepilogo. Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **ConvertSQLReport.XML** viene creato. (l'attributo facoltativo)  
  
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
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
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
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
o Gestione configurazione  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Passaggio successivo  
Per informazioni sulle opzioni della riga di comando, vedere [opzioni della riga di comando nella Console SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
Per altre informazioni sui file di script di esempio console, vedere [funziona con i file di Script di esempio Console &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
Il passaggio successivo dipende dai requisiti progetto:  
  
1.  Per specificare una password o l'esportazione / importazione per le password, vedere [la gestione delle password &#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  Per la generazione di report, vedere [generazione di report &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  Per risolvere i problemi nella console, vedere [Troubleshooting &#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  
