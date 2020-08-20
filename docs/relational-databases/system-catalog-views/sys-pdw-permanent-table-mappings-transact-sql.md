---
title: sys. pdw_permanent_table_mappings (Transact-SQL)
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 12261e8e38e75edf7dd596ca2b3499100cfff5ad
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646841"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys. pdw_permanent_table_mappings (Transact-SQL)
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  Associa le tabelle utente permanenti ai nomi degli oggetti interni per **object_id**. Consigliato per ottenere prestazioni migliori rispetto a **sys. pdw_table_mappings**.  
  
> [!NOTE]
> **sys. pdw_permanent_table_mappings** contiene i mapping alle tabelle permanenti e non include i mapping delle tabelle temporanee.

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36)**|Nome fisico della tabella.<br /><br /> **physical_name** e **object_id** formano la chiave per questa visualizzazione.||  
|object_id|**int**|ID oggetto per la tabella. Vedere [sys. objects &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** e **object_id** formano la chiave per questa visualizzazione.||  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_index_mappings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
