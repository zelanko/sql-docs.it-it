---
title: sys. dm_tran_session_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 148cab2122a907c138a2bd74c5f3403d231e2793
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262674"
---
# <a name="sysdm_tran_session_transactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni di correlazione per le sessioni e le transazioni associate.  
  
> [!NOTE]  
>  Per chiamare questo oggetto [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] da [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]o, usare il nome **sys. dm_pdw_nodes_tran_session_transactions**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_id|**int**|ID della sessione nella quale viene eseguita la transazione.|  
|transaction_id|**bigint**|ID della transazione.|  
|transaction_descriptor|**binario (8)**|Identificatore di transazione utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la comunicazione con il driver client.|  
|enlist_count|**int**|Numero di richieste attive nella sessione della transazione.|  
|is_user_transaction|**bit**|1 = La transazione è stata iniziata da una richiesta utente.<br /><br /> 0 = Transazione di sistema.|  
|is_local|**bit**|1 = Transazione locale.<br /><br /> 0 = Transazione distribuita o transazione di sessione associata integrata.|  
|is_enlisted|**bit**|1 = Transazione distribuita integrata.<br /><br /> 0 = Non è una transazione distribuita integrata.|  
|is_bound|**bit**|1 = La transazione è attiva nella sessione tramite sessioni associate.<br /><br /> 0 = La transazione non è attiva nella sessione tramite sessioni associate.|  
|open_transaction_count||Numero di transazioni aperte per ogni sessione.|  
|pdw_node_id|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   

## <a name="remarks"></a>Osservazioni  
 È possibile che una transazione venga eseguita in più di una sessione tramite sessioni associate e transazioni distribuite. In tali casi, sys.dm_tran_session_transactions visualizzerà più righe per lo stesso transaction_id, una per ogni sessione in cui viene eseguita la transazione.  
  
 Eseguendo più richieste in modalità autocommit e utilizzando MARS (Multiple Active Result Sets), è possibile che vi siano più transazioni attive in una singola sessione. In tali casi, sys.dm_tran_session_transactions visualizzerà più righe per lo stesso transaction_id, una per ogni transazione eseguita nella sessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


