---
title: sys. pdw_materialized_view_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 5dca3564e8e2ccc83f0968d42c636112880f6e56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401680"
---
# <a name="syspdw_materialized_view_distribution_properties-transact-sql-preview"></a>sys. pdw_materialized_view_distribution_properties (Transact-SQL) (anteprima)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Visualizza le visualizzazioni materializzate delle informazioni di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------| 
|object_id|**int**|ID della vista materializzata per cui sono state specificate le proprietà.| 
|distribution_policy |**tinyint**|2 = HASH</br>4 = ROUND_ROBIN|  
|distribution_policy_desc |**nvarchar (60)**|HASH, ROUND_ROBIN|  
 
## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione VIEW DATABASE STATE.
 
## <a name="see-also"></a>Vedere anche

[Crea vista MATERIALIZZAta come SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[MODIFICARE la vista MATERIALIZZAta &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[SPIEGA &#40;&#41;Transact-SQL](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys. pdw_materialized_view_mappings &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;&#41;Transact-SQL](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse e Parallel data warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Visualizzazioni di sistema supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Istruzioni T-SQL supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
