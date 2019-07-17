---
title: Sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL) | Microsoft Docs
description: Restituisce lo stato corrente di semafori di risorse usato per limitare l'ottimizzazione delle query simultanee
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf134f630e4112f0cef87b7138b92fc83959e230
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097668"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Restituisce lo stato corrente di semafori di risorse usato per limitare l'ottimizzazione delle query simultanee.

|Colonna|type|Descrizione|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|ID pool di risorse in Resource Governor|  
|**name**|**sysname**|Compilare il nome di attività di controllo (Gateway di Gateway di piccole dimensioni, il Gateway di medie, grandi dimensioni)|
|**max_count**|**int**|Il numero massimo configurato di compilazioni simultanee|
|**active_count**|**int**|Il numero attualmente attivo di consente di compilare in questa attività di controllo|
|**waiter_count**|**int**|Il numero di oggetti waiter in questa attività di controllo|
|**threshold_factor**|**bigint**|Fattore di soglia che definisce la parte di memoria massima utilizzata da ottimizzazione delle query.  Per il gateway di piccole dimensioni, threshold_factor indica l'utilizzo della memoria query optimizer massima in byte per una query prima che sia necessario per ottenere un accesso nel gateway di piccole dimensioni.  Per il gateway di medie e grandi dimensione, threshold_factor viene mostrata la parte della memoria totale del server disponibile per questo controllo. Quando si calcola la soglia di utilizzo di memoria per il controllo viene utilizzato come divisore.|
|**threshold**|**bigint**|Memoria di soglia successiva in byte.  La query è necessario per ottenere un accesso a questo gateway se questa soglia viene raggiunta l'utilizzo della memoria.  "-1" se la query non è richiesto un accesso a questo gateway.|
|**is_active**|**bit**|Indica se la query è necessario passare il controllo corrente o No.|


## <a name="permissions"></a>Permissions  
SQL Server richiede l'autorizzazione VIEW SERVER STATE nel server.

Database SQL di Azure richiede l'autorizzazione VIEW DATABASE STATE nel database.


## <a name="remarks"></a>Note  
SQL Server Usa un approccio di gateway a più livelli per limitare il numero di compilazioni simultanee consentite.  Vengono utilizzati tre gateway, tra cui piccole, medie e grandi. I gateway per evitare l'esaurimento dello spazio complessivo di risorse di memoria dai consumer che richiedono memoria più grande di compilazione.

È in attesa su un risultato di gateway nella compilazione posticipata. Oltre ai ritardi nella compilazione, le richieste limitate avrà un RESOURCE_SEMAPHORE_QUERY_COMPILE associato accumulo di tipo di attesa. Il tipo di attesa RESOURCE_SEMAPHORE_QUERY_COMPILE può indicare che le query usano una grande quantità di memoria per la compilazione e che la memoria è esaurita o in alternativa è disponibile memoria sufficiente disponibile in generale, tuttavia disponibile unità in uno specifico gateway sono state esaurite. L'output del **sys.dm_exec_query_optimizer_memory_gateways** può essere utilizzato per risolvere scenari in cui era presente memoria insufficiente per compilare un piano di esecuzione di query.  

## <a name="examples"></a>Esempi  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>R. Visualizzazione delle statistiche durante i semafori di risorse  
Quali sono le statistiche di ottimizzazione memoria gateway corrente per questa istanza di SQL Server?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Come usare il comando DBCC MEMORYSTATUS per monitorare l'utilizzo di memoria in SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[la compilazione di query di grandi dimensioni è in attesa in RESOURCE_SEMAPHORE_QUERY_COMPILE in SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
