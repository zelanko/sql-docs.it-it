---
title: Identificare le attese associate ai gruppi di disponibilità
description: Identificare le attese associate ai gruppi di disponibilità Always On con Transact-SQL (T-SQL) e gli eventi estesi.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
author: rothja
ms.author: jroth
manager: jroth
ms.openlocfilehash: d56681623ab9ad47d2784fdd67d853c7e7102a21
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66789521"
---
# <a name="identify-waits-associated-with-availability-groups"></a>Identificare le attese associate ai gruppi di disponibilità
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nella risoluzione dei problemi di latenza dei gruppi di disponibilità Always On si può monitorare l'accumulo delle statistiche di attesa usando tipi di attesa specifici ai gruppi di disponibilità nella vista a gestione dinamica (DMV) [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
 Per informazioni generali sull'utilizzo delle statistiche di attesa, vedere [SQL Server 2005 Waits and Queues](https://technet.microsoft.com/library/cc966413.aspx) (Attese e code in SQL Server 2005). Il documento è stato scritto per SQL Server 2005, ma le informazioni che contiene sono applicabili anche alle versioni successive di SQL Server.  
  
## <a name="query-for-availability-groups-wait-types"></a>Query per i tipi di attesa dei gruppi di disponibilità  
 Utilizzare la query T-SQL riportata di seguito per recuperare tutte le statistiche di attesa con i tipi di attesa dei gruppi di disponibilità:  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 Per monitorare le statistiche di attesa tramite l'acquisizione di eventi estesi, utilizzare il comando T-SQL seguente.  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 È possibile visualizzare il mapping di chiave-valore del tipo di attesa eseguendo la query seguente:  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Tipi di attese](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  
