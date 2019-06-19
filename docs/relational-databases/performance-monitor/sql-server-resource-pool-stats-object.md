---
title: Oggetto Resource Pool Stats di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 86dcb119efd9c6bb179aae9208f8e8209a5f4671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649487"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server - Oggetto Statistiche del pool di risorse
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'oggetto SQLServer: Statistiche del pool di risorse contiene contatori delle prestazioni che forniscono informazioni sulle statistiche del pool di risorse di Resource Governor.  
  
 Ciascun pool di risorse attivo crea un'istanza dell'oggetto prestazioni SQLServer: Statistiche del pool di risorse con lo stesso nome dell'istanza del pool di risorse di Resource Governor. Nella seguente tabella vengono descritti i contatori supportati in questa istanza.  
  
|Nome contatore|Descrizione|  
|------------------|-----------------|  
|**Quantità di concessioni di memoria attive (KB)**|Quantità totale corrente di memoria concessa, in kilobyte (KB). Queste informazioni sono disponibili anche in [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).| 
|**Conteggio delle concessioni di memoria attive**|Conteggio totale corrente delle concessioni di memoria. Queste informazioni sono disponibili anche in [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**I/O letti da disco (ms)**|Tempo medio in millisecondi, richiesto per un'operazione di lettura dal disco.|  
|**I/O lettura disco media (ms) base**|Solo per uso interno.|
|**I/O scritti su disco (ms)**|Tempo medio in millisecondi, richiesto per un'operazione di scrittura su disco.|  
|**I/O scrittura disco media (ms) base**|Solo per uso interno.|
|**Destinazione di memoria cache (KB)**|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per la cache.|  
|**Destinazione di memoria per la compilazione (KB)**|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per le compilazioni di query.|  
|**% di effetto di controllo CPU**|Effetto di Resource Governor sul pool di risorse. Calcolato come (% di utilizzo CPU) / (% di utilizzo CPU senza Resource Governor.|  
|**% CPU ritardata**|CPU di sistema ritardata per tutte le richieste nell'istanza specificata dell'oggetto prestazione come percentuale del tempo totale di attività.|
|**Base % CPU ritardata**|Solo per uso interno.|
|**% effettiva CPU**|Utilizzo della CPU di sistema da parte di tutte le richieste nell'istanza specificata dell'oggetto prestazione come percentuale del tempo totale di attività.|
|**Base % effettiva CPU**|Solo per uso interno.|
|**% di utilizzo CPU**|Utilizzo di larghezza di banda della CPU da parte di tutte le richieste in tutti i gruppi del carico di lavoro appartenenti al pool. Viene misurato in relazione al computer e normalizzato a tutte le CPU del sistema. Tale valore viene modificato quando si modifica la quantità di CPU disponibile per il processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore non è normalizzato secondo i dati ricevuti dal processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Base % di utilizzo CPU**|Solo per uso interno.|
|**% di destinazione utilizzo CPU**|Valore di destinazione di percentuale di utilizzo della CPU per il pool di risorse in base alle impostazioni di configurazione del pool di risorse e al carico del sistema.|  
|**% CPU violata**|Differenza tra la percentuale di prenotazione della CPU e la percentuale di pianificazione effettiva.|
|**Byte letti da disco/sec**|Numero di byte letti dal disco nell'ultimo secondo.|  
|**I/O limitati letti da disco/sec**|Numero delle operazioni di lettura limitate nell'ultimo secondo.|  
|**I/O letti da disco/sec**|Numero delle operazioni di lettura dal disco nell'ultimo secondo.| 
|**Byte scritti su disco/sec**|Numero di byte scritti su disco nell'ultimo secondo.|  
|**I/O limitati scritti su disco/sec**|Numero delle operazioni di scrittura limitate nell'ultimo secondo.| 
|**I/O scritti su disco/sec**|Numero delle operazioni di scrittura su disco nell'ultimo secondo.|
|**Memoria massima (KB)**|Quantità massima, in kilobyte (KB), di memoria di cui dispone il pool di risorse sulla base delle impostazioni del pool e dello stato del server.| 
|**Timeout concessioni di memoria/sec**|Numero di timeout di concessioni di memoria al secondo.|
|**Concessioni di memoria/sec**|Numero di concessioni di memoria nel pool di risorse al secondo.| 
|**Conteggio concessioni di memoria in sospeso**|Numero di richieste per le concessioni di memoria in sospeso nelle code. Queste informazioni sono disponibili anche in [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).|
|**Destinazione di memoria per l'esecuzione di query (KB)**|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per la concessione di memoria per l'esecuzione di query. Queste informazioni sono disponibili anche in [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**Memoria di destinazione (KB)**|Quantità, in kilobyte (KB), di memoria di destinazione che il pool di risorse tenta di ottenere sulla base delle impostazioni del pool e dello stato del server.|   
|**Memoria utilizzata (KB)**|Quantità di memoria utilizzata, in kilobyte (KB), per il pool di risorse.|  

  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server - Oggetto Statistiche gruppi del carico di lavoro](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
