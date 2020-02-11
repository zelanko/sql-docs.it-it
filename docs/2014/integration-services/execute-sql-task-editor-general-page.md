---
title: Editor attività Esegui SQL (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96d211defa789888a3fd7b513b4dff60fa795cb6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058993"
---
# <a name="execute-sql-task-editor-general-page"></a>Editor attività Esegui XML (pagina Generale)
  Usare la pagina **Generale** della finestra di dialogo **Editor attività Esegui SQL** per configurare l'attività Esegui SQL e specificare l'istruzione SQL eseguita dall'attività.  
  
 Per altre informazioni su questa attività, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md), [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md), e [Set di risultati nell'attività Esegui SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md). Per sapere di più sul linguaggio di query Transact-SQL, vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Esegui SQL nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di immettere una descrizione per l'attività Esegui SQL. È consigliabile includere nella descrizione informazioni sugli scopi dell'attività, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **TimeOut**  
 Consente di specificare il numero massimo di secondi durante i quali l'attività viene eseguita prima del timeout. Il valore 0 indica un tempo infinito. Il valore predefinito è 0.  
  
> [!NOTE]  
>  Il timeout delle stored procedure non si verifica se queste emulano la funzionalità di sospensione specificando un periodo di tempo per la creazione di connessioni e il completamento di transazioni maggiore rispetto al numero di secondi indicato da **TimeOut**. Le stored procedure che eseguono query sono comunque soggette alle restrizioni di tempo specificate da **TimeOut**.  
  
 **CodePage**  
 Consente di specificare la tabella codici da utilizzare durante la conversione di valori Unicode in variabili. Il valore predefinito corrisponde alla tabella codici del computer locale.  
  
> [!NOTE]  
>  Quando l'attività Esegui SQL usa una gestione connessione ADO o ODBC, la proprietà **CodePage** non è disponibile. Se la soluzione richiede l'utilizzo di una tabella codici, utilizzare una gestione connessione OLE DB o ADO.NET con l'attività Esegui SQL.  
  
 **TypeConversionMode**  
 Se si imposta questa proprietà su `Allowed`, l'attività Esegui SQL tenterà di convertire il parametro di output e i risultati della query nel tipo di dati della variabile a cui sono assegnati i risultati. Si applica al tipo di set di risultati **Riga singola** .  
  
 **ResultSet**  
 Consente di specificare il tipo di risultati previsto per un'istruzione SQL in fase di esecuzione. È possibile scegliere tra **Riga singola**, **Set dei risultati completo**, **XML**o **Nessuno**.  
  
 **ConnectionType**  
 Consente di scegliere il tipo di gestione connessione da utilizzare per la connessione a un'origine dati. I tipi di connessione disponibili includono **OLE DB**, **ODBC**, **ADO**, **ADO.NET** e **SQLMOBILE**.  
  
 **Argomenti correlati:** [gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md), [gestione connessione ODBC](connection-manager/odbc-connection-manager.md), [gestione connessione ADO](connection-manager/ado-connection-manager.md), gestione connessione [ADO.NET](connection-manager/ado-net-connection-manager.md), gestione connessione [SQL Server Compact edizione](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Connessione**  
 Consente di scegliere una connessione da un elenco di gestioni connessione definite. Per creare una nuova connessione, selezionare \< **nuova connessione...**>.  
  
 **SQLSourceType**  
 Consente di selezionare il tipo di origine dell'istruzione SQL eseguita dall'attività.  
  
 A seconda del tipo di gestione connessione utilizzato dall'attività Esegui SQL, è necessario utilizzare indicatori di parametro specifici nelle istruzioni SQL con parametri.  
  
 **Argomenti correlati:** Sezione esecuzione di comandi SQL con parametri nell' [attività Esegui SQL](control-flow/execute-sql-task.md)  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un'istruzione Transact-SQL. Selezionando questo valore, verrà visualizzata l'opzione dinamica **SQLStatement**.|  
|**Connessione file**|Consente di selezionare un file contenente un'istruzione Transact-SQL. Impostando questa opzione, verrà visualizzata l'opzione dinamica **FileConnection**.|  
|**Variabile**|Consente di impostare l'origine su una variabile che definisce l'istruzione Transact-SQL. Se si seleziona questo valore, viene visualizzata l'opzione dinamica **SourceVariable**.|  
  
 **QueryIsStoredProcedure**  
 Indica se l'istruzione SQL specificata da eseguire è una stored procedure. Questa proprietà è di lettura/scrittura solo se l'attività utilizza una gestione connessione ADO. Altrimenti, la proprietà è di sola lettura e il relativo valore è `false`.  
  
 **BypassPrepare**  
 Indica se l'istruzione SQL è stata preparata.  Il valore `true` ignora la preparazione, il valore `false` prepara l'istruzione SQL prima dell'esecuzione. Questa opzione è disponibile solo con le connessioni OLE DB che supportano la preparazione.  
  
 **Argomenti correlati:**  [esecuzione preparata](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Sfoglia**  
 Individuare un file contenente un'istruzione SQL tramite la finestra di dialogo **Apri** . Selezionare un file per copiarne il contenuto sotto forma di istruzione SQL nella proprietà **SQLStatement** .  
  
 **Compila query**  
 Consente di creare un'istruzione SQL tramite la finestra di dialogo **Generatore query** , uno strumento grafico usato per la creazione di query. Questa opzione è disponibile quando l'opzione **SQLSourceType** è impostata su **Input diretto**.  
  
 **Analizza query**  
 Consente di convalidare la sintassi dell'istruzione SQL.  
  
## <a name="sqlsourcetype-dynamic-options"></a>Opzioni dinamiche SQLSourceType  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Input diretto  
 **SQLStatement**  
 Digitare l'istruzione SQL da eseguire nella casella di opzione oppure fare clic sul pulsante (...) per digitare l'istruzione SQL nella finestra di dialogo **Immetti query SQL** o fare clic su **Compila query** per comporre l'istruzione con la finestra di dialogo **Generatore di query**.  
  
 **Argomenti correlati:** [Generatore di query](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Connessione file  
 **FileConnection**  
 Selezionare una gestione connessione file esistente o fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variabile  
 **SourceVariable**  
 Selezionare una variabile esistente oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Esegui SQL &#40;pagina Mapping parametri&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Editor attività Esegui SQL &#40;pagina del set di risultati&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
