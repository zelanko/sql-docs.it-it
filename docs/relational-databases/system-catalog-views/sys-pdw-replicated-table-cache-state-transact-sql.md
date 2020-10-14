---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 19a5132bd78b3cc1cca48be193b34126a9f83c3e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036895"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  Restituisce lo stato della cache associata a una tabella replicata mediante **object_id**.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID oggetto per la tabella. Vedere [sys. objects &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **object_id** è la chiave per questa visualizzazione.||  
|state|**nvarchar(40)**|Stato della cache della tabella replicata per questa tabella.|' Nobattistraday ',' Ready '|  
  
## <a name="example"></a>Esempio
Questo esempio unisce sys.pdw_replicated_table_cache_state con sys. Tables per recuperare il nome della tabella e lo stato della cache della tabella replicata.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>Passaggi successivi  
 Per un elenco di tutte le viste del catalogo per analisi sinapsi di Azure e data warehouse parallele, vedere [analisi delle sinapsi di Azure e viste del catalogo data warehouse parallele](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
