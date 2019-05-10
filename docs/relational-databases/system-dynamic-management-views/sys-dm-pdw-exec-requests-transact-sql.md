---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6e0dac258c03bafb0769e5abb1697be67b1289f2
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105520"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le richieste attualmente o recentemente attivo in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Elenca una riga per ogni richiesta o alla query.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chiave per questa visualizzazione. ID numerico univoco associato alla richiesta.|Deve essere univoco tra tutte le richieste nel sistema.|  
|session_id|**nvarchar(32)**|ID numerico univoco associato alla sessione in cui è stata eseguita la query. See [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Stato corrente della richiesta.|'In esecuzione', 'Sospeso', 'Completed', 'Annullato', "Non riuscito".|  
|submit_time|**datetime**|Ora in cui è stata inviata la richiesta per l'esecuzione.|Valido **datetime** inferiore o uguale a start_time e ora corrente.|  
|start_time|**datetime**|Ora di inizio dell'esecuzione della richiesta.|NULL per le richieste in coda. in caso contrario, validi **datetime** minore o uguale all'ora corrente.|  
|end_compile_time|**datetime**|Ora in cui il motore completato la compilazione della richiesta.|NULL per le richieste che non sono stati compilati ancora; in caso contrario, un valore valido **datetime** minore start_time e minore o uguale all'ora corrente.|
|end_time|**datetime**|Ora in cui l'esecuzione della richiesta completato, non è riuscita o è stata annullata.|Null per le richieste in coda o attive. in caso contrario, un valore valido **datetime** minore o uguale all'ora corrente.|  
|total_elapsed_time|**int**|Tempo trascorso nell'esecuzione poiché è stata avviata la richiesta, in millisecondi.|Compreso tra 0 e la differenza tra start_time ed end_time.</br></br> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione verrà generato l'avviso "il valore massimo è stato superato."</br></br> Il valore massimo in millisecondi è identico 24,8 giorni.|  
|Etichetta|**nvarchar(255)**|Stringa di etichetta facoltativa associata alcune istruzioni di query SELECT.|Qualsiasi stringa che contiene 'a-z', 'A-Z','0-9', '_'.|  
|error_id|**nvarchar(36)**|ID univoco dell'errore associato alla richiesta, se presente.|Visualizzare [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); se si è verificato alcun errore impostato su NULL.|  
|database_id|**int**|Identificatore del database utilizzato dal contesto esplicito (ad esempio, usare DB_X).|Vedere ID nel [Sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|comando|**nvarchar(4000)**|Contiene il testo completo della richiesta di stato inviato dall'utente.|Qualsiasi testo di query o di richiesta valido. Le query che durano più di 4000 byte vengono troncate.|  
|resource_class|**nvarchar(20)**|La classe di risorse per questa richiesta. Vedere correlati **concurrency_slots_used** nelle [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).  Per altre informazioni sulle classi di risorse, vedere [classi & i carico di lavoro di gestione delle risorse](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) |Classi di risorse statiche</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Classi di risorse dinamiche</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|L'importanza di impostare la richiesta è stata inviata. Le richieste con una priorità inferiore rimarrà in coda in stato sospeso, se vengono inviate le richieste di maggiore importanza.  Le richieste con un'importanza superiore verranno eseguite prima delle richieste di importanza inferiore che sono state inviate in precedenza.  Per altre informazioni sull'importanza, vedere [carico di lavoro di importanza](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance).  |NULL</br>Bassa</br>below_normal</br>normale (impostazione predefinita)</br>above_normal</br>Elevata|
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione di metadati nel [limiti di capacità](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) argomento.   
  
## <a name="permissions"></a>Permissions

 È richiesta l'autorizzazione VIEW SERVER STATE.  
  
## <a name="security"></a>Sicurezza

 DM pdw_exec_requests non filtrare i risultati della query in base alle autorizzazioni specifiche del database. Gli account di accesso con autorizzazione VIEW SERVER STATE possono ottenere risultati i risultati della query per tutti i database  
  
>[!WARNING]  
>Un utente malintenzionato può usare DM pdw_exec_requests per recuperare informazioni su oggetti di database specifici, concedendo semplicemente l'autorizzazione VIEW SERVER STATE e in mancanza di un'autorizzazione specifico del database.  
  
## <a name="see-also"></a>Vedere anche

 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
