---
title: Messaggi personalizzati per la registrazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4601b1f7f73b513eea94de2206f68b5d58053b35
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437858"
---
# <a name="custom-messages-for-logging"></a>Messaggi personalizzati per la registrazione
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sono disponibili numerosi eventi personalizzati per la scrittura di voci di log per i pacchetti e per molte attività. È possibile utilizzare tali voci per salvare informazioni dettagliate su stato di esecuzione, risultati e problemi, tramite la registrazione di eventi predefiniti o messaggi definiti dall'utente da analizzare in un secondo momento. È ad esempio possibile registrare la data e l'ora di inizio e di fine di un'operazione di inserimento bulk per identificare problemi di prestazioni durante l'esecuzione del pacchetto.  
  
 Le voci di log personalizzate costituiscono un set diverso da quello degli eventi di registrazione standard, disponibili per i pacchetti e per tutti i contenitori e le attività. Le voci di log personalizzate vengono create appositamente per acquisire informazioni utili su specifiche attività di un pacchetto. Per l'attività Esegui SQL è ad esempio disponibile una voce di log personalizzata che registra nel log l'istruzione SQL eseguita dall'attività.  
  
 Tutte le voci di log includono informazioni di data e ora, comprese le voci di log scritte automaticamente all'inizio e alla fine dell'esecuzione di un pacchetto. Per molti eventi vengono scritte più voci nel log. Questo avviene in genere per gli eventi che includono varie fasi. Per l'evento `ExecuteSQLExecutingQuery`, ad esempio, vengono scritte tre voci di log: una dopo l'acquisizione di una connessione al database da parte dell'attività, una dopo l'inizio della preparazione dell'istruzione SQL da parte dell'attività e un'altra al termine dell'esecuzione dell'istruzione SQL.  
  
 Sono disponibili voci di log personalizzate per gli oggetti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] seguenti:  
  
 [Pacchetto](#Package)  
  
 [Attività Inserimento bulk](#BulkInsert)  
  
 [Attività Flusso di dati](#DataFlow)  
  
 [Attività Esegui DTS 2000](#ExecuteDTS200)  
  
 [Attività Esegui processo](#ExecuteProcess)  
  
 [Attività Esegui SQL](#ExecuteSQL)  
  
 [Attività File system](#FileSystem)  
  
 [Attività FTP](#FTP)  
  
 [Attività Message Queue](#MessageQueue)  
  
 [Attività Script](#Script)  
  
 [Attività Invia messaggi](#SendMail)  
  
 [Attività Trasferisci database](#TransferDatabase)  
  
 [Attività Trasferisci messaggi di errore](#TransferErrorMessages)  
  
 [Attività Trasferisci processi](#TransferJobs)  
  
 [Attività Trasferisci account di accesso](#TransferLogins)  
  
 [Attività Trasferisci stored procedure master](#TransferMasterStoredProcedures)  
  
 [Attività Trasferisci oggetti di SQL Server](#TransferSQLServerObjects)  
  
 [Attività servizi Web](#WebServices)  
  
 [Attività Lettore di dati WMI](#WMIDataReader)  
  
 [Attività Monitoraggio eventi WMI](#WMIEventWatcher)  
  
 [Attività XML](#XML)  
  
## <a name="log-entries"></a>Voci di log  
  
###  <a name="package"></a><a name="Package"></a>Pacchetto  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per i pacchetti.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`PackageStart`|Indica che l'esecuzione del pacchetto è iniziata.<br /><br /> Nota: questa voce di log viene scritta automaticamente nel log. e non può essere esclusa.|  
|`PackageEnd`|Indica che l'esecuzione del pacchetto è stata completata.<br /><br /> Nota: questa voce di log viene scritta automaticamente nel log. e non può essere esclusa.|  
|`Diagnostic`|Offre informazioni sulla configurazione del sistema che influisce sull'esecuzione dei pacchetti, ad esempio il numero di file eseguibili che è possibile eseguire simultaneamente.<br /><br /> La voce di log `Diagnostic` include anche le voci precedenti e seguenti alle chiamate a provider di dati esterni. Per altre informazioni, vedere [Risoluzione dei problemi relativi alla connettività dei pacchetti degli strumenti](troubleshooting/troubleshooting-tools-for-package-connectivity.md).|  
  
###  <a name="bulk-insert-task"></a><a name="BulkInsert"></a>Attività Inserimento bulk  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Inserimento bulk.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|Indica che l'inserimento bulk è iniziato.|  
|`DTSBulkInsertTaskEnd`|Indica che l'inserimento bulk è terminato.|  
|`DTSBulkInsertTaskInfos`|Offre informazioni descrittive sull'attività.|  
  
###  <a name="data-flow-task"></a><a name="DataFlow"></a>Attività flusso di dati  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Flusso di dati.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`BufferSizeTuning`|Indica che l'attività Flusso di dati ha modificato le dimensioni del buffer. In questa voce di log vengono indicati i motivi della modifica delle dimensioni del buffer e le nuove dimensioni temporanee del buffer.|  
|`OnPipelinePostEndOfRowset`|Indica che a un componente è stato inviato il segnale di fine del set di righe, che viene impostato dall'ultima chiamata al metodo `ProcessInput`. Viene scritta una voce per ogni componente del flusso di dati che elabora dati di input. Tale voce include il nome del componente.|  
|`OnPipelinePostPrimeOutput`|Indica che il componente ha completato l'ultima chiamata al metodo `PrimeOutput`. A seconda del flusso di dati, è possibile che vengano scritte più voci di log. Se il componente è un'origine, indica che tale componente ha terminato l'elaborazione delle righe.|  
|`OnPipelinePreEndOfRowset`|Indica che un componente sta per ricevere il segnale di fine del set di righe, che viene impostato dall'ultima chiamata al metodo `ProcessInput`. Viene scritta una voce per ogni componente del flusso di dati che elabora dati di input. Tale voce include il nome del componente.|  
|`OnPipelinePrePrimeOutput`|Indica che un componente sta per ricevere una chiamata dal metodo `PrimeOutput`. A seconda del flusso di dati, è possibile che vengano scritte più voci di log.|  
|`OnPipelineRowsSent`|Specifica il numero delle righe inviate all'input di un componente da una chiamata al metodo `ProcessInput`. La voce di log include il nome del componente.|  
|`PipelineBufferLeak`|Fornisce informazioni su tutti i componenti che hanno mantenuto attivi i buffer dopo la chiusura di Gestione buffer. Questo significa che le risorse dei buffer non sono state rilasciate e potrebbero verificarsi perdite di memoria. Nella voce di log vengono indicati il nome del componente e l'ID del buffer.|  
|`PipelineExecutionPlan`|Specifica il piano di esecuzione del flusso di dati. Fornisce informazioni sulle modalità di invio dei buffer ai componenti. Insieme alla voce PipelineExecutionTrees, queste informazioni illustrano ciò che avviene nell'ambito dell'attività.|  
|`PipelineExecutionTrees`|Specifica gli alberi di esecuzione del layout nel flusso di dati. L'utilità di pianificazione del motore flusso di dati utilizza tali alberi per compilare il piano di esecuzione del flusso di dati.|  
|`PipelineInitialization`|Fornisce le informazioni di inizializzazione relative all'attività, che includono le directory da utilizzare per l'archiviazione temporanea dei dati BLOB, le dimensioni predefinite del buffer e il numero di righe in un buffer. A seconda della configurazione dell'attività Flusso di dati, è possibile che vengano scritte più voci di log.|  
  
###  <a name="execute-dts-2000-task"></a><a name="ExecuteDTS200"></a> Attività Esegui pacchetto DTS 2000  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Esegui pacchetto DTS 2000.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|Indica che l'attività ha iniziato a eseguire un pacchetto DTS 2000.|  
|`ExecuteDTS80PackageTaskEnd`|Indica che l'attività è terminata.<br /><br /> Nota: l'esecuzione del pacchetto DTS 2000 può continuare anche dopo il termine dell'attività.|  
|`ExecuteDTS80PackageTaskTaskInfo`|Offre informazioni descrittive sull'attività.|  
|`ExecuteDTS80PackageTaskTaskResult`|Restituisce il risultato dell'esecuzione del pacchetto DTS 2000 eseguito dall'attività.|  
  
###  <a name="execute-process-task"></a><a name="ExecuteProcess"></a>Attività Esegui processo  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Esegui processo.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|Fornisce informazioni sul processo di esecuzione del file eseguibile che l'attività dovrà eseguire.<br /><br /> Vengono scritte due voci di log. Una contiene informazioni sul nome e la posizione del file eseguibile eseguito dall'attività, l'altra registra l'uscita dall'eseguibile.|  
|`ExecuteProcessVariableRouting`|Fornisce informazioni sulle variabili indirizzate all'input e agli output del file eseguibile. Vengono scritte voci di log per stdin (l'input), stdout (l'output) e stderr (l'output degli errori).|  
  
###  <a name="execute-sql-task"></a><a name="ExecuteSQL"></a>Attività Esegui SQL  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività Esegui SQL.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|Fornisce informazioni sulle fasi di esecuzione dell'istruzione SQL. Vengono scritte voci di log quando l'attività acquisisce la connessione al database, quando inizia a preparare l'istruzione SQL e al termine dell'esecuzione dell'istruzione SQL. La voce di log per la fase di preparazione include l'istruzione SQL utilizzata dall'attività.|  
  
###  <a name="file-system-task"></a><a name="FileSystem"></a>Attività file System  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività File system.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`FileSystemOperation`|Indica l'operazione eseguita dall'attività. Questa voce di log viene scritta all'inizio dell'operazione sul file system e include informazioni sull'origine e sulla destinazione.|  
  
###  <a name="ftp-task"></a><a name="FTP"></a>Attività FTP  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività FTP.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`FTPConnectingToServer`|Indica che l'attività ha stabilito una connessione al server FTP.|  
|`FTPOperation`|Specifica l'inizio e il tipo dell'operazione FTP eseguita dall'attività.|  
  
###  <a name="message-queue-task"></a><a name="MessageQueue"></a>Attività Message Queue  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Message Queue.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica che l'attività ha terminato l'apertura della coda di messaggi.|  
|`MSMQBeforeOpen`|Indica che l'attività ha iniziato ad aprire la coda di messaggi.|  
|`MSMQBeginReceive`|Indica che l'attività ha iniziato a ricevere un messaggio.|  
|`MSMQBeginSend`|Indica che l'attività ha iniziato a inviare un messaggio.|  
|`MSMQEndReceive`|Indica che l'attività ha terminato la ricezione di un messaggio.|  
|`MSMQEndSend`|Indica che l'attività ha terminato l'invio di un messaggio.|  
|`MSMQTaskInfo`|Offre informazioni descrittive sull'attività.|  
|`MSMQTaskTimeOut`|Indica che si è verificato il timeout dell'attività.|  
  
###  <a name="script-task"></a><a name="Script"></a>Attività script  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività Script.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|Restituisce i risultati dell'implementazione della registrazione nell'ambito dello script. Viene scritta una voce di log per ogni chiamata al metodo `Log` dell'oggetto `Dts`. Tale voce viene scritta al momento dell'esecuzione del codice. Per altre informazioni, vedere [Registrazione nell'attività Script](extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
###  <a name="send-mail-task"></a><a name="SendMail"></a>Attività Invia messaggi  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Invia messaggi.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Indica che l'attività ha iniziato a inviare un messaggio di posta elettronica.|  
|`SendMailTaskEnd`|Indica che l'attività ha terminato l'invio di un messaggio di posta elettronica.|  
|`SendMailTaskInfo`|Offre informazioni descrittive sull'attività.|  
  
###  <a name="transfer-database-task"></a><a name="TransferDatabase"></a>Attività Trasferisci database  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci database.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`SourceDB`|Specifica il database copiato dall'attività.|  
|`SourceSQLServer`|Specifica il computer da cui è stato copiato il database.|  
  
###  <a name="transfer-error-messages-task"></a><a name="TransferErrorMessages"></a>Attività Trasferisci messaggi di errore  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci messaggi di errore.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|Indica che l'attività ha terminato il trasferimento dei messaggi di errore.|  
|`TransferErrorMessagesTaskStartTransferringObjects`|Indica che l'attività ha iniziato a trasferire messaggi di errore.|  
  
###  <a name="transfer-jobs-task"></a><a name="TransferJobs"></a>Attività Trasferisci processi  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci processi.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|Indica che l'attività ha terminato il trasferimento dei processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.|  
|`TransferJobsTaskStartTransferringObjects`|Indica che l'attività ha iniziato a trasferire processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.|  
  
###  <a name="transfer-logins-task"></a><a name="TransferLogins"></a>Attività Trasferisci account di accesso  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci account di accesso.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|Indica che l'attività ha terminato il trasferimento degli account di accesso.|  
|`TransferLoginsTaskStartTransferringObjects`|Indica che l'attività ha iniziato a trasferire account di accesso.|  
  
###  <a name="transfer-master-stored-procedures-task"></a><a name="TransferMasterStoredProcedures"></a>Attività Trasferisci stored procedure master  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci stored procedure master.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|Indica che l'attività ha terminato il trasferimento delle stored procedure definite dall'utente archiviate nel database **master** .|  
|`TransferStoredProceduresTaskStartTransferringObjects`|Indica che l'attività ha iniziato a trasferire le stored procedure definite dall'utente archiviate nel database **master** .|  
  
###  <a name="transfer-sql-server-objects-task"></a><a name="TransferSQLServerObjects"></a>Attività Trasferisci oggetti SQL Server  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|Indica che l'attività ha terminato il trasferimento degli oggetti di database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|Indica che l'attività ha iniziato a trasferire oggetti di database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
  
###  <a name="web-services-task"></a><a name="WebServices"></a> Attività Servizio Web  
 Nella tabella seguente sono elencate le voci di log personalizzate che è possibile abilitare per l'attività Servizio Web.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`WSTaskBegin`|Indica che l'attività ha iniziato ad accedere a un servizio Web.|  
|`WSTaskEnd`|Indica che l'attività ha completato un metodo per il servizio Web.|  
|`WSTaskInfo`|Offre informazioni descrittive sull'attività.|  
  
###  <a name="wmi-data-reader-task"></a><a name="WMIDataReader"></a>Attività lettore di dati WMI  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Lettore di dati WMI.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|Indica che l'attività ha iniziato a leggere dati WMI.|  
|`WMIDataReaderOperation`|Specifica la query WQL eseguita dall'attività.|  
  
###  <a name="wmi-event-watcher-task"></a><a name="WMIEventWatcher"></a>Attività Monitoraggio eventi WMI  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Monitoraggio eventi WMI.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|Indica che l'evento monitorato dall'attività si è verificato.|  
|`WMIEventWatcherTimedout`|Indica che si è verificato il timeout dell'attività.|  
|`WMIEventWatcherWatchingForWMIEvents`|Indica che l'attività ha iniziato a eseguire la query WQL. La voce include la query.|  
  
###  <a name="xml-task"></a><a name="XML"></a>Attività XML  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività XML.  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`XMLOperation`|Fornisce informazioni sull'operazione eseguita dall'attività.|   
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
