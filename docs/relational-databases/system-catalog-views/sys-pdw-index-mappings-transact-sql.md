---
description: sys. pdw_index_mappings (Transact-SQL)
title: sys. pdw_index_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e79b15df940c154d20c2bc6a4ab5218717ddabe5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400967"
---
# <a name="syspdw_index_mappings-transact-sql"></a>sys. pdw_index_mappings (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Esegue il mapping degli indici logici al nome fisico usato nei nodi di calcolo, come riflesso da una combinazione univoca di **object_id** della tabella che contiene l'indice e la **index_id** di un particolare indice all'interno della tabella.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID oggetto per la tabella logica in cui esiste questo indice. Vedere [sys. objects &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** e **object_id** formano la chiave per questa visualizzazione.||  
|index_id|**nvarchar(32)**|ID dell'indice. Vedere [sys. indexes &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).||  
|physical_name|**nvarchar (36)**|Nome dell'indice nei database nei nodi di calcolo.<br /><br /> **physical_name** e **object_id** formano la chiave per questa visualizzazione.||  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_table_mappings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys. pdw_database_mappings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
