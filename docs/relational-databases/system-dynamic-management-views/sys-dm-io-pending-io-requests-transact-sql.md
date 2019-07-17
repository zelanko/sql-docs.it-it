---
title: sys.dm_io_pending_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d199797d9835f7acaea413490a0182af057e4c5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265836"
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni richiesta di I/O in sospeso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_io_pending_io_requests**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|Indirizzo di memoria della richiesta di I/O. Non ammette i valori Null.|  
|**io_type**|**nvarchar(60)**|Tipo di richiesta di I/O in sospeso. Non ammette i valori Null.|  
|**io_pending_ms_ticks**|**bigint**|Solo per uso interno. Non ammette i valori Null.| 
|**io_pending**|**int**|Indica se la richiesta di I/O è in sospeso o è stata completata da Windows. Una richiesta di I/O può essere ancora in sospeso anche quando Windows ha completato la richiesta, ma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non ha ancora eseguito uno scambio di contesto per l'elaborazione della richiesta di I/O e la relativa rimozione dall'elenco. Non ammette i valori Null.|  
|**io_completion_routine_address**|**varbinary(8)**|Funzione interna da chiamare quando la richiesta di I/O viene completata. Ammette i valori Null.|  
|**io_user_data_address**|**varbinary(8)**|Solo per uso interno. Ammette i valori Null.|  
|**scheduler_address**|**varbinary(8)**|Utilità di pianificazione sulla quale è stata eseguita la richiesta di I/O. La richiesta di I/O verrà visualizzata nell'elenco delle richieste di I/O in sospeso dell'utilità di pianificazione. Per altre informazioni, vedere [DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). Non ammette i valori Null.|  
|**io_handle**|**varbinary(8)**|Handle di file utilizzato nella richiesta di I/O. Ammette i valori Null.|  
|**io_offset**|**bigint**|Offset della richiesta di I/O. Non ammette i valori Null.|  
|**io_handle_path**|**nvarchar(256)**| Percorso del file che viene usato nella richiesta dei / o. Ammette i valori Null.|
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="permissions"></a>Permissions  

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I/O funzioni e viste a gestione dinamica relative &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


