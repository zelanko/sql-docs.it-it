---
title: sys. dm _pdw_nodes_exec_text_query_plan (Transact-SQL) | Microsoft Docs
description: Vista a gestione dinamica che restituisce lo Showplan in formato testo per un batch TSQL o per un'istruzione specifica nel batch.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 45f26c9569950c2450318abf546a838632e06f20
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145666"
---
# <a name="sysdm_pdw_nodes_exec_text_query_plan--transact-sql"></a>sys. dm _pdw_nodes_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Restituisce il piano Showplan in formato testo per un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] o per un'istruzione specifica nel batch.

## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_ID**|**Int**|ID numerico univoco associato al nodo.|
|**dbid**|**smallint**|ID del database di contesto attivo al momento della compilazione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente a questo piano. Per istruzioni SQL ad hoc e preparate, l'ID del database in cui sono state compilate le istruzioni.<br /><br /> La colonna ammette i valori Null.|  
|**objectid**|**Int**|ID dell'oggetto (ad esempio, stored procedure o funzione definita dall'utente) per il piano della query. Per i batch ad hoc e preparati, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.|  
|**number**|**smallint**|Valore intero della stored procedure numerata. Per i batch ad hoc e preparati, questa colonna è **null**.<br /><br /> La colonna ammette i valori Null.| 
|**crittografati**|**bit**|Indica se la stored procedure corrispondente è crittografata.<br /><br /> 0 = non crittografata<br /><br /> 1 = crittografata<br /><br /> La colonna non ammette i valori Null.|  
|**query_plan**|**ssNoVersion**|Contiene la rappresentazione Showplan della fase di compilazione del piano di esecuzione della query specificato con *plan_handle*. La rappresentazione Showplan è in formato testo. Viene generato un piano per ogni batch contenente ad esempio istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, chiamate di stored procedure e chiamate di funzioni definite dall'utente.<br /><br /> La colonna ammette i valori Null.|  

## <a name="remarks"></a>Remarks  
Si applicano le stesse osservazioni in [sys. dm _exec_text_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql?view=sql-server-ver15) .  

## <a name="permissions"></a>Permissions  
 Richiedere il ruolo del server **sysadmin** o l'autorizzazione `VIEW SERVER STATE` nel server.  
  
## <a name="see-also"></a>Vedere anche  
 [Transact-SQL SQL Data Warehouse e Parallel data warehouse &#40;viste a gestione dinamica&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Passaggi successivi
 Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).