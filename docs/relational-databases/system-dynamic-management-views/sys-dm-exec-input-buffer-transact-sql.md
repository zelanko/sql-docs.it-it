---
title: sys.dm_exec_input_buffer (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8531f33f2d027eba14d4416e9138560b25ead20e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013123"
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (Transact-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sulle istruzioni inviate a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>Argomenti  
*session_id*  
L'id di sessione è in esecuzione batch per essere cercato. *session_id* viene **smallint**. *session_id* può essere ottenuto dagli oggetti a gestione dinamica seguenti:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
L'elemento request_id dal [exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md). *request_id* viene **int**.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|Il tipo di evento nel buffer di input per il valore spid specificato.|  
|**parameters**|**smallint**|Tutti i parametri forniti per l'istruzione.|  
|**event_info**|**nvarchar(max)**|Il testo dell'istruzione nel buffer di input per il valore spid specificato.|  
  
## <a name="permissions"></a>Permissions  
 Sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se l'utente dispone dell'autorizzazione VIEW SERVER STATE, l'utente visualizzerà le sessioni in esecuzione tutte nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; in caso contrario, l'utente verrà visualizzato solo nella sessione corrente.  
  
 Sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se l'utente è il proprietario del database, l'utente visualizzerà tutti in esecuzione sessioni nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; in caso contrario, l'utente verrà visualizzato solo nella sessione corrente.  
  
## <a name="remarks"></a>Note  
 Questa funzione a gestione dinamica può essere utilizzata in combinazione con Sys. dm _ exec_requests o con attraverso la pratica **CROSS APPLY**.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-simple-example"></a>A. Esempio semplice  
 Nell'esempio seguente viene illustrato il passaggio di un id di sessione (SPID) e un id richiesta per la funzione.  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. Tra si applicano alle informazioni aggiuntive  
 L'esempio seguente elenca il buffer di input per le sessioni con id di sessione superiore a 50.  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
