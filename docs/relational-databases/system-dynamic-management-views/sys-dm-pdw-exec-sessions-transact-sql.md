---
title: sys.dm_pdw_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fac2105011440cbabd3ed7eedebdaeb5cba37346
ms.sourcegitcommit: 2111068372455b5ec147b19ca6dbf339980b267d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/25/2019
ms.locfileid: "58417173"
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le sessioni attualmente o recentemente aperte nell'appliance. Elenca una riga per ogni sessione.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|Id della query corrente o dell'ultima query eseguita (se la sessione viene terminata e la query è stata in esecuzione al momento della terminazione). Chiave per questa visualizzazione.|Deve essere univoco in tutte le sessioni nel sistema.|  
|status|**nvarchar(10)**|Per le sessioni correnti, indica se la sessione è attualmente attivo o inattivo. Per le sessioni precedenti, la sessione potrebbe mostrare lo stato chiuso o terminato (se la sessione è stata chiusa forzatamente).|'ACTIVE', 'CLOSED', 'IDLE', 'TERMINATE'|  
|request_id|**nvarchar(32)**|L'id della query corrente o ultima esecuzione della query.|Deve essere univoco tra tutte le richieste nel sistema. Null se non è stato eseguito.|  
|security_id|**varbinary(85)**|ID di sicurezza dell'entità che esegue la sessione.||  
|login_name|**nvarchar(128)**|Il nome di accesso dell'entità che esegue la sessione.|Qualsiasi stringa conforme alle convenzioni di denominazione utente.|  
|login_time|**datetime**|Data e ora in cui l'utente connesso e questa sessione è stata creata.|Valido **datetime** prima dell'ora corrente.|  
|query_count|**int**|Acquisisce il numero di query/richiesteQuesta sessione è stata eseguita dopo la creazione.|Maggiore o uguale a 0.|  
|is_transactional|**bit**|Acquisisce se una sessione è attualmente in una transazione oppure No.|0 per commit automatico, 1 per transazionale.|  
|client_id|**nvarchar(255)**|Consente di acquisire informazioni sul client per la sessione.|Qualsiasi stringa valida.|  
|APP_NAME|**nvarchar(255)**|Consente di acquisire le informazioni sul nome dell'applicazione se lo si desidera impostare come parte del processo di connessione.|Qualsiasi stringa valida.|  
|sql_spid|**int**|Il numero di id dello SPID Desiderato. Uso di `session_id` questa sessione. Usare la `sql_spid` colonna da aggiungere al **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\* Avviso \* \***  questa colonna contiene SPID chiuso.||  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione di metadati nel [limiti di capacità](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) argomento.  
  
## <a name="permissions"></a>Permissions  
 È necessaria l'autorizzazione `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
