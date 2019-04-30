---
title: Oggetto Resource Pool Stats di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fdf00d1291180197f66cd6cb23cf27f10659c68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183016"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server - Oggetto Statistiche del pool di risorse
  L'oggetto SQLServer: Statistiche del pool di risorse contiene contatori delle prestazioni che forniscono informazioni sulle statistiche del pool di risorse di Resource Governor.  
  
 Ciascun pool di risorse attivo crea un'istanza dell'oggetto prestazioni SQLServer: Statistiche del pool di risorse con lo stesso nome dell'istanza del pool di risorse di Resource Governor. Nella seguente tabella vengono descritti i contatori supportati in questa istanza.  
  
|Nome contatore|Descrizione|  
|------------------|-----------------|  
|% di utilizzo CPU|Utilizzo di larghezza di banda della CPU da parte di tutte le richieste in tutti i gruppi del carico di lavoro appartenenti al pool. Viene misurato in relazione al computer e normalizzato a tutte le CPU del sistema. Tale valore viene modificato quando si modifica la quantità di CPU disponibile per il processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore non è normalizzato secondo i dati ricevuti dal processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|% di destinazione utilizzo CPU|Valore di destinazione di percentuale di utilizzo della CPU per il pool di risorse in base alle impostazioni di configurazione del pool di risorse e al carico del sistema.|  
|% di effetto di controllo CPU|Effetto di Resource Governor sul pool di risorse. Calcolato come (% di utilizzo CPU) / (% di utilizzo CPU senza Resource Governor.|  
|Destinazione di memoria per la compilazione (KB)|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per le compilazioni di query.|  
|Destinazione di memoria cache (KB)|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per la cache.|  
|Destinazione di memoria per l'esecuzione di query (KB)|Destinazione di memoria di Service Broker corrente, in kilobyte (KB) per la concessione di memoria per l'esecuzione di query. Queste informazioni sono disponibili anche in [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Concessioni di memoria/sec|Numero di concessioni di memoria nel pool di risorse al secondo.|  
|Conteggio delle concessioni di memoria attive|Conteggio totale corrente delle concessioni di memoria. Queste informazioni sono disponibili anche in [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Timeout concessioni di memoria/sec|Numero di timeout di concessioni di memoria al secondo.|  
|Quantità di concessioni di memoria attive (KB)|Quantità totale corrente di memoria concessa, in kilobyte (KB). Queste informazioni sono disponibili anche in [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Conteggio concessioni di memoria in sospeso|Numero di richieste per le concessioni di memoria in sospeso nelle code. Queste informazioni sono disponibili anche in [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Memoria massima (KB)|Quantità massima, in kilobyte (KB), di memoria di cui dispone il pool di risorse sulla base delle impostazioni del pool e dello stato del server.|  
|Memoria utilizzata (KB)|Quantità di memoria utilizzata, in kilobyte (KB), per il pool di risorse.|  
|Memoria di destinazione (KB)|Quantità, in kilobyte (KB), di memoria di destinazione che il pool di risorse tenta di ottenere sulla base delle impostazioni del pool e dello stato del server.|  
|I/O letti da disco/sec|Numero delle operazioni di lettura dal disco nell'ultimo secondo.|  
|I/O limitati letti da disco/sec|Numero delle operazioni di lettura limitate nell'ultimo secondo.|  
|Byte letti da disco/sec|Numero di byte letti dal disco nell'ultimo secondo.|  
|I/O letti da disco (ms)|Tempo medio in millisecondi, richiesto per un'operazione di lettura dal disco.|  
|I/O scritti su disco/sec|Numero delle operazioni di scrittura su disco nell'ultimo secondo.|  
|I/O limitati scritti su disco/sec|Numero delle operazioni di scrittura limitate nell'ultimo secondo.|  
|Byte scritti su disco/sec|Numero di byte scritti su disco nell'ultimo secondo.|  
|I/O scritti su disco (ms)|Tempo medio in millisecondi, richiesto per un'operazione di scrittura su disco.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server - Oggetto Statistiche gruppi del carico di lavoro](sql-server-workload-group-stats-object.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
