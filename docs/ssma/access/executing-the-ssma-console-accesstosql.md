---
title: Esecuzione della Console SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 97425a6795889f72b329280ff70f9638378e7799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006565"
---
# <a name="executing-the-ssma-console-accesstosql"></a>Esecuzione della Console SSMA (AccessToSQL)
Microsoft offre un solido set di comandi di file di script e opzioni della riga di comando per eseguire e controllare le attività SSMA. Le sezioni che seguono in modo dettagliato lo stesso.  
  
## <a name="project--script-file-commands"></a>Comandi di File di progetto Script  
I comandi di progetto di gestire la creazione di progetti, apertura, salvataggio e chiusura di progetti.  
  
**Command**  
  
Crea-nuovo-progetto: Crea un nuovo progetto SSMA.  
  
**Script**  
  
-   `project-folder` indica la cartella del progetto di creazione.  
  
-   `project-name` indica il nome del progetto. {string}  
  
-   `overwrite-if-exists`Attributo facoltativo indica se un progetto esistente deve essere sovrascritti. {boolean}  
  
-   `project-type` è un attributo facoltativo.  Le opzioni seguenti sono disponibili per il tipo di progetto:  
  
    -   sql-server-2005  
  
    -   sql-server-2008  
  
    -   sql-server-2012  
  
    -   sql-server-2014  
  
    -   sql-server-2016  
  
    -   sql-azure  
  
    Valore predefinito è "sql-server-2008".  
  
**Esempio:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
Attributo 'Sovrascrivi-if-exists' è **false** per impostazione predefinita.  
  
Attributo 'project-type' è **sql Server°2008** per impostazione predefinita.  
  
**Command**  
  
Open-progetto: Apre un progetto esistente.  
  
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
**Nota:** L'applicazione Console SSMA per Access supporta la compatibilità con le versioni precedenti. Sarà in grado di aprire progetti creati dalla versione precedente di SSMA.  
  
**Command**  
  
Save-progetto: Salva il progetto di migrazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Chiudi-progetto: Chiude il progetto di migrazione.  
  
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
  
Il **esplorare** funzionalità dell'interfaccia utente non è supportata nella console.  
  
Il **l'autenticazione di windows** e **porta** parametri non sono applicabili quando ci si connette a SQL Azure.  
  
Per altre informazioni su 'Crea file di Script', vedere [creazione di file di Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
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
  
caricamento-accesso-database: Consente di caricare i file di database di access  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
oppure  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
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
<force-load  
  
  object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
oppure  
  
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
  
-   Si connette al database di SQL Server o SQL Azure di destinazione e carica interamente elevato metadati a livello di database di destinazione, ma non nei metadati.  
  
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
  
generare report di valutazione  
  
-   Genera report di valutazione nel database di origine.  
  
-   Se la connessione di database di origine non viene eseguita prima di eseguire questo comando, viene generato un errore e l'applicazione console viene chiusa.  
  
-   Errore di connessione al server di database di origine durante l'esecuzione del comando, comporta anche terminare l'applicazione console.  
  
**Script**  
  
-   `assessment-report-folder:` Specifica una cartella in cui il report di valutazione può essere archiviati. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti considerati per la generazione di report di valutazione (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `assessment-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **AssessmentReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oppure  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandi di File di Script di migrazione  
I comandi di migrazione convertire lo schema di database di destinazione per lo schema di origine e la migrazione dei dati al server di destinazione.  
  
L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
convert-schema  
  
-   Esegue la conversione dello schema di origine allo schema di destinazione.  
  
-   Se la connessione di database di origine o di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di origine o di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
-   `conversion-report-folder:` Specifica cartella dove è possibile archiviare il report di valutazione. (l'attributo facoltativo)  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la conversione dello schema (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `conversion-report-overwrite:` Specifica se sovrascrivere la cartella di report di valutazione se esiste già.  
  
    **Il valore predefinito:** false. (l'attributo facoltativo)  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **SchemaConversionReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
oppure  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Command**  
  
migrate-data  
  
1.  Esegue la migrazione dei dati di origine alla destinazione.  
  
**Script**  
  
-   `object-name:` Specifica gli oggetti di origine considerati per la migrazione dei dati (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
-   `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
-   `write-summary-report-to:` Specifica il percorso in cui verrà generato il report.  
  
    Se viene specificato solo il percorso della cartella, quindi l'opzione file in base al nome **DataMigrationReport&lt;n&gt;. XML** viene creato. (l'attributo facoltativo)  
  
    La creazione di report ha due altre categorie secondarie:  
  
    -   `report-errors` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
    -   `verbose` (= "true/false", con impostazione predefinita come "false" (attributi facoltativi))  
  
**Esempio di sintassi:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
oppure  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Command**  
  
collegamento-tabelle: Questo comando Collega la tabella di origine (accesso) nella tabella di destinazione.  
  
**Script**  
  
**Esempio di sintassi:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
oppure  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Command**  
  
Scollega-tabelle: Questo comando consente di scollegare la tabella di origine (accesso) della tabella di destinazione.  
  
**Script**  
  
**Esempi di sintassi:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
oppure  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandi File Script di preparazione alla migrazione  
Mapping dello schema tra i database di origine e di destinazione viene iniziata dal comando la preparazione della migrazione.  
  
**Command**  
  
map-schema: Mapping dello schema del database di origine allo schema di destinazione.  
  
**Script**  
  
-   `source-schema` Specifica lo schema di origine che si intende eseguire la migrazione.  
  
-   `sql-server-schema` Specifica lo schema di destinazione in cui desideriamo venga eseguita la migrazione.  
  
**Esempio di sintassi:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Comandi di gestibilità  
I comandi di facilità di gestione consentono di sincronizzare gli oggetti di database di destinazione con il database di origine.  
  
L'output di console predefinito impostazione per i comandi di migrazione è il report di output 'Full' con nessun report di errore dettagliato: Riepilogo solo dal nodo radice dell'albero di origine oggetto.  
  
**Command**  
  
synchronize-target  
  
1.  Sincronizza gli oggetti di destinazione con il database di destinazione.  
  
2.  Se questo comando viene eseguito sul database di origine, viene rilevato un errore.  
  
3.  Se la connessione di database di destinazione non viene eseguita prima di eseguire questo comando o la connessione al server di database di destinazione non riesce durante l'esecuzione del comando, viene generato un errore e l'applicazione console viene chiusa.  
  
**Script**  
  
1.  `object-name:` Specifica gli oggetti di destinazione considerati per la sincronizzazione con database di destinazione (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `on-error:` Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   -Totale report come avviso  
  
    -   report-each-come-avviso  
  
    -   Errore-script  
  
4.  `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di sincronizzazione (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **TargetSynchronizationReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
oppure  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
oppure  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Command**  
  
aggiornamento da database  
  
-   Aggiorna gli oggetti di origine dal database.  
  
-   Se questo comando viene eseguito sul database di destinazione, viene generato un errore.  
  
**Script**  
  
Richiede uno o più nodi di metabase come parametro della riga di comando.  
  
1.  `object-name:` Specifica gli oggetti origine considerati per l'aggiornamento dal database di origine (può avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
2.  `object-type:` Specifica il tipo dell'oggetto specificato nell'attributo nome di oggetto (se categoria dell'oggetto è specificato il tipo di oggetto sarà "category").  
  
3.  `on-error:` Specifica se occorre indicare errori di aggiornamento come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
    -   -Totale report come avviso  
  
    -   report-each-come-avviso  
  
    -   Errore-script  
  
4.  `report-errors-to:` Specifica percorso di segnalazione errori per l'operazione di aggiornamento (attributo facoltativo) se viene fornito percorso della cartella, solo del file in base al nome **SourceDBRefreshReport.XML** viene creato.  
  
**Esempio di sintassi:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
oppure  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
oppure  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandi File Script di generazione script  
La generazione di Script, i comandi consentono di salvare l'output della console in un file di script.  
  
**Command**  
  
come Save-script  
  
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
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
oppure  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Passaggio successivo  
Per informazioni sulle opzioni della riga di comando, vedere [opzioni della riga di comando nella Console SSMA &#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Per informazioni sui file di script di esempio console, vedere [funziona con il FilesExecuting Script di esempio Console della Console SSMA &#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
Il passaggio successivo dipende dai requisiti progetto:  
  
-   Per specificare una password o l'esportazione / importazione per le password, vedere [la gestione delle password &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Per la generazione di report, vedere [generazione di report &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Per risolvere i problemi nella console, vedere [Troubleshooting &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
