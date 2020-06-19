---
title: Impostare le proprietà di un pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 917c5af173fa1e7087d47789b17b0845ab426dad
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963371"
---
# <a name="set-package-properties"></a>Impostazione delle proprietà di un pacchetto
  Quando viene creato un pacchetto in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] utilizzando l'interfaccia grafica offerta da [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è possibile impostare le proprietà dell'oggetto pacchetto nella finestra Proprietà.  
  
 In tale finestra **le proprietà** possono essere elencate per categorie o in ordine alfabetico. Per elencare gli elementi della finestra **Proprietà** per categoria, fare clic sull'icona Per categoria.  
  
 Quando si utilizza questa modalità, le proprietà visualizzate nella finestra **Proprietà** vengono raggruppate nelle categorie seguenti:  
  
-   [Checkpoint](#Checkpoints)  
  
-   [Esecuzione](#Execution)  
  
-   [Valore esecuzione forzato](#ForcedExecutionValue)  
  
-   [Identificazione](#Identification)  
  
-   [Varie](#Misc)  
  
-   [Sicurezza](#Security)  
  
-   [Transazioni](#Transactions)  
  
-   [Version](#Version)  
  
 Per informazioni sulle proprietà aggiuntive di un pacchetto che non è possibile impostare nella finestra **Proprietà** , vedere <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>Per impostare le proprietà di un pacchetto nella finestra Proprietà  
  
-   [Impostare le proprietà di un pacchetto](../../2014/integration-services/set-the-properties-of-a-package.md)  
  
## <a name="properties-by-category"></a>Proprietà per categoria  
 Nelle tabelle seguenti vengono elencate le proprietà di un pacchetto in base alla categoria.  
  
###  <a name="checkpoints"></a><a name="Checkpoints"></a> Checkpoint  
 È possibile utilizzare le proprietà in questa categoria per riavviare il pacchetto da un punto problematico nel flusso di controllo, anziché rieseguire il pacchetto dall'inizio del flusso di controllo. Per ulteriori informazioni, vedere [Restart Packages by Using Checkpoints](packages/restart-packages-by-using-checkpoints.md).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`CheckpointFileName`|Nome del file in cui vengono acquisite le informazioni di checkpoint che consentono il riavvio del pacchetto. Se l'esecuzione del pacchetto viene completata correttamente, questo file verrà eliminato.|  
|`CheckpointUsage`|Specifica quando è possibile riavviare il pacchetto. I possibili valori sono `Never`, `IfExists` e `Always`. Il valore predefinito della proprietà è `Never`, che indica che il pacchetto non può essere riavviato. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|`SaveCheckpoints`|Specifica se i checkpoint vengono scritti nel file del checkpoint durante l'esecuzione del pacchetto. Il valore predefinito di questa proprietà è `False`.|  
  
> [!NOTE]  
>  L'opzione `/CheckPointing on` dell'utilità dtexec equivale all'impostazione della proprietà `SaveCheckpoints` del pacchetto su TRUE e della proprietà `CheckpointUsage` su ALWAYS. Per altre informazioni, vedere [dtexec Utility](packages/dtexec-utility.md).  
  
###  <a name="execution"></a><a name="Execution"></a> Esecuzione  
 Le proprietà di questa categoria consentono di configurare il comportamento in fase di esecuzione dell'oggetto di pacchetto.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`DelayValidation`|Indica se la convalida del pacchetto viene posticipata fino all'esecuzione del pacchetto. Il valore predefinito di questa proprietà è `False`.|  
|**Disable**|Indica se il pacchetto è disabilitato. Il valore predefinito di questa proprietà è `False`.|  
|`DisableEventHandlers`|Specifica se i gestori di eventi del pacchetto vengono eseguiti. Il valore predefinito di questa proprietà è `False`.|  
|`FailPackageOnFailure`|Indica se il pacchetto deve essere interrotto in caso di errore in uno dei suoi componenti. L'unico valore valido di questa proprietà è `False`.|  
|`FailParentOnError`|Indica se il contenitore padre deve essere interrotto in caso di errore in uno dei contenitori figli. Il valore predefinito della proprietà è `False`.|  
|`MaxConcurrentExecutables`|Numero di file eseguibili che il pacchetto è in grado di eseguire contemporaneamente. Il valore predefinito di questa proprietà è **-1**, che indica che non esiste alcun limite.|  
|`MaximumErrorCount`|Numero massimo di errori che si possono verificare prima che l'esecuzione del pacchetto venga arrestata. Il valore predefinito di questa proprietà è **1**.|  
|`PackagePriorityClass`|Classe di priorità del thread Win32 del pacchetto. I possibili valori sono `Default`, `AboveNormal`, `Normal`, `BelowNormal` e `Idle`. Il valore predefinito di questa proprietà è `Default`. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="forced-execution-value"></a><a name="ForcedExecutionValue"></a>Valore esecuzione forzata  
 Le proprietà di questa categoria consentono di configurare un valore di esecuzione facoltativo per il pacchetto.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`ForcedExecutionValue`|Se proprietà ForceExecutionValue è impostato su `True` , valore che specifica il valore di esecuzione facoltativo restituito dal pacchetto. Il valore predefinito di questa proprietà è **0**.|  
|`ForcedExecutionValueType`|Il tipo di dati di ForcedExecutionValue. Il valore predefinito di questa proprietà è `Int32`.|  
|`ForceExecutionValue`|Valore booleano che specifica se il valore di esecuzione facoltativo del contenitore deve essere forzato in modo da contenere un valore specifico. Il valore predefinito di questa proprietà è `False`.|  
  
###  <a name="identification"></a><a name="Identification"></a>Identificazione  
 Le proprietà di questa categoria forniscono informazioni quali l'identificatore univoco e il nome del pacchetto.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`CreationDate`|Data di creazione del pacchetto.|  
|`CreatorComputerName`|Nome del computer in cui è stato creato il pacchetto.|  
|`CreatorName`|Nome dell'utente che ha creato il pacchetto.|  
|`Description`|Descrizione delle funzionalità del pacchetto.|  
|`ID`|GUID del pacchetto, assegnato al momento della creazione. Questa proprietà è di sola lettura. Per generare un nuovo valore casuale per la `ID` proprietà, selezionare **\<Generate New ID>** nell'elenco a discesa.|  
|`Name`|Nome del pacchetto.|  
|`PackageType`|Tipo di pacchetto. I possibili valori sono `Default`, `DTSDesigner`, `DTSDesigner100`, `DTSWizard`, `SQLDBMaint` e `SQLReplication`. Il valore predefinito di questa proprietà è `Default`. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="misc"></a><a name="Misc"></a>Varie  
 Le proprietà di questa categoria vengono utilizzate per l'accesso alle configurazioni e alle espressioni utilizzate dal pacchetto e per fornire informazioni sulle impostazioni locali e sulla modalità di registrazione del pacchetto. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`Configurations`|Raccolta delle configurazioni utilizzate dal pacchetto. Per visualizzare e configurare le configurazioni del pacchetto, fare clic sul pulsante Sfoglia **(...)**.|  
|`Expressions`|Per creare espressioni per le proprietà del pacchetto, fare clic sul pulsante Sfoglia **(...)**.<br /><br /> Nota: è possibile creare espressioni di proprietà per tutte le proprietà del pacchetto incluse nel modello a oggetti, non solo le proprietà elencate nella Finestra Proprietà.<br /><br /> Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md).<br /><br /> Per visualizzare le espressioni di proprietà esistenti, espandere `Expressions`. Per modificare e valutare un'espressione, fare clic sul pulsante Sfoglia **(...)** nella casella di testo dell'espressione.|  
|`ForceExecutionResult`|Risultato dell'esecuzione del pacchetto. I valori sono `None`, `Success`, `Failure` e `Completion`. Il valore predefinito di questa proprietà è `None`. Per altre informazioni, vedere T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|`LocaleId`|Impostazioni locali Microsoft Win32. Il valore predefinito di questa proprietà è costituito dalle impostazioni locali del sistema operativo sul computer locale.|  
|`LoggingMode`|Valore che specifica il comportamento di registrazione del pacchetto. I possibili valori sono `Disabled`, `Enabled` e `UseParentSetting`. Il valore predefinito di questa proprietà è `UseParentSetting`. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|`OfflineMode`|Indica se il pacchetto è in modalità offline. Questa proprietà è di sola lettura. e viene impostata a livello di progetto. In genere, Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] tenta di connettersi a ogni origine dei dati utilizzata dal pacchetto per convalidare i metadati associati alle origini e alle destinazioni. È possibile attivare l'opzione **Offline** dal menu **SSIS** anche prima di aprire un pacchetto, per impedire questi tentativi di connessione e gli errori di convalida risultanti quando le origini dei dati non sono disponibili. È anche possibile abilitare l'opzione **Offline** per rendere più veloci le operazioni di progettazione e disabilitarla solo quando si vuole convalidare il pacchetto.|  
|`SuppressConfigurationWarnings`|Indica se gli avvisi generati dalle configurazioni vengono soppressi. Il valore predefinito di questa proprietà è `False`.|  
|`UpdateObjects`|Indica se il pacchetto viene aggiornato in modo da utilizzare le versioni più recenti, se disponibili, degli oggetti che contiene. Se ad esempio la proprietà è impostata su `True`, un pacchetto che include un'attività Inserimento bulk viene aggiornato in modo da utilizzare la versione più recente dell'attività Inserimento bulk disponibile in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Il valore predefinito di questa proprietà è `False`.|  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Le proprietà di questa categoria consentono di impostare il livello di protezione del pacchetto. Per altre informazioni, vedere [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`PackagePassword`|Password per i livelli di protezione del pacchetto ( `EncryptSensitiveWithPassword` e `EncryptAllWithPassword` ) che richiedono le password.|  
|`ProtectionLevel`|Livello di protezione del pacchetto. I valori sono `DontSaveSensitive` , `EncryptSensitiveWithUserKey` , `EncryptSensitiveWithPassword` , `EncryptAllWithPassword` e **ServerStorage**. Il valore predefinito di questa proprietà è `EncryptSensitiveWithUserKey`. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="transactions"></a><a name="Transactions"></a>Transazioni  
 Le proprietà di questa categoria consentono di configurare il livello di isolamento e l'opzione relativa alle transazioni per il pacchetto. Per altre informazioni, vedere [Transazioni di Integration Services](integration-services-transactions.md).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`IsolationLevel`|Livello di isolamento della transazione del pacchetto.  Il valore predefinito di questa proprietà è `Serializable`. I valori validi sono <br />`Unspecified`<br />`Chaos`<br />`ReadUncommitted`<br />`ReadCommitted`<br />`RepeatableRead`<br />`Serializable`<br />`Snapshot`.<br /><br /> La proprietà `IsolationLevel` viene applicata automaticamente alle transazioni del pacchetto solo quando il valore della proprietà `TransactionOption` è `Required`.<br /><br /> Il valore della proprietà `IsolationLevel` richiesta da un contenitore figlio viene ignorato quando le condizioni seguenti sono vere:<br /><br /> Il valore della proprietà `TransactionOption` del contenitore figlio è `Supported`.<br />Il contenitore figlio partecipa alla transazione di un contenitore padre.<br /><br /> Il valore della proprietà `IsolationLevel` richiesta dal contenitore viene rispettato solo quando il contenitore avvia una nuova transazione. Un contenitore avvia una nuova transazione quando le condizioni seguenti sono vere:<br /><br /> Il valore della proprietà `TransactionOption` del contenitore è `Required`.<br />Non è stata ancora avviata alcuna transazione da parte del padre.<br /><br /> <br /><br /> Nota: il valore `Snapshot` della proprietà `IsolationLevel` non è compatibile con le transazioni del pacchetto, quindi non è possibile utilizzare la proprietà `IsolationLevel` per impostare il livello di isolamento delle transazioni del pacchetto su `Shapshot`. È necessario invece eseguire una query SQL per impostare le transazioni del pacchetto su `Snapshot`. Per altre informazioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).<br /><br /> Per ulteriori informazioni sulla proprietà `IsolationLevel`, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|`TransactionOption`|Supporto delle transazioni da parte del pacchetto. I possibili valori sono `NotSupported`, `Supported` e `Required`. Il valore predefinito di questa proprietà è `Supported`. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="version"></a><a name="Version"></a>Versione  
 Le proprietà di questa categoria forniscono informazioni sulla versione dell'oggetto di pacchetto.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`VersionBuild`|Numero di build del pacchetto.|  
|`VersionComments`|Commenti sulla versione del pacchetto.|  
|`VersionGUID`|GUID della versione del pacchetto. Questa proprietà è di sola lettura.|  
|`VersionMajor`|Versione principale più recente del pacchetto.|  
|`VersionMinor`|Versione secondaria più recente del pacchetto.|  
  
  
