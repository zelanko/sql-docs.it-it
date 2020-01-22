---
title: Strumenti per la risoluzione dei problemi relativi all'esecuzione dei pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cd39b7315903335fe2370ae148579f3fe9d07abc
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637808"
---
# <a name="troubleshooting-tools-for-package-execution"></a>Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include funzionalità e strumenti per la risoluzione dei problemi che possono verificarsi quando si eseguono i pacchetti dopo averli completati e distribuiti.  
  
 In fase di progettazione, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] offre punti di interruzione che consentono di sospendere l'esecuzione dei pacchetti, una finestra di stato e visualizzatori dati che consentono di visualizzare il passaggio dei dati nel flusso di dati. Queste funzionalità non sono tuttavia disponibili quando si eseguono i pacchetti distribuiti. Le tecniche principali per la risoluzione dei problemi relativi ai pacchetti distribuiti sono le seguenti:  
  
-   Intercettazione e gestione degli errori dei pacchetti tramite gestori di eventi.  
  
-   Acquisizione dei dati errati tramite output degli errori.  
  
-   Registrazione dei passaggi dell'esecuzione dei pacchetti.  
  
 Per evitare problemi relativi all'esecuzione di pacchetti, è inoltre possibile utilizzare le tecniche e i suggerimenti seguenti.  
  
-   **Verifica dell'integrità dei dati tramite transazioni**. Per altre informazioni, vedere [Transazioni di Integration Services](../integration-services-transactions.md).  
  
-   **Riavvio dei pacchetti dal punto di errore tramite checkpoint**. Per altre informazioni, vedere [Riavvio dei pacchetti tramite checkpoint](../packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>Intercettazione e gestione degli errori dei pacchetti tramite gestori di eventi  
 I gestori degli eventi consentono di rispondere ai molti eventi generati dal pacchetto e dai relativi oggetti.  
  
-   **Creazione di un gestore dell'evento per l'evento OnError**. Nel gestore dell'evento è possibile utilizzare un'attività Invia messaggi per inviare a un amministratore una notifica dell'errore, utilizzare un'attività Script e la logica personalizzata per ottenere informazioni di sistema per la risoluzione dei problemi oppure eliminare le risorse temporanee o l'output incompleto. Per altre informazioni, vedere [Gestori eventi di Integration Services &#40;SSIS&#41;](../integration-services-ssis-event-handlers.md).  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>Risoluzione dei problemi relativi ai dati errati tramite output degli errori  
 È possibile utilizzare l'output degli errori disponibile in numerosi componenti flusso di dati per indirizzare le righe contenenti errori a una destinazione distinta, per un'analisi successiva.  
  
-   **Acquisizione dei dati errati tramite output degli errori**. È possibile inviare le righe contenenti errori a una destinazione distinta, ad esempio una tabella degli errori o un file di testo. Tramite l'output degli errori vengono aggiunte automaticamente due colonne numeriche contenenti il numero dell'errore a causa del quale la riga è stata rifiutata e l'ID della colonna in cui si è verificato l'errore. Per altre informazioni, vedere [Gestione degli errori nei dati](../data-flow/error-handling-in-data.md).  
  
-   **Aggiunta di informazioni descrittive agli output degli errori**. Per semplificare l'analisi dell'output degli errori, oltre ai due identificatori numerici specificati dall'output stesso è possibile aggiungere informazioni descrittive.  
  
     **Aggiungere la descrizione dell'errore**. Utilizzando un componente script, è possibile analizzare in modo semplice la descrizione dell'errore. Per ulteriori informazioni, vedere [miglioramento di un output degli errori per il componente script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
     **Aggiungere il nome della colonna Error**. Per informazioni sul nome della colonna corrispondente all'ID di colonna salvato dall'output degli errori non è sufficiente il componente script, ma sono necessarie ulteriori operazioni. Ogni ID di colonna in un flusso di dati è univoco all'interno dell'attività Flusso di dati ed è persistente nel pacchetto in fase di progettazione. L'approccio seguente consente di aggiungere il nome di colonna all'output degli errori. Per un esempio di come usare questo approccio, vedere [aggiunta del nome della colonna errore a un output degli errori](https://go.microsoft.com/fwlink/?LinkId=261546) in dougbert.com.  
  
    1.  **Creare una tabella di ricerca di nomi di colonna**. Creare un'applicazione separata in cui viene utilizzata l'API di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per eseguire un'iterazione su ogni pacchetto salvato, ogni flusso di dati nel pacchetto, ogni oggetto nel flusso di dati e ogni input e output nell'oggetto del flusso di dati. Nell'applicazione l'ID di colonna e il nome di ogni colonna devono essere persistenti nella tabella di ricerca, insieme all'ID dell'attività Flusso di dati padre e a quello del pacchetto.  
  
    2.  **Aggiungere il nome della colonna all'output**. Aggiungere all'output degli errori una trasformazione Ricerca che consenta di eseguire una ricerca del nome della colonna nella tabella di ricerca creata al passaggio precedente. Per la ricerca è possibile utilizzare l'ID di colonna nell'output degli errori, l'ID di pacchetto, disponibile nella variabile di sistema System::PackageID, e l'ID dell'attività Flusso di dati, disponibile nella variabile di sistema System::TaskID.  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>Risoluzione dei problemi relativi all'esecuzione di pacchetti tramite i report delle operazioni  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono disponibili report delle operazioni standard per facilitare il monitoraggio dei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che sono stati distribuiti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Con i report relativi ai pacchetti è possibile visualizzare lo stato e la cronologia dei pacchetti e, se necessario, identificare la causa di eventuali errori.  
  
 Per altre informazioni, vedere [Risoluzione dei problemi relativi ai report per l'esecuzione del pacchetto](troubleshooting-reports-for-package-execution.md).  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>Risoluzione dei problemi relativi all'esecuzione di pacchetti tramite viste SSISDB  
 Sono disponibili diverse viste di database SSISDB su cui è possibile eseguire una query per monitorare l'esecuzione dei pacchetti e altre informazioni sulle operazioni. Per ulteriori informazioni, vedere [monitoraggio per le esecuzioni di pacchetti e altre operazioni](../performance/monitor-running-packages-and-other-operations.md).  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>Risoluzione dei problemi relativi all'esecuzione di pacchetti tramite la registrazione  
 Abilitando la registrazione è possibile tenere traccia di ciò che avviene durante l'esecuzione dei pacchetti. I provider di log consentono di acquisire informazioni sugli eventi specificati da utilizzare per un'analisi successiva e di salvare tali informazioni in una tabella di database, in un file flat, in un file XML o in un altro formato di output supportato.  
  
-   **Abilitazione della registrazione**. È possibile ottimizzare l'output di registrazione selezionando solo gli eventi e le informazioni che si desidera acquisire. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md).  
  
-   **Selezionare l'evento Diagnostic del pacchetto per risolvere i problemi relativi al provider.** Sono presenti messaggi di registrazione per il supporto della risoluzione dei problemi relativi all'interazione di un pacchetto con origini dati esterne. Per altre informazioni, vedere [Risoluzione dei problemi relativi alla connettività dei pacchetti degli strumenti](troubleshooting-tools-for-package-connectivity.md).  
  
-   **Miglioramento dell'output di registrazione predefinito**. La registrazione comporta in genere l'accodamento di righe alla destinazione di registrazione ogni volta che viene eseguito un pacchetto. Sebbene ogni riga dell'output di registrazione identifichi il pacchetto in base al nome e all'identificatore univoco e identifichi inoltre l'esecuzione del pacchetto tramite un identificatore ExecutionID univoco, una grande quantità di output di registrazione in un unico elenco può essere difficile da analizzare.  
  
     L'approccio seguente consente di migliorare l'output di registrazione predefinito e semplificare la generazione di report:  
  
    1.  **Creare una tabella padre per la registrazione di ogni esecuzione di un pacchetto**. In questa tabella padre è inclusa una singola riga per ogni esecuzione di un pacchetto e viene utilizzato l'identificatore ExecutionID per il collegamento ai record figlio nella tabella di registrazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. È possibile utilizzare un'attività Esegui SQL all'inizio di ogni pacchetto per creare questa nuova riga e registrare l'ora di inizio. È quindi possibile utilizzare un'altra attività Esegui SQL alla fine del pacchetto per aggiornare la riga con ora di fine, durata e stato.  
  
    2.  **Aggiungere informazioni di controllo al flusso di dati**. È possibile utilizzare la trasformazione Controllo per aggiungere alle righe del flusso di dati informazioni sull'esecuzione del pacchetto che ha creato o modificato ogni riga. La trasformazione Controllo rende disponibili nove informazioni, incluse quelle relative a PackageName ed ExecutionInstanceGUID. Per altre informazioni, vedere [Trasformazione Controllo](../data-flow/transformations/audit-transformation.md). Se si desidera includere in ogni riga informazioni personalizzate a scopo di controllo, è possibile aggiungere le informazioni desiderate alle righe del flusso di dati utilizzando una trasformazione Colonna derivata. Per altre informazioni, vedere [Trasformazione Colonna derivata](../data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Valutare l'opportunità di acquisire i dati sul conteggio delle righe**. Prendere in considerazione la creazione di una tabella separata per le informazioni sul conteggio delle righe, in cui ogni istanza di esecuzione di un pacchetto è identificata tramite il relativo ExecutionID. Utilizzare la trasformazione Conteggio righe per salvare il conteggio delle righe in una serie di variabili in punti critici del flusso di dati. Al termine del flusso di dati, utilizzare un'attività Esegui SQL per inserire le serie di valori in una riga della tabella, per operazioni successive di analisi e creazione di report.  
  
     Per altre informazioni su questo approccio, vedere la sezione relativa a registrazione e controllo ETL nel white paper [!INCLUDE[msCoName](../../includes/msconame-md.md)] [Progetto REAL: progettazione ETL di Business Intelligence](https://www.microsoft.com/download/details.aspx?id=14582).  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>Risoluzione dei problemi relativi all'esecuzione di pacchetti tramite i file di dump del debug  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è possibile creare file di dump del debug contenenti informazioni sull'esecuzione di un pacchetto. Per altre informazioni, vedere [Generazione di file di dump per l'esecuzione del pacchetto](generating-dump-files-for-package-execution.md).  
  
## <a name="troubleshoot-run-time-validation-issues"></a>Risoluzione dei problemi relativi alla convalida in fase di esecuzione  
 A volte potrebbe non essere possibile connettersi alle origini dati o convalidare parte dei pacchetti prima di aver eseguito alcune attività nei pacchetti. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include le funzionalità seguenti per permettere di evitare gli errori di convalida che altrimenti si verificherebbero da queste condizioni:  
  
-   **Configurazione della proprietà DelayValidation per gli elementi del pacchetto non validi quando il pacchetto viene caricato**. È possibile impostare la proprietà `DelayValidation` su `True` per gli elementi del pacchetto la cui configurazione non è valida, per impedire errori di convalida quando il pacchetto viene caricato. Potrebbe ad esempio essere presente un'attività Flusso di dati in cui viene utilizzata una tabella di destinazione che non esiste fino a quando non viene creata in fase di esecuzione da un'attività Esegui SQL. La proprietà `DelayValidation` può essere abilitata a livello di pacchetto oppure delle singole attività e dei singoli contenitori del pacchetto.  
  
     La proprietà `DelayValidation` può essere impostata in un'attività Flusso di dati ma non nei singoli componenti flusso di dati. È possibile ottenere un risultato simile impostando la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> dei singoli componenti flusso di dati su `false`. Quando, tuttavia, il valore di questa proprietà è impostato su `false`, il componente non riconosce le modifiche ai metadati delle origini dei dati esterne. Impostando la proprietà `true` su <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A>, è possibile evitare problemi causati da blocchi nel database, in particolare quando nel pacchetto vengono utilizzate transazioni.  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>Risoluzione dei problemi relativi alle autorizzazioni in fase di esecuzione  
 Se si verificano errori quando si cerca di eseguire pacchetti distribuiti tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile che gli account usati non dispongano delle autorizzazioni necessarie. Per informazioni su come risolvere i problemi legati all'esecuzione di pacchetti dai processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Un pacchetto SSIS non viene eseguito quando viene chiamato da un passaggio di processo di SQL Server Agent](https://support.microsoft.com/kb/918760). Per altre informazioni sull'esecuzione di pacchetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Processi di SQL Server Agent per i pacchetti](../packages/sql-server-agent-jobs-for-packages.md).  
  
 Per connettersi a origini dati Excel o Access, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent richiede un account con autorizzazione di lettura, scrittura, creazione ed eliminazione dei file temporanei nella cartella specificata dalle variabili di ambiente TEMP e TMP.  
  
## <a name="troubleshoot-64-bit-issues"></a>Risoluzione dei problemi relativi ai componenti a 64 bit  
  
-   **Alcuni provider di dati non sono disponibili nella piattaforma a 64 bit**. In particolare, il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet, necessario per la connessione alle origini dati Excel o Access, non è disponibile in una versione a 64 bit.  
  
## <a name="troubleshoot-errors-without-a-description"></a>Risoluzione dei problemi relativi agli errori senza descrizione  
 Se viene generato un errore di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] senza descrizione, è possibile individuare la descrizione in [Guida di riferimento ai messaggi e agli errori di Integration Services](../integration-services-error-and-message-reference.md) cercando l'errore in base al numero corrispondente. Al momento, nell'elenco non sono incluse informazioni per la risoluzione dei problemi.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Configurazione di un output degli errori in un componente del flusso di dati](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog relativo all'[aggiunta del nome della colonna di errore a un output degli errori](https://go.microsoft.com/fwlink/?LinkId=261546) nel sito dougbert.com.  
  
  
