---
title: Contenitori in Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c147c5fc44f8dcb96679ecc83d3b88fd474830a3
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289857"
---
# <a name="integration-services-containers"></a>Contenitori in Integration Services
  I contenitori sono oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che forniscono la struttura ai pacchetti e i servizi alle attività. Supportano la ripetizione dei flussi di controllo nei pacchetti e consentono di raggruppare attività e contenitori in unità di lavoro significative. Oltre alle attività, i contenitori possono includere anche altri contenitori.  
  
 Nei pacchetti i contenitori vengono utilizzati per gli scopi seguenti:  
  
-   Ripetere determinate attività per ogni elemento di una raccolta, ad esempio i file in una cartella, schemi o oggetti SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects). Un pacchetto può ad esempio eseguire istruzioni Transact-SQL disponibili in più file.  
  
-   Ripetere determinate attività finché un'espressione specificata non restituisce **false**. Un pacchetto può ad esempio inviare un messaggio di posta elettronica diverso per sette volte, ovvero uno per ogni giorno della settimana.  
  
-   Creare gruppi di attività e contenitori che devono avere esito positivo o negativo come singola unità. Un pacchetto può ad esempio raggruppare attività che eliminano e aggiungono righe in una tabella di database e quindi eseguire il commit o il rollback di tutte le attività quando una di queste non riesce.  
  
## <a name="container-types"></a>Tipi di contenitori  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre quattro tipi di contenitori per la compilazione dei pacchetti, elencati nella tabella seguente.  
  
|Contenitore|Descrizione|  
|---------------|-----------------|  
|[Contenitore Ciclo Foreach](../../integration-services/control-flow/foreach-loop-container.md)|Esegue ripetutamente un determinato flusso di controllo utilizzando un enumeratore.|  
|[Contenitore Ciclo For](../../integration-services/control-flow/for-loop-container.md)|Esegue ripetutamente un determinato flusso di controllo verificando una condizione.|  
|[Contenitore Sequenza](../../integration-services/control-flow/sequence-container.md)|Raggruppa attività e contenitori in flussi di controllo che costituiscono subset del flusso di controllo del pacchetto.|  
|[Contenitore Host delle attività](../../integration-services/control-flow/task-host-container.md)|Fornisce servizi a una singola attività.|  
  
 Anche i gestori dell'evento e i pacchetti sono tipi di contenitori. Per altre informazioni, vedere [Pacchetti di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md) e [Gestori eventi di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="summary-of-container-properties"></a>Riepilogo delle proprietà dei contenitori  
 Tutti i tipi di contenitori dispongono di un set di proprietà comune. Se si creano pacchetti usando gli strumenti grafici offerti da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , per i contenitori Ciclo Foreach, Ciclo For e Sequenza vengono elencate nella finestra Proprietà le proprietà seguenti. Le proprietà dei contenitori host delle attività vengono configurate nell'ambito della configurazione dell'attività incapsulata nell'host. Le proprietà degli host delle attività vengono impostate quando si configura l'attività.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**DelayValidation**|Valore booleano che indica se la convalida del contenitore viene posticipata fino alla fase di esecuzione. Il valore predefinito di questa proprietà è **False**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>.|  
|**Descrizione**|Descrizione del contenitore. La proprietà contiene una stringa, ma può essere vuota.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>.|  
|**Disable**|Valore booleano che indica se il contenitore verrà eseguito. Il valore predefinito di questa proprietà è **False**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>.|  
|**DisableEventHandlers**|Valore booleano che indica se i gestori di eventi associati al contenitore verranno eseguiti. Il valore predefinito di questa proprietà è **False**.|  
|**FailPackageOnFailure**|Valore booleano che specifica se il pacchetto deve essere interrotto in caso di errore nel contenitore. Il valore predefinito di questa proprietà è **False**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>.|  
|**FailPackageOnFailure**|Valore booleano che specifica se il contenitore padre deve essere interrotto in caso di errore nel contenitore. Il valore predefinito di questa proprietà è **False**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>.|  
|**ForcedExecutionValue**|Se la proprietà **ForceExecutionValue** è impostata su **True**, rappresenta l'oggetto che contiene il valore di esecuzione facoltativo per il contenitore. Il valore predefinito di questa proprietà è **0**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>.|  
|**ForcedExecutionValueType**|Il tipo di dati **ForcedExecutionValue**. Il valore predefinito di questa proprietà è **Int32**.|  
|**ForceExecutionResult**|Valore che specifica il risultato forzato dell'esecuzione del pacchetto o del contenitore. I valori sono **None**, **Success**, **Failure**e **Completion**. Il valore predefinito di questa proprietà è **None**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>.|  
|**ForceExecutionValue**|Valore booleano che specifica se il valore di esecuzione facoltativo del contenitore deve essere forzato in modo da contenere un valore specifico. Il valore predefinito di questa proprietà è **False**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>.|  
|**ID**|GUID del contenitore, assegnato al momento della creazione del pacchetto. Questa proprietà è di sola lettura.<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>.|  
|**IsolationLevel**|Livello di isolamento della transazione del contenitore. I valori sono **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**e **Snapshot**. Il valore predefinito di questa proprietà è **Serializable**. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|**LocaleID**|Impostazioni locali Microsoft Win32. Il valore predefinito di questa proprietà è costituito dalle impostazioni locali del sistema operativo sul computer locale.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>.|  
|**LoggingMode**|Valore che specifica il comportamento di registrazione del contenitore. I possibili valori sono **Disabled**, **Enabled**e **UseParentSetting**. Il valore predefinito di questa proprietà è **UseParentSetting**. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|**MaximumErrorCount**|Numero massimo di errori che possono verificarsi prima che l'esecuzione del contenitore venga arrestata. Il valore predefinito di questa proprietà è **1**.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>.|  
|**Nome**|Nome del contenitore.<br /><br /> Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>.|  
|**TransactionOption**|Supporto delle transazioni da parte del contenitore. I possibili valori sono **NotSupported**, **Supported**e **Required**. Il valore predefinito di questa proprietà è **Supported**. Per altre informazioni, vedere <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
 Per ulteriori informazioni su tutte le proprietà disponibili per i contenitori Ciclo Foreach, Ciclo For, Sequenza e host delle attività durante la relativa configurazione a livello di codice, vedere gli argomenti relativi alle API di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] seguenti:  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>Oggetti che estendono le funzionalità dei contenitori  
 I contenitori includono flussi di controllo costituiti da eseguibili e vincoli di precedenza. Possono inoltre utilizzare variabili e gestori di eventi. Il contenitore Host attività costituisce un'eccezione perché, dal momento che incapsula una singola attività, non utilizza vincoli di precedenza.  
  
### <a name="executables"></a>Eseguibili  
 Il termine eseguibile si riferisce alle attività a livello di contenitore e a qualsiasi contenitore all'interno del contenitore in considerazione. Un eseguibile può essere costituito da uno dei contenitori e una delle attività disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oppure da un'attività personalizzata. Per altre informazioni, vedere [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md).  
  
### <a name="precedence-constraints"></a>Vincoli di precedenza  
 I vincoli di precedenza collegano in un flusso di controllo ordinato i contenitori e le attività presenti in uno stesso contenitore padre. Per altre informazioni, vedere [Vincoli di precedenza](../../integration-services/control-flow/precedence-constraints.md).  
  
### <a name="event-handlers"></a>Gestori di eventi  
 I gestori di eventi a livello di contenitore rispondono agli eventi generati dal contenitore o dagli altri oggetti inclusi al suo interno. Per altre informazioni, vedere [Gestori eventi di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="variables"></a>Variabili  
 Nelle variabili usate nei contenitori sono incluse le variabili di sistema a livello di contenitore disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e le variabili definite dall'utente usate dal contenitore. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="break-points"></a>Punti di interruzione  
 Quando si imposta un punto di interruzione in un contenitore e la condizione di interruzione è **Interrompi quando il contenitore riceve l'evento OnVariableValueChanged**, definire la variabile nell'ambito del contenitore.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
