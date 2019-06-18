---
title: sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa87aa3514af538f55965b00efe8f5965f5c753f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63003497"
---
# <a name="sysdmdbxtpnonclusteredindexstats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  sys.dm_db_xtp_nonclustered_index_stats include statistiche sulle operazioni sugli indici non cluster nelle tabelle ottimizzate per la memoria. sys.dm_db_xtp_nonclustered_index_stats contiene una riga per ogni indice non cluster in una tabella ottimizzata per la memoria nel database corrente.  
  
 Le statistiche riflesse in sys.dm_db_xtp_nonclustered_index_stats vengono raccolte quando la struttura dell'indice in memoria viene creata. Le strutture degli indici in memoria vengono ricreate al riavvio del database.  
  
 Utilizzare sys.dm_db_xtp_nonclustered_index_stats per comprendere e monitorare l'attività dell'indice durante le operazioni DML e quando un database viene portato online. Quando un database con una tabella ottimizzata per la memoria viene riavviato, l'indice viene compilato inserendo una riga per volta in memoria. Il conteggio delle divisioni di pagina, dei merge e del consolidamento può aiutare a capire il lavoro svolto per la compilazione dell'indice quando un database viene portato online. Inoltre, è possibile anche osservare i conteggi prima e dopo una serie di operazioni DML.  
  
 Numerosi tentativi sono indicativi di problemi di concorrenza; contattare il supporto [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Per altre informazioni sugli indici con ottimizzazione per la memoria, non cluster, vedere [panoramica dei meccanismi interni OLTP In memoria SQL Server](https://t.co/T6zToWc6y6), pagina 17.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID dell'oggetto.|  
|xtp_object_id|**bigint**|ID della tabella con ottimizzazione per la memoria.|  
|index_id|**int**|ID dell'indice.|  
|delta_pages|**bigint**|Numero totale di pagine delta per questo indice nell'albero.|  
|internal_pages|**bigint**|Per uso interno. Numero totale di pagine interne per questo indice nell'albero.|  
|leaf_pages|**bigint**|Numero totale di pagine foglia per questo indice nell'albero.|  
|outstanding_retired_nodes|**bigint**|Per uso interno. Numero totale di nodi per questo indice nelle strutture interne.|  
|page_update_count|**bigint**|Numero cumulativo di operazioni di aggiornamento di una pagina nell'indice.|  
|page_update_retry_count|**bigint**|Numero cumulativo di tentativi di un'operazione di aggiornamento di una pagina nell'indice.|  
|page_consolidation_count|**bigint**|Numero cumulativo di consolidamenti di pagine nell'indice.|  
|page_consolidation_retry_count|**bigint**|Numero cumulativo di tentativi di operazioni di consolidamento di pagine.|  
|page_split_count|**bigint**|Numero cumulativo di operazioni di divisione pagina nell'indice.|  
|page_split_retry_count|**bigint**|Numero cumulativo di tentativi di operazioni di divisione pagina.|  
|key_split_count|**bigint**|Numero cumulativo di divisione chiave nell'indice.|  
|key_split_retry_count|**bigint**|Numero cumulativo di tentativi di operazioni di divisione chiave.|  
|page_merge_count|**bigint**|Numero cumulativo di operazioni di unione di pagine nell'indice.|  
|page_merge_retry_count|**bigint**|Numero cumulativo di tentativi di operazioni di unione di pagine.|  
|key_merge_count|**bigint**|Numero cumulativo di operazioni di unione di chiavi nell'indice.|  
|key_merge_retry_count|**bigint**|Numero cumulativo di tentativi di operazioni di unione di chiavi.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il database corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Memoria-con ottimizzazione per la tabella viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
