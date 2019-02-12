---
title: Sys.dm_os_job_object (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 074981f19f0eb74a7e7c7d4e82466957f0ff98b8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022202"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>Sys.dm_os_job_object (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Restituisce una riga singola che descrive la configurazione dell'oggetto processo che gestisce il processo di SQL Server, nonché determinate statistiche di utilizzo delle risorse a livello di oggetto processo. Restituisce un set vuoto se SQL Server non è in esecuzione in un oggetto processo. 

Un oggetto processo è un costrutto di Windows che implementa la governance delle risorse di CPU, memoria e i/o a livello di sistema operativo. Per altre informazioni sugli oggetti di processo, vedere [gli oggetti processo](/windows/desktop/ProcThread/job-objects). 
  
|Colonne|Tipo di dati|Descrizione|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Specifica la parte di cicli del processore che possono usare i thread di SQL Server durante ogni intervallo di pianificazione. Il valore viene indicato come percentuale di cicli disponibili entro un intervallo di pianificazione del ciclo di 10000. Ad esempio, il valore 100 indica che i thread possono usare core CPU viene loro piena capacità.|
|cpu_affinity_mask|**bigint**|Una maschera di bit che descrive quale processori logici il processo di SQL Server può utilizzare all'interno del gruppo di processori. Ad esempio, cpu_affinity_mask 255 (1111 1111 in formato binario) significa che i primi otto processori logici sono utilizzabile.|
|cpu_affinity_group|**int**|Il numero del gruppo del processore utilizzata da SQL Server.|
|memory_limit_mb|**bigint**|La quantità massima di memoria riservata, in MB, che tutti i processi dell'oggetto processo, tra cui SQL Server, è possono usare in modo cumulativo.| 
|process_memory_limit_mb |**bigint**|La quantità massima di memoria riservata, in MB, che un singolo processo nell'oggetto processo, ad esempio SQL Server, è possibile usare.|
|workingset_limit_mb |**bigint**|La quantità massima di memoria, in MB, che è possibile usare il set di lavoro di SQL Server.|
|non_sos_mem_gap_mb|**bigint**|La quantità di memoria, espressa in MB, riservare per gli stack di thread, le DLL e altre allocazioni di memoria non SOS. Memoria di destinazione SOS è la differenza tra `process_memory_limit_mb` e `non_sos_mem_gap_mb`.| 
|low_mem_signal_threshold_mb|**bigint**|Una soglia di memoria, in MB. Quando la quantità di memoria disponibile per l'oggetto processo è di sotto questa soglia, viene inviato un segnale di notifica di memoria insufficiente per il processo di SQL Server. |
|total_user_time|**bigint**|Numero totale di 100 segni di graduazione ns che hanno trascorso thread all'interno dell'oggetto processo in modalità utente, poiché è stato creato l'oggetto processo. |
|total_kernel_time |**bigint**|Numero totale di 100 segni di graduazione ns che hanno trascorso thread all'interno dell'oggetto processo in modalità kernel, poiché è stato creato l'oggetto processo. |
|write_operation_count |**bigint**|Il numero totale di operazioni i/o su dischi locali emessi da SQL Server poiché è stato creato l'oggetto processo di scrittura. |
|read_operation_count |**bigint**|Numero totale di operazioni dei / o lettura sui dischi locali emessi da SQL Server poiché è stato creato l'oggetto processo. |
|peak_process_memory_used_mb|**bigint**|La quantità massima di memoria, in MB, che un singolo processo nell'oggetto processo, ad esempio SQL Server, è utilizzato poiché è stato creato l'oggetto processo.| 
|peak_job_memory_used_mb|**bigint**|La quantità massima di memoria, in MB, che tutti i processi dell'oggetto processo hanno usato in modo cumulativo poiché l'oggetto processo è stata creata.|
  
## <a name="permissions"></a>Permissions  
In istanza gestita di Database SQL, è necessario `VIEW SERVER STATE` autorizzazione. Nel Database SQL, è necessario il `VIEW DATABASE STATE` autorizzazione nel database.  
 
## <a name="see-also"></a>Vedere anche  

Per informazioni sulle istanze gestite, vedere [istanza gestita di Database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
