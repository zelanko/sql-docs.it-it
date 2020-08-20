---
description: sp_query_store_force_plan (Transact-SQL)
title: sp_query_store_force_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SP_QUERY_STORE_FORCE_PLAN
- SP_QUERY_STORE_FORCE_PLAN
- SYS.SP_QUERY_STORE_FORCE_PLAN_TSQL
- SP_QUERY_STORE_FORCE_PLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_force_plan
- sp_query_store_force_plan
ms.assetid: 0068f258-b998-4e4e-b47b-e375157c8213
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 91ecfae192c0af671961120e4cd2efbf6cac36b0
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646261"
---
# <a name="sp_query_store_force_plan-transact-sql"></a>sp_query_store_force_plan (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Consente di forzare un piano specifico per una query specifica.  
  
 Quando un piano è forzato per una query specifica, ogni volta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che rileva la query, tenta di forzare il piano in Query Optimizer. Se l'utilizzo forzato del piano ha esito negativo, viene generato un evento esteso e viene richiesto a Query Optimizer di ottimizzare in modo normale.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_query_store_force_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @query_id = ] query_id` ID della query. *query_id* è di tipo **bigint**e non prevede alcun valore predefinito.  
  
`[ @plan_id = ] plan_id` ID del piano di query da forzare. *plan_id* è di tipo **bigint**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione **ALTER** per il database.
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sulle query nell'archivio query.  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 Dopo aver identificato il query_id e plan_id che si desidera forzare, utilizzare l'esempio seguente per forzare l'utilizzo di un piano da parte della query.  
  
```sql  
EXEC sp_query_store_force_plan 3, 3;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_remove_query &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [Viste del catalogo di Query Store &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite il Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sp_query_store_reset_exec_stats &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)       
 [Procedure consigliate per l'archivio query](../../relational-databases/performance/best-practice-with-the-query-store.md#CheckForced)    
  
  
