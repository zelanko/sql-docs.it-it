---
title: Sys.dm_exec_distributed_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37fd17f17d8b6aa1a30f48d75258d27f4a45561a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097801"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le richieste attualmente o recentemente active nelle query di PolyBase. Elenca una riga per ogni richiesta o alla query.  
  
 Basato su sessione e un utente può richiedere ID, quindi recuperare le richieste distribuite effettive generate in modo da essere eseguito - tramite sys.dm_exec_distributed_requests. Ad esempio, una query che interessano SQL normali e le tabelle esterne SQL verrà scomposizione in varie istruzioni/richieste eseguite nei nodi di calcolo diversi. Per monitorare i passaggi distribuiti in tutti i nodi di calcolo, si introduce un ID esecuzione 'global' che può essere utilizzato per tenere traccia di tutte le operazioni sui nodi di calcolo associati a una determinata richiesta e un operatore, rispettivamente.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|Chiave per questa visualizzazione. Id numerico univoco associato alla richiesta.|Deve essere univoco tra tutte le richieste nel sistema.|  
|execution_id|**nvarchar(32**|Id numerico univoco associato alla sessione in cui è stata eseguita la query.||  
|status|**nvarchar(32**|Stato corrente della richiesta.|'Pending', 'Authorizing', 'AcquireSystemResources', 'Initializing', 'Plan', 'Parsing', 'AquireResources', 'Running', 'Cancelling', 'Complete', 'Failed', 'Cancelled'.|  
|error_id|**nvarchar(36)**|Id univoco dell'errore associato alla richiesta, se presente.|Se si è verificato alcun errore, impostato su NULL.|  
|start_time|**datetime**|Ora di inizio dell'esecuzione della richiesta.|0 per le richieste in coda. in caso contrario, valido datetime minore o uguale all'ora corrente.|  
|end_time|**datetime**|Ora in cui il motore completato la compilazione della richiesta.|Null per le richieste in coda o attive. in caso contrario, un oggetto datetime valido inferiore o uguale all'ora corrente.|  
|total_elapsed_time|**int**|Tempo trascorso nell'esecuzione poiché è stata avviata la richiesta, in millisecondi.|Compreso tra 0 e la differenza tra start_time ed end_time. Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione verrà generato l'avviso "il valore massimo è stato superato." Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
  
## <a name="see-also"></a>Vedere anche  
 [PolyBase con DMV di risoluzione dei problemi](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
