---
title: Proprietà OLAP di Analysis Services | Microsoft Docs
ms.date: 03/15/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e2643488710548b3a773730e9b9898125783dc3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714588"
---
# <a name="olap-properties"></a>Proprietà OLAP
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà del server OLAP elencate nelle tabelle seguenti. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Si applica a:** Solo in modalità server multidimensionale  
  
## <a name="memory"></a>Memoria  
 **DefaultPageSizeForData**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForDataHeader**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndex**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndexHeader**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForString**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForHash**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForProp**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 **Abilitata**  
 Proprietà booleana che specifica se l'elaborazione lenta delle aggregazioni è abilitata.  
  
 **SleepIntervalSecs**  
 Proprietà a valore integer a 32 bit con segno che definisce l'intervallo in secondi durante il quale il server controlla se vi sono processi di elaborazione lenta in attesa.  
  
 **MaxCPUUsage**  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce l'utilizzo massimo della CPU (espressa in percentuale) per l'elaborazione lenta. Il server esegue il monitoraggio dell'utilizzo medio della CPU in base agli snapshot. I picchi di utilizzo della CPU superano in genere questa soglia.  
  
 Il valore predefinito di questa proprietà è 0,5, che indica un utilizzo massimo della CPU del 50% per l'elaborazione lenta.  
  
 **MaxObjectsInParallel**  
 Proprietà a valore integer a 32 bit con segno che definisce il numero massimo di partizioni che possono essere sottoposte ad elaborazione lenta in parallelo.  
  
 **MaxRetries**  
 Proprietà a valore integer a 32 bit con segno che definisce il numero di tentativi prima che venga generato un errore se l'elaborazione lenta ha esito negativo.  
  
## <a name="processplan"></a>ProcessPlan  
 **CacheRowsetRows**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CacheRowsetToDisk**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DistinctBuffer**  
 Proprietà a valore integer a 32 bit con segno che definisce la dimensione di un buffer interno utilizzato per il conteggio dei valori distinti. Per rendere più veloce l'elaborazione Distinct Count a scapito della quantità di memoria utilizzata, è necessario aumentare il valore di questa proprietà.  
  
 **EnableRolapDimQueryTableGrouping**  
 Proprietà booleana che specifica se il raggruppamento di tabella è abilitato per dimensioni ROLAP. Se questa proprietà è impostata su True, quando si eseguono query su dimensioni ROLAP in fase di esecuzione, le query vengono eseguite contemporaneamente su intere tabelle di dimensioni ROLAP, anziché separatamente per ogni attributo.  
  
 **EnableTableGrouping**  
 Proprietà booleana che specifica se il raggruppamento di tabella è abilitato. Se questa proprietà è impostata su True, le query vengono eseguite contemporaneamente su intere tabelle di dimensioni ROLAP, anziché separatamente per ogni attributo.  
  
 **ForceMultiPass**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxTableDepth**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustConst**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustFactor**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryLimit**  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce la quantità massima di memoria dedicata all'elaborazione, espressa come percentuale della memoria fisica.  
  
 Il valore predefinito di questa proprietà è 65, corrispondente al 65% della memoria fisica dedicata all'elaborazione di cubi e dimensioni.  
  
 **MemoryLimitErrorEnabled**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **OptimizeSchema**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 **DefaultRefreshInterval**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DimensionLatencyAccuracy**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PartitionLatencyAccuracy**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="process"></a>Process  
 **AggregationMemoryLimitMax**  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce la quantità massima di memoria dedicata all'elaborazione di aggregazioni, espressa come percentuale della memoria fisica.  
  
 Il valore predefinito di questa proprietà è 80, corrispondente all'80% della memoria fisica dedicata all'elaborazione di aggregazioni.  
  
 **AggregationMemoryLimitMin**  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce la quantità minima di memoria dedicata all'elaborazione di aggregazioni, espressa come percentuale della memoria fisica. Per rendere più veloce l'elaborazione delle aggregazioni a scapito della quantità di memoria utilizzata, è necessario aumentare il valore di questa proprietà.  
  
 Il valore predefinito di questa proprietà è 10, che indica che all'elaborazione di aggregazioni verrà dedicata la percentuale minima del 10% della memoria fisica.  
  
 **AggregationNewAlgo**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationPerfLog2**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationsBuildEnabled**  
 Proprietà booleana che specifica se la compilazione di aggregazioni è abilitata. Si tratta di un meccanismo per sottoporre a benchmark la compilazione di aggregazioni senza modificarne la progettazione.  
  
 **BufferMemoryLimit**  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce il limite della memoria buffer di elaborazione, espressa come percentuale della memoria fisica.  
  
 Il valore predefinito di questa proprietà è 60, che indica che per la memoria buffer è possibile utilizzare al massimo il 60% della memoria fisica.  
  
 **BufferRecordLimit**  
 Proprietà a valore integer a 32 bit con segno che definisce il numero di record memorizzabili nel buffer durante l'elaborazione.  
  
 Il valore predefinito di questa proprietà è 1048576 (record).  
  
 **CacheRecordLimit**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CheckDistinctRecordSortOrder**  
 Proprietà booleana che specifica se l'ordinamento dei risultati di una query Distinct Count è significativo durante l'elaborazione di partizioni. Il valore True indica che l'ordinamento non è significativo e deve essere "verificato" dal server. Quando si elaborano partizioni con misura Distinct Count, le query vengono inviate a SQL con la clausola ORDER BY. Per un'elaborazione più veloce, è necessario impostare questa proprietà su False.  
  
 Il valore predefinito di questa proprietà è True, che indica che l'ordinamento non è significativo e deve essere verificato.  
  
 **DatabaseConnectionPoolConnectTimeout**  
 Proprietà a valore integer a 32 bit con segno che definisce il timeout in secondi per l'apertura di una nuova connessione.  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 Proprietà a valore integer a 32 bit con segno che definisce il timeout in secondi per connessioni OLEDB esterne ai database.  
  
 **DatabaseConnectionPoolMax**  
 Proprietà a valore integer a 32 bit con segno che definisce il numero massimo di connessioni in pool ai database.  
  
 Il valore predefinito di questa proprietà è 50 (connessioni).  
  
 **DatabaseConnectionPoolTimeout**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataFileInitEnabled**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataPlacementOptimization**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataSliceInitEnabled**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DeepCompressValue**  
 Proprietà booleana applicabile a misure con tipo di dati Double che specifica se i numeri possono essere compressi a scapito della precisione numerica. Il valore False indica nessuna compressione e nessuna perdita di precisione.  
  
 Il valore predefinito di questa proprietà è True, corrispondente all'abilitazione della compressione a scapito della precisione numerica.  
  
 **DimensionPropertyKeyCache**  
 Proprietà booleana che specifica se le chiavi delle proprietà delle dimensioni vengono memorizzate nella cache. Se le chiavi non sono univoche, è necessario impostare questa proprietà su True.  
  
 **IndexBuildEnabled**  
 Proprietà booleana che specifica se vengono compilati indici durante l'elaborazione. Questa proprietà viene utilizzata per benchmark e raccolta di informazioni.  
  
 **IndexBuildThreshold**  
 Proprietà a valore integer a 32 bit con segno che definisce una soglia per il conteggio delle righe al di sotto della quale non vengono compilati indici per partizioni.  
  
 Il valore predefinito per questa proprietà è 4096 (righe).  
  
 **IndexFileInitEnabled**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MapFormatMask**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RecordsReportGranularity**  
 Proprietà a valore integer a 32 bit che definisce la frequenza (in righe) con cui il server registra eventi di traccia durante l'elaborazione.  
  
 Il valore predefinito di questa proprietà è 1000, corrispondente a un evento di traccia registrato una volta ogni 1000 righe.  
  
 **ROLAPDimensionProcessingEffort**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="query"></a>Query  
 **AggregationsUseEnabled**  
 Proprietà booleana che specifica se le aggregazioni archiviate vengono utilizzate in fase di esecuzione. Questa proprietà consente di disabilitare le aggregazioni senza modificarne la progettazione o rielaborarle. Viene utilizzata per benchmark e raccolta di informazioni.  
  
 Il valore predefinito di questa proprietà è True, corrispondente all'abilitazione delle aggregazioni.  
  
 **AllowSEFiltering**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationCacheRegistryMaxIterations**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationEvaluationPolicy**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ConvertDeletedToUnknown**  
 Proprietà booleana che specifica se i membri di dimensione eliminati vengono convertiti in membri sconosciuti.  
  
 **CopyLinkedDataCacheAndRegistry**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCacheRegistryMaxIterations**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultDrillthroughMaxRows**  
 Proprietà a valore integer a 32 bit con segno che definisce il numero massimo di righe che possono essere restituite da una query drill-through.  
  
 Il valore predefinito di questa proprietà è 10000 (righe).  
  
 **DimensionPropertyCacheSize**  
 Proprietà a valore integer a 32 bit che specifica la quantità di memoria (in byte) utilizzata per memorizzare nella cache membri di dimensione utilizzati in una query.  
  
 Il valore predefinito è 4.000.000 byte (4 MB) per gerarchia dell'attributo, per query attiva. Il valore predefinito rappresenta dimensioni della cache ben bilanciate per le soluzioni con gerarchie tipiche. Tuttavia, le dimensioni con un numero molto elevato di membri, nell'ordine di milioni, o le gerarchie profonde offrono prestazioni migliori se si aumenta questo valore.  
  
 Implicazioni dell'aumento delle dimensioni della cache:  
  
-   I costi di utilizzo della memoria aumentano quando si consente l'utilizzo di una maggiore quantità di memoria per le dimensioni della cache. L'utilizzo effettivo dipende dall'esecuzione della query. Non tutte le query utilizzano la quantità massima consentita.  
  
     Si noti che la memoria usata da tali cache viene considerata non compattabile e sarà inclusa nel conteggio relativo a **TotalMemoryLimit**.  
  
-   Ha effetto su tutti i database del server. **DimensionPropertyCachesize** è una proprietà a livello di server. La modifica di questa proprietà influisce su tutti i database in esecuzione nell'istanza corrente.  
  
Approccio per la stima dei requisiti della cache di dimensione:  
  
1.  Iniziare aumentando di un valore elevato le dimensioni della cache di dimensione per determinare se tale approccio costituisce un vantaggio. È possibile ad esempio raddoppiare il valore predefinito come passaggio iniziale.  
  
2.  Se risulta evidente un miglioramento delle prestazioni, ridurre il valore in modo incrementale fino a raggiungere un equilibrio tra prestazioni e utilizzo della memoria.  


 **ExpressNonEmptyUseEnabled**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IgnoreNullRolapRows**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IndexUseEnabled**  
 Proprietà booleana che specifica se vengono utilizzati indici in fase di esecuzione. Questa proprietà viene utilizzata per benchmark e raccolta di informazioni.  
  
 **MapHandleAlgorithm**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxRolapOrConditions**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
 
 **RowsetSerializationLimit**   
 Si applica ad Azure Analysis Services. Limita il numero di righe restituite in un set di righe al client. Valore predefinito è -1, vale a dire alcun limite viene applicato. Si applica alle query sia DAX e MDX. Può essere utilizzato per proteggere le risorse del server di esportazione di dati su vasta scala. Le query inviate al server che superano il limite vengono annullate e viene restituito un errore.  

 **UseCalculationCacheRegistry**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheFreeLastPageMemory**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistry**  
 Proprietà booleana che specifica se abilitare il registro della cache dei dati, in cui vengono memorizzati i risultati delle query (ma non i risultati calcolati).  
  
 **UseDataCacheRegistryHashTable**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistryMultiplyKey**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataSlice**  
 Proprietà booleana che specifica se utilizzare sezioni di dati di partizioni in fase di esecuzione per ottimizzare le query. Questa proprietà viene utilizzata per benchmark e raccolta di informazioni.  
  
 **UseMaterializedIterators**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseSinglePassForDimSecurityAutoExist**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseVBANet**  
 Proprietà booleana che specifica se utilizzare assembly .NET VBA per funzioni definite dall'utente.  
  
 **CalculationPrefetchLocality\ ApplyIntersect**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\ ApplySubtract**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\ PrefetchLowerGranularities**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel\ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="jobs"></a>processi  
 **ProcessAggregation\ MemoryModel\ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition\ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
