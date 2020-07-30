---
title: sys. dm_pdw_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 74cfb2819cd462a2e3cf695cbb0daf92b4dac5a3
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332383"
---
# <a name="sysdm_pdw_exec_connections-transact-sql"></a>sys. dm_pdw_exec_connections (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Restituisce informazioni sulle connessioni stabilite per questa istanza di [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e i dettagli di ogni connessione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Identifica la sessione associata alla connessione Utilizzare `SESSION_ID()` per restituire l'oggetto `session_id` della connessione corrente.|  
|connect_time|**datetime**|Timestamp relativo al momento in cui è stata stabilita la connessione. Non ammette i valori Null.|  
|encrypt_option|**nvarchar(40)**|Indica TRUE (connessione crittografata) o FALSE (la connessione non è enctypred).|  
|auth_scheme|**nvarchar(40)**|Specifica lo schema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Autenticazione di Windows utilizzato con questa connessione. Non ammette i valori Null.|  
|client_id|**varchar(48)**|Indirizzo IP del client che si connette a questo server. Ammette i valori Null.|  
|sql_spid|**int**|ID del processo server della connessione. Utilizzare `@@SPID` per restituire l'oggetto `sql_spid` della connessione corrente. Per la maggior parte degli scopi, usare `session_id` invece.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione **View Server state** per il server.  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
| Da | To | Relazione |
| ---- | -- | ------------ |
|dm_pdw_exec_sessions. session_id|dm_pdw_exec_connections. session_id|Uno-a-uno|  
|dm_pdw_exec_requests. connection_id|dm_pdw_exec_connections. connection_id|Molti-a-uno|  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Query tipica per raccogliere informazioni su una connessione query personalizzata.  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

