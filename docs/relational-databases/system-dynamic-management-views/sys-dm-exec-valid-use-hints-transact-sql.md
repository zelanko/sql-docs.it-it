---
title: sys. dm_exec_valid_use_hints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c6fcaa491f7d42e255ed329a8e16798437aa2c7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67936796"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys. dm_exec_valid_use_hints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Restituisce i nomi di hint supportati da [hint](../../t-sql/queries/hints-transact-sql-query.md#use_hint) . Elenca un nome di hint per riga.  
  
Usare questa DMV per visualizzare l'elenco di tutti i suggerimenti supportati sotto la notazione USE HINT.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome dell'hint.|

Vedere [hint](../../t-sql/queries/hints-transact-sql-query.md#use_hint) per la query per le descrizioni di ogni hint.

Introdotta [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] in SP1.
  
## <a name="see-also"></a>Vedere anche  
    
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

