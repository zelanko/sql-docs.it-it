---
title: sys. dm_os_job_object (database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2020
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b7674e3e7696d91170f9bf955808923d713479a1
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2020
ms.locfileid: "77147415"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Restituisce una singola riga che descrive la configurazione dell'oggetto processo che gestisce il processo di SQL Server, nonché alcune statistiche sull'utilizzo delle risorse a livello di oggetto processo. Restituisce un set vuoto se SQL Server non è in esecuzione in un oggetto processo.

Un oggetto processo è un costrutto di Windows che implementa la governance delle risorse di CPU, memoria e i/o a livello del sistema operativo. Per ulteriori informazioni sugli oggetti processo, vedere [oggetti processo](/windows/desktop/ProcThread/job-objects).
  
|Colonne|Tipo di dati|Descrizione|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Specifica la parte di cicli del processore che i thread di SQL Server possono usare durante ogni intervallo di pianificazione. Il valore viene segnalato come percentuale dei cicli disponibili all'interno di un intervallo di pianificazione di 10000 cicli. Ad esempio, il valore 100 indica che i thread possono usare i core CPU sono la capacità completa.|
|cpu_affinity_mask|**bigint**|Maschera di bit che descrive i processori logici che il processo di SQL Server può utilizzare all'interno del gruppo di processori. Ad esempio, cpu_affinity_mask 255 (1111 1111 in formato binario) indica che è possibile utilizzare i primi otto processori logici. <br /><br />Questa colonna è disponibile per la compatibilità con le versioni precedenti. Non segnala il gruppo di processori e il valore restituito potrebbe non essere corretto quando un gruppo di processori contiene più di 64 processori logici. Utilizzare la `process_physical_affinity` colonna per determinare invece l'affinità del processore.|
|cpu_affinity_group|**int**|Numero del gruppo di processori utilizzato dal SQL Server.|
|memory_limit_mb|**bigint**|Quantità massima di memoria vincolata, in MB, che tutti i processi nell'oggetto processo, incluso SQL Server, possono utilizzare cumulativamente.| 
|process_memory_limit_mb |**bigint**|Quantità massima di memoria vincolata, in MB, che un singolo processo nell'oggetto processo, ad esempio SQL Server, può utilizzare.|
|workingset_limit_mb |**bigint**|Quantità massima di memoria, in MB, che può essere utilizzata dal SQL Server working set.|
|non_sos_mem_gap_mb|**bigint**|Quantità di memoria, in MB, riservata per gli stack di thread, le dll e altre allocazioni di memoria non SOS. La memoria di destinazione SOS è la `process_memory_limit_mb` differenza `non_sos_mem_gap_mb`tra e.| 
|low_mem_signal_threshold_mb|**bigint**|Una soglia di memoria, in MB. Quando la quantità di memoria disponibile per l'oggetto processo è inferiore a questa soglia, al processo di SQL Server viene inviato un segnale di notifica di memoria insufficiente. |
|total_user_time|**bigint**|Il numero totale di cicli di 100 NS che i thread all'interno dell'oggetto processo hanno impiegato in modalità utente, dal momento della creazione dell'oggetto processo. |
|total_kernel_time |**bigint**|Il numero totale di cicli di 100 NS che i thread all'interno dell'oggetto processo hanno impiegato in modalità kernel, dall'inizio della creazione dell'oggetto processo. |
|write_operation_count |**bigint**|Numero totale di operazioni di i/o di scrittura sui dischi locali emessi da SQL Server dall'oggetto del processo creato. |
|read_operation_count |**bigint**|Numero totale di operazioni di i/o di lettura sui dischi locali emessi da SQL Server dall'oggetto del processo creato. |
|peak_process_memory_used_mb|**bigint**|Quantità massima di memoria, in MB, utilizzata da un singolo processo nell'oggetto processo, ad esempio SQL Server, dopo la creazione dell'oggetto processo.| 
|peak_job_memory_used_mb|**bigint**|Quantità massima di memoria, in MB, che tutti i processi nell'oggetto processo sono stati utilizzati cumulativamente dall'oggetto processo creato.|
|process_physical_affinity|**nvarchar (3072)**|Maschere di bit che descrivono i processori logici che il processo di SQL Server può utilizzare in ogni gruppo di processori. Il valore di questa colonna è costituito da una o più coppie di valori, ciascuna racchiusa tra parentesi graffe. In ogni coppia il primo valore è il numero del gruppo di processori e il secondo valore è la maschera di bit di affinità per il gruppo di processori. Ad esempio, il valore `{{0,a}{1,2}}` indica che la maschera di affinità per il `0` gruppo `a` di`1010` processori è (in formato binario, che indica che vengono utilizzati i processori 2 e 4) e che la `1` maschera `2` di`10` affinità per il gruppo di processori è (in formato binario, che indica che viene utilizzato il processore 2).|
  
## <a name="permissions"></a>Autorizzazioni  
In Istanza gestita di database SQL, è `VIEW SERVER STATE` richiesta l'autorizzazione. Nel database SQL è richiesta l'autorizzazione `VIEW DATABASE STATE` nel database.  
 
## <a name="see-also"></a>Vedere anche  

Per informazioni sulle istanze gestite, vedere [istanza gestita di database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
