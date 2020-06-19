---
title: Proprietà log | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
author: minewiskan
ms.author: owend
ms.openlocfilehash: af365a21443f3feeb54ce2f76c729ba40909b9df
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940652"
---
# <a name="log-properties"></a>Proprietà dei log
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà dei log server elencate nelle tabelle seguenti. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
## <a name="general"></a>Generale  
 `File`  
 Proprietà stringa che identifica il nome del file di log del server. Questa proprietà viene applicata solo quando viene usato un file su disco per la registrazione invece che una tabella di database (condizione predefinita).  
  
 Il valore predefinito di questa proprietà è msmdsrv.log.  
  
 `FileBufferSize`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MessageLogs`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="error-log"></a>log degli errori  
 È possibile impostare queste proprietà a livello di istanza del server per modificare i valori predefiniti per la configurazione errori visualizzati in altri strumenti e finestre di progettazione. Per ulteriori informazioni [, vedere la pagina relativa alla configurazione degli errori per l'elaborazione di cubi, partizioni e dimensioni &#40;SSAS-&#41;multidimensionali](../multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md) <xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A> .  
  
 **ErrorLog\ErrorLogFileName**  
 Proprietà usata come impostazione predefinita durante operazioni di elaborazione eseguite sul server.  
  
 **ErrorLog\ErrorLogFileSize**  
 Proprietà usata come impostazione predefinita durante operazioni di elaborazione eseguite sul server.  
  
 **ErrorLog\KeyErrorAction**  
 Specifica l'azione eseguita dal server quando si verifica un errore `KeyNotFound`. Le risposte valide a questo errore sono le seguenti:  
  
-   `ConvertToUnknown`: indica al server di allocare il valore della chiave con errore al membro sconosciuto.  
  
-   `DiscardRecord`: indica al server di escludere il record.  
  
 **ErrorLog\KeyErrorLogFile**  
 Si tratta di un nome di file definito dall'utente che deve avere un'estensione di file log ed essere posizionato in una cartella in cui l'account del servizio dispone delle autorizzazioni di lettura-scrittura. Il file di log conterrà solo gli errori generati durante l'elaborazione. Se sono necessarie informazioni più dettagliate, usare utilità Traccia eventi.  
  
 **ErrorLog\KeyErrorLimit**  
 Numero massimo di errori di integrità dei dati che il server consentirà prima di interrompere l'elaborazione. Un valore pari a 1 indica che non vi sono limiti. L'impostazione predefinita è 0, che indica l'arresto dell'elaborazione dopo il primo errore. È inoltre possibile impostare come valore un numero intero.  
  
 **ErrorLog\KeyErrorLimitAction**  
 Specifica l'azione eseguita dal server quando il numero di errori di chiave ha raggiunto il limite superiore. Le risposte valide a questa azione sono le seguenti:  
  
-   `StopProcessing` indica al server di arrestare l'elaborazione quando il limite errori viene raggiunto.  
  
-   `StopLogging` indica al server di arrestare la registrazione degli errori quando il limite errori viene raggiunto, senza interrompere però l'elaborazione.  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 Specifica l'azione eseguita dal server quando si verifica un errore `KeyNotFound`. Le risposte valide a questo errore sono le seguenti:  
  
-   `IgnoreError`: indica al server di continuare l'elaborazione senza registrare l'errore né conteggiarlo ai fini del limite degli errori di chiave. Ignorando l'errore, si consente semplicemente la continuazione dell'elaborazione senza aggiungere l'errore al numero complessivo e senza registrarlo nella schermata o nel file di log. Per il record specifico è presente un problema di integrità dei dati. Di conseguenza, il record non può essere aggiunto al database e verrà rimosso o aggregato al membro sconosciuto, come determinato dalla proprietà `KeyErrorAction`.  
  
-   `ReportAndContinue` indica al server di registrare l'errore, di conteggiarlo per il limite di errori di chiave e di continuare l'elaborazione. Il record che ha attivato l'errore viene rimosso o convertito in membro sconosciuto.  
  
-   `ReportAndStop` indica al server di registrare l'errore e di arrestare immediatamente l'elaborazione, indipendentemente dal limite di errori di chiave. Il record che ha attivato l'errore viene rimosso o convertito in membro sconosciuto.  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 Specifica l'azione eseguita dal server in caso di chiave duplicata. I valori validi includono `IgnoreError` per continuare l'elaborazione come se non si fosse verificato alcun errore, `ReportAndContinue` per registrare l'errore e continuare l'elaborazione e `ReportAndStop` per registrare l'errore e arrestare immediatamente l'elaborazione, anche se il numero di errori è inferiore al limite.  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 Specifica l'azione eseguita dal server quando una chiave Null è stata convertita nel membro sconosciuto. I valori validi includono `IgnoreError` per continuare l'elaborazione come se non si fosse verificato alcun errore, `ReportAndContinue` per registrare l'errore e continuare l'elaborazione e `ReportAndStop` per registrare l'errore e arrestare immediatamente l'elaborazione, anche se il numero di errori è inferiore al limite.  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 Specifica l'azione eseguita dal server quando `NullProcessing` è impostato su `Error` per un attributo della dimensione. Viene generato un errore quando un valore Null non è consentito in un attributo specificato. Questa proprietà di configurazione errori indica il passaggio successivo, ovvero la segnalazione dell'errore e la continuazione dell'elaborazione fino al raggiungimento del limite degli errori. I valori validi includono `IgnoreError` per continuare l'elaborazione come se non si fosse verificato alcun errore, `ReportAndContinue` per registrare l'errore e continuare l'elaborazione e `ReportAndStop` per registrare l'errore e arrestare immediatamente l'elaborazione, anche se il numero di errori è inferiore al limite.  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 Proprietà usata come impostazione predefinita durante operazioni di elaborazione eseguite sul server.  
  
 **ErrorLog\IgnoreDataTruncation**  
 Proprietà usata come impostazione predefinita durante operazioni di elaborazione eseguite sul server.  
  
## <a name="exception"></a>Eccezione  
 **Exception\CreateAndSendCrashReports**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\CrashReportsFolder**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOn**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOff**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MiniDumpFlagsOn**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MinidumpErrorList**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="flight-recorder"></a>Flight Recorder  
 **FlightRecorder\Enabled**  
 Proprietà booleana che indica se la funzionalità Traccia eventi è abilitata.  
  
 **FlightRecorder\FileSizeMB**  
 Proprietà a valore integer a 32 bit con segno che definisce la dimensione in megabyte del file su disco della Traccia eventi.  
  
 **FlightRecorder\LogDurationSec**  
 Proprietà a valore integer a 32 bit con segno che definisce la frequenza in secondi del rollover della Traccia eventi.  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 Proprietà stringa che definisce il nome del file di definizione dello snapshot, contenente comandi di individuazione inviati al server quando viene eseguito uno snapshot.  
  
 Il valore predefinito di questa proprietà è vuoto, al quale per impostazione predefinita viene assegnato il nome di file FlightRecorderSnapshotDef.xml.  
  
 **FlightRecorder\SnapshotFrequencySec**  
 Proprietà a valore integer a 32 bit con segno che definisce la frequenza in secondi dello snapshot.  
  
 **FlightRecorder\TraceDefinitionFile**  
 Proprietà stringa che identifica il nome del file di definizione della traccia eventi.  
  
 Il valore predefinito di questa proprietà è vuoto, al quale per impostazione predefinita viene assegnato il nome di file FlightRecorderTraceDef.xml.  
  
## <a name="query-log"></a>Query Log  
 **Si applica a:** Solo modalità server multidimensionale  
  
 **QueryLog\QueryLogFileName**  
 Proprietà stringa che identifica il nome del file di log delle query. Questa proprietà viene applicata solo quando viene usato un file su disco per la registrazione invece che una tabella di database (condizione predefinita).  
  
 **QueryLog\QueryLogSampling**  
 Proprietà a valore integer a 32 bit con segno che definisce la frequenza di campionamento del log delle query.  
  
 Il valore predefinito di questa proprietà è 10, corrispondente alla registrazione di 1 query di server su 10.  
  
 **QueryLog\QueryLogFileSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **QueryLog\QueryLogConnectionString**  
 Proprietà stringa che identifica la connessione al database del log delle query.  
  
 **QueryLog\QueryLogTableName**  
 Proprietà stringa che identifica il nome della tabella del log delle query.  
  
 Il valore predefinito di questa proprietà è OlapQueryLog.  
  
 **QueryLog\CreateQueryLogTable**  
 Proprietà booleana che indica se creare la tabella del log delle query.  
  
 Il valore predefinito di questa proprietà è False e indica che il server non crea automaticamente la tabella del log e non registra eventi di query.  
  
> [!NOTE]  
>  Per ulteriori informazioni sulla configurazione del log di query, vedere [operazioni di log in Analysis Services](../instances/log-operations-in-analysis-services.md).  
  
## <a name="trace"></a>Trace  
 **Trace\TraceBackgroundDistributionPeriod**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceBackgroundFlushPeriod**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileBufferSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceMaxRowsetSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceProtocolTraffic**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceReportFQDN**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRequestParameters**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà del server in Analysis Services](server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
