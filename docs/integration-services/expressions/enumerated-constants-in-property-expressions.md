---
title: Costanti enumerate in espressioni di proprietà | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c233d75beabca847937f85977acfd0e2230dc7c2
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922777"
---
# <a name="enumerated-constants-in-property-expressions"></a>Costanti enumerate in espressioni di proprietà

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Nelle espressioni di proprietà che includono valori di un elenco di membri di un enumeratore è necessario utilizzare i valori numerici dei membri dell'enumeratore, anziché i relativi nomi descrittivi. In un'espressione che imposta la proprietà **LoggingMode** , ad esempio, è necessario usare il valore numerico 2, anziché il nome descrittivo Disabled.  
  
 In questo argomento vengono elencati solo i valori numerici equivalenti ai nomi descrittivi degli enumeratori i cui membri vengono comunemente utilizzati nelle espressioni di proprietà. Nel modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono inclusi numerosi enumeratori aggiuntivi che è possibile usare durante la programmazione del modello a oggetti per la compilazione di pacchetti a livello di programmazione o per la creazione di elementi di pacchetto con codice personalizzato, quali attività e componenti dei flussi di dati.  
  
 Oltre alle proprietà personalizzate dei pacchetti e degli oggetti di pacchetto, nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è incluso un set di proprietà disponibili per pacchetti, attività e contenitori Ciclo Foreach, Ciclo For e Sequenza. Le proprietà comuni impostate tramite valori di enumeratori, ovvero **ForceExecutionResult**, **LoggingMode**, **IsolationLevel** e **Transaction Option**, sono elencate nella sezione Proprietà comuni.  
  
 Nelle sezioni seguenti vengono fornite informazioni sulle costanti enumerate:  
  
 [Pacchetto](#Package)  
  
 [Enumeratori per il ciclo Foreach](#Foreach)  
  
 [Attività](#Tasks)  
  
 [Attività Piano di manutenzione](#MaintenancePlanTasks)  
  
 [Proprietà comuni](#CommonProperties)  
  
##  <a name="package"></a><a name="Package"></a> Pacchetto  
 Nelle tabelle seguenti vengono elencati i nomi descrittivi e i valori numerici equivalenti per le proprietà dei pacchetti che è possibile impostare utilizzando i valori di un enumeratore.  
  
 Proprietà **PackageType**: impostata usando i valori dell'enumerazione **DTSPackageType**.  
  
|Nome descrittivo in DTSPackageType|Valore numerico|  
|-------------------------------------|-------------------|  
|Predefinito|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 Proprietà **CheckpointUsage**: impostata usando i valori dell'enumerazione **DTSCheckpointUsage**.  
  
|Nome descrittivo in DTSCheckpointUsage|Valore numerico|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Sempre|2|  
  
 Proprietà **PackagePriorityClass**: impostata usando i valori dell'enumerazione **DTSPriorityClass**.  
  
|Nome descrittivo in DTSPriorityClass|Valore numerico|  
|---------------------------------------|-------------------|  
|Predefinito|0|  
|AboveNormal|1|  
|Normale|2|  
|BelowNormal|3|  
|Idle|4|  
  
 Proprietà **ProtectionLevel**: impostata usando i valori dell'enumerazione **DTSProtectionLevel**.  
  
|Nome descrittivo in DTSProtectionLevel|Valore numerico|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="precedence-constraints"></a><a name="PrecedenceConstraints"></a> Vincoli di precedenza  
 Proprietà **EvalOp**: impostata usando i valori dell'enumerazione **DTSPrecedenceEvalOp**.  
  
|Nome descrittivo in DTSPrecedenceEvalOp|Valore numerico|  
|------------------------------------------|-------------------|  
|Expression|1|  
|Vincolo|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 Proprietà **Value**: impostata usando i valori dell'enumerazione **DTSExecResult**.  
  
|Nome descrittivo|Valore numerico|  
|-------------------|-------------------|  
|Operazione completata|0|  
|Operazioni non riuscite|1|  
|Completion|2|  
|Cancellati|3|  
  
##  <a name="foreach-loop-enumerators"></a><a name="Foreach"></a> Enumeratori per il ciclo Foreach  
 Il ciclo Foreach include un set di enumeratori con proprietà che possono essere impostate tramite espressioni di proprietà.  
  
### <a name="foreach-ado-enumerator"></a>Foreach ADO Enumerator  
 Proprietà **Type**: impostata usando i valori dell'enumerazione **ADOEnumerationType**.  
  
|Nome descrittivo in ADOEnumerationType|Valore numerico|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Enumeratore Foreach Nodelist  
 Proprietà **SourceDocumentType**, **InnerXPathStringSourceType** e **OuterXPathStringSourceType**: impostate usando i valori dell'enumerazione **SourceType**.  
  
|Nome descrittivo in SourceType|Valore numerico|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variabile|1|  
|DirectInput|2|  
  
 Proprietà **EnumerationType**: impostata usando i valori dell'enumerazione **EnumerationType**.  
  
|Nome descrittivo in EnumerationType|Valore numerico|  
|--------------------------------------|-------------------|  
|Strumento di spostamento|0|  
|Nodo|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 Proprietà **InnerElementType**: impostata usando i valori dell'enumerazione **InnerElementType**.  
  
|Nome descrittivo in InnerElementType|Valore numerico|  
|---------------------------------------|-------------------|  
|Strumento di spostamento|0|  
|Nodo|1|  
|NodeText|2|  
  
##  <a name="tasks"></a><a name="Tasks"></a> Attività  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include numerose attività con proprietà che possono essere impostate tramite espressioni di proprietà.  
  
### <a name="analysis-services-execute-ddl-task"></a>Attività Esegui DDL Analysis Services  
 Proprietà **SourceType**: impostata usando i valori dell'enumerazione **DDLSourceType**.  
  
|Nome descrittivo in DDLSourceType|Valore numerico|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variabile|2|  
  
### <a name="bulk-insert-task"></a>Inserimento bulk - attività  
 Proprietà **DataFileType**: impostata usando i valori dell'enumerazione **DTSBulkInsert_DataFileType**.  
  
|Nome descrittivo in DTSBulkInsert_DataFileType|Valore numerico|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>Attività Esegui SQL  
 Proprietà **ResultSetType**: impostata usando i valori dell'enumerazione **ResultSetType**.  
  
|Nome descrittivo in ResultSetType|Valore numerico|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 Proprietà **SqlStatementSourceType**: impostata usando i valori dell'enumerazione **SqlStatementSourceType**.  
  
|Nome descrittivo in SqlStatementSourceType|Valore numerico|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variabile|3|  
  
### <a name="file-system-task"></a>Attività File system  
 Proprietà **Operation**: impostata usando i valori dell'enumerazione **DTSFileSystemOperation**.  
  
|Nome descrittivo in DTSFileSystemOperation|Valore numerico|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 Proprietà **Attributes**: impostata usando i valori dell'enumerazione **DTSFileSystemAttributes**.  
  
|Nome descrittivo in DTSFileSystemAttributes|Valore numerico|  
|----------------------------------------------|-------------------|  
|Normale|0|  
|Archiviazione|1|  
|Nascosto|2|  
|ReadOnly|4|  
|Sistema|8|  
  
### <a name="ftp-task"></a>Attività FTP  
 Proprietà **Operation**: impostata usando i valori dell'enumerazione **DTSFTPOp**.  
  
|Nome descrittivo in DTSFTPOp|Valore numerico|  
|-------------------------------|-------------------|  
|Send|0|  
|Ricevere|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 Proprietà **MessageType**: impostata usando i valori dell'enumerazione **MQMessageType**.  
  
|Nome descrittivo in MQMessageType|Valore numerico|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 Proprietà **StringCompareType**: impostata usando i valori dell'enumerazione **MQStringMessageCompare**.  
  
|Nome descrittivo in MQStringMessageCompare|Valore numerico|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 Proprietà **TaskType**: impostata usando i valori dell'enumerazione **MQType**.  
  
|Nome descrittivo in MQType|Valore numerico|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Invia messaggi - attività  
 Proprietà **MessageSourceType**: impostata usando i valori dell'enumerazione **SendMailMessageSourceType**.  
  
|Nome descrittivo in SendMailMessageSourceType|Valore numerico|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variabile|2|  
  
 Proprietà **Priority**: impostata usando i valori dell'enumerazione **MailPriority**.  
  
|Nome descrittivo in MailPriority|Valore numerico|  
|-----------------------------------|-------------------|  
|Alto|1|  
|Normale|3|  
|Basso|5|  
  
### <a name="transfer-database-task"></a>Attività Trasferisci database  
 Proprietà **Action**: impostata usando i valori dell'enumerazione **TransferAction**.  
  
|Nome descrittivo in TransferAction|Valore numerico|  
|-------------------------------------|-------------------|  
|Copiare|0|  
|Spostamento|1|  
  
 Proprietà **Method**: impostata usando i valori dell'enumerazione **TransferMethod**.  
  
|Nome descrittivo in TransferMethod|Valore numerico|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Attività Trasferisci messaggi di errore  
 Proprietà **IfObjectExists**: impostata usando i valori dell'enumerazione **IfObjectExists**.  
  
|Nome descrittivo in IfObjectExists|Valore numerico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>Attività Trasferisci processi  
 Proprietà **IfObjectExists**: impostata usando i valori dell'enumerazione **IfObjectExists**.  
  
|Nome descrittivo in IfObjectExists|Valore numerico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>Attività Trasferisci account di accesso  
 Proprietà **IfObjectExists**: impostata usando i valori dell'enumerazione **IfObjectExists**.  
  
|Nome descrittivo in IfObjectExists|Valore numerico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 Proprietà **LoginsToTransfer**: impostata usando i valori dell'enumerazione **LoginsToTransfer**.  
  
|Nome descrittivo in LoginsToTransfer|Valore numerico|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Attività Trasferisci stored procedure master  
 Proprietà **IfObjectExists**: impostata usando i valori dell'enumerazione **IfObjectExists**.  
  
|Nome descrittivo in IfObjectExists|Valore numerico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>Attività Trasferisci oggetti di SQL Server  
 Proprietà **ExistingData**: impostata usando i valori dell'enumerazione **ExistingData**.  
  
|Nome descrittivo in ExistingData|Valore numerico|  
|-----------------------------------|-------------------|  
|Replace|0|  
|Accoda|1|  
  
### <a name="web-service-task"></a>Attività Servizio Web  
 Proprietà **OutputType**: impostata usando i valori dell'enumerazione **DTSOutputType**.  
  
|Nome descrittivo in DTSOutputType|Valore numerico|  
|------------------------------------|-------------------|  
|File|0|  
|Variabile|1|  
  
### <a name="wmi-data-reader-task"></a>Attività Lettore di dati WMI  
 Proprietà **OverwriteDestination**: impostata usando i valori dell'enumerazione **OverwriteDestination**.  
  
|Nome descrittivo in OverwriteDestination|Valore numerico|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 Proprietà **OutputType**: impostata usando i valori dell'enumerazione **OutputType**.  
  
|Nome descrittivo in OutputType|Valore numerico|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 Proprietà **DestinationType**: impostata usando i valori dell'enumerazione **DestinationType**.  
  
|Nome descrittivo in DestinationType|Valore numerico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variabile|1|  
  
 Proprietà **WqlQuerySourceType**: impostata usando i valori dell'enumerazione **QuerySourceType**.  
  
|Nome descrittivo in QuerySourceType|Valore numerico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variabile|2|  
  
 Proprietà **ActionAtEvent** di Monitoraggio eventi WMI: impostata usando i valori dell'enumerazione **ActionAtEvent**.  
  
|Nome descrittivo in ActionAtEvent|Valore numerico|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 Proprietà **ActionAtTimeout**: impostata usando i valori dell'enumerazione **ActionAtTimeout**.  
  
|Nome descrittivo in ActionAtTimeout|Valore numerico|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 Proprietà **AfterEvent**: impostata usando i valori dell'enumerazione **AfterEvent**.  
  
|Nome descrittivo in AfterEvent|Valore numerico|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 Proprietà **AfterTimeout**: impostata usando i valori dell'enumerazione **AfterTimeout**.  
  
|Nome descrittivo in AfterTimeout|Valore numerico|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 Proprietà **WqlQuerySourceType**: impostata usando i valori dell'enumerazione **QuerySourceType**.  
  
|Nome descrittivo in QuerySourceType|Valore numerico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variabile|2|  
  
### <a name="xml-task"></a>Attività XML  
 Proprietà **OperationType**: impostata usando i valori dell'enumerazione **DTSXMLOperation**.  
  
|Nome descrittivo in DTSXMLOperation|Valore numerico|  
|--------------------------------------|-------------------|  
|Convalida|0|  
|XSLT|1|  
|XPATH|2|  
|Unione|3|  
|Diff|4|  
|Patch|5|  
  
 Proprietà **SourceType**, **SecondOperandType** e **XPathSourceType**: impostate usando i valori dell'enumerazione **DTSXMLSourceType**.  
  
|Nome descrittivo in DTSXMLSourceType|Valore numerico|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variabile|1|  
|DirectInput|2|  
  
 Proprietà **DestinationType** e **DiffGramDestinationType**: impostate usando i valori dell'enumerazione **DTSXMLSaveResultTo**.  
  
|Nome descrittivo in DTSXMLSaveResultTo|Valore numerico|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variabile|1|  
  
 Proprietà **ValidationType**: impostata usando i valori dell'enumerazione **DTSXMLValidationType**.  
  
|Nome descrittivo in DTSXMLValidationType|Valore numerico|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 Proprietà **XPathOperation**: impostata usando i valori dell'enumerazione **DTSXMLXPathOperation**.  
  
|Nome descrittivo in DTSXMLXPathOperation|Valore numerico|  
|-------------------------------------------|-------------------|  
|Versione di valutazione|0|  
|Valori|1|  
|NodeList|2|  
  
 Proprietà **DiffOptions**: impostata usando i valori dell'enumerazione **DTSXMLDiffOptions**. Le opzioni in questo enumeratore non si escludono a vicenda. Per utilizzare più opzioni, specificare le opzioni desiderate in un elenco delimitato da virgole.  
  
|Nome descrittivo in DTSXMLDiffOptions|Valore numerico|  
|----------------------------------------|-------------------|  
|nessuno|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 Proprietà **DiffAlgorithm**: impostata usando i valori dell'enumerazione **DTSXMLDiffAlgorithm**.  
  
|Nome descrittivo in DTSXMLDiffAlgorithm|Valore numerico|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Veloce|1|  
|Preciso|2|  
  
##  <a name="maintenance-plan-tasks"></a><a name="MaintenancePlanTasks"></a> Attività Piano di manutenzione  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include un set di attività che consentono di eseguire attività di SQL Server da usare in piani di manutenzione e pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta l'uso di queste attività a livello di codice e la documentazione di riferimento per la programmazione non include la documentazione dell'API di tali attività e dei relativi enumeratori.  
  
### <a name="all-maintenance-tasks"></a>Tutte le attività di manutenzione  
 Tutte le attività di manutenzione utilizzano le enumerazioni seguenti per impostare le proprietà specificate.  
  
 Proprietà **DatabaseSelectionType**: impostata usando i valori dell'enumerazione **DatabaseSelection**.  
  
|Nome descrittivo in DatabaseSelection|Valore numerico|  
|----------------------------------------|-------------------|  
|nessuno|0|  
|Tutti|1|  
|Sistema|2|  
|Utente|3|  
|Specifica|4|  
  
 Proprietà **TableSelectionType**: impostata usando i valori dell'enumerazione **TableSelection**.  
  
|Nome descrittivo in TableSelection|Valore numerico|  
|-------------------------------------|-------------------|  
|nessuno|0|  
|Tutti|1|  
|Specifica|2|  
  
 Proprietà **ObjectTypeSelection**: impostata usando i valori dell'enumerazione **ObjectType**.  
  
|Nome descrittivo in ObjectType|Valore numerico|  
|---------------------------------|-------------------|  
|Tabella|0|  
|Visualizza|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Attività Backup database  
 Proprietà **DestinationCreationType**: impostata usando i valori dell'enumerazione **DestinationType**.  
  
|Nome descrittivo in DestinationType|Valore numerico|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manuale|1|  
  
 Proprietà **ExistingBackupsAction**: impostata usando i valori dell'enumerazione **ActionForExistingBackups**.  
  
|Nome descrittivo in ActionForExistingBackups|Valore numerico|  
|-----------------------------------------------|-------------------|  
|Accoda|0|  
|Overwrite|1|  
  
 Proprietà **BackupAction**: impostata usando i valori dell'enumerazione **BackupTaskType**. Questa proprietà viene usata insieme alla proprietà **BackupIsIncremental** per definire il tipo di backup eseguito dall'attività.  
  
|Nome descrittivo in BackupTaskType|Valore numerico|  
|-------------------------------------|-------------------|  
|Database|0|  
|File|1|  
|File di log|2|  
  
 Proprietà **BackupDevice**: impostata usando i valori dell'enumerazione **DeviceType** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
|Nome descrittivo in DeviceType|Valore numerico|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Nastro|1|  
|File|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>Pulizia file manutenzione - attività  
 Proprietà **FileTypeSelected**: impostata usando i valori dell'enumerazione **FileType**.  
  
|Nome descrittivo in FileType|Valore numerico|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 Proprietà **OlderThanTimeUnitType**: impostata usando i valori dell'enumerazione **TimeUnitType**.  
  
|Nome descrittivo in TimeUnitType|Valore numerico|  
|-----------------------------------|-------------------|  
|Giorno|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>Attività Aggiorna statistiche  
 Proprietà **UpdateType**: impostata usando i valori dell'enumerazione **StatisticsTarget** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
|Nome descrittivo in StatisticsTarget|Valore numerico|  
|---------------------------------------|-------------------|  
|Colonna|1|  
|Indice|2|  
|Tutti|3|  
  
##  <a name="common-properties"></a><a name="CommonProperties"></a> Proprietà comuni  
 I pacchetti, le attività e i contenitori Ciclo Foreach, Ciclo For e Sequenza possono utilizzare le enumerazioni seguenti per impostare le proprietà specificate.  
  
 Proprietà **ForceExecutionResult**: impostata usando i valori dell'enumerazione **DTSForcedExecResult**.  
  
|Nome descrittivo in DTSForcedExecResult|Valore numerico|  
|------------------------------------------|-------------------|  
|nessuno|-1|  
|Operazione completata|0|  
|Operazioni non riuscite|1|  
|Completion|2|  
  
 Proprietà **IsolationLevel**: impostata usando i valori dell'enumerazione **IsolationLevel** di .NET Framework. Per altre informazioni, vedere la libreria di classi di Microsoft .NET Framework in [MSDN Library](https://go.microsoft.com/fwlink?LinkId=17313).  
  
 Proprietà **LoggingMode**: impostata usando i valori dell'enumerazione **DTSLoggingMode**.  
  
|Nome descrittivo in DTSLoggingMode|Valore numerico|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|Attivato|1|  
|Disabled|2|  
  
 Proprietà **TransactionOption**: impostata usando i valori dell'enumerazione **DTSTransactionOption**.  
  
|Nome descrittivo in DTSTransactionOption|Valore numerico|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Supportato|1|  
|Obbligatoria|2|  
  
## <a name="related-tasks"></a>Attività correlate  
 [Aggiungere o modificare un'espressione di proprietà](../../integration-services/expressions/add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Pacchetti di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Contenitori in Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Vincoli di precedenza](../../integration-services/control-flow/precedence-constraints.md)  
  
  
