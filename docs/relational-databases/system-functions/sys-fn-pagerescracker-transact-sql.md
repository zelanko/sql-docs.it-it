---
title: sys.fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Documentazione per la funzione di sistema sys.fn_PageResCracker.
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 2fc7136b60dba47813b9942316ee6fdfbc64f307
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58899707"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Restituisce il `db_id`, `file_id`, e `page_id` per il dato `page_resource` valore. 
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argomenti  
*page_resource*    
È il formato esadecimale a 8 byte di una risorsa di pagina del database.
  
## <a name="tables-returned"></a>Tabelle restituite  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|db_id|**int**|ID database|  
|file_id|**int**|ID file|  
|page_id|**int**|ID pagina|  
  
## <a name="remarks"></a>Note  
`sys.fn_PageResCracker` Consente di convertire la rappresentazione esadecimale a 8 byte di una pagina del database in un set di righe che contiene l'ID del database, file di ID e l'ID di pagina della pagina.   

È possibile ottenere una risorsa di pagina valida dal `page_resource` della colonna della [exec_requests &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) vista a gestione dinamica o la [Sys. sysprocesses &#40;&#41; ](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) vista di sistema. Se una risorsa di pagina non valido viene utilizzata il valore restituito è NULL.  
L'uso primario di `sys.fn_PageResCracker` consiste nel semplificare i join tra queste visualizzazioni e i [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) funzione a gestione dinamica per ottenere informazioni relative alla pagina, ad esempio il oggetto a cui appartiene.
  
## <a name="permissions"></a>Permissions  
Le esigenze degli utenti `VIEW SERVER STATE` autorizzazione nel server.  
  
## <a name="examples"></a>Esempi  
Il `sys.fn_PageResCracker` funzione può essere utilizzata in combinazione con [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) per risolvere i problemi di pagina correlati attese e blocco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Lo script seguente è riportato un esempio di come è possibile utilizzare queste funzioni per raccogliere informazioni sulla pagina di database per tutte le richieste attive che sono attualmente in attesa di un tipo di risorsa di pagina. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
