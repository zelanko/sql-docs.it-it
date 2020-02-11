---
title: sys. pdw_materialized_view_column_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 934b1ed84aa7391ad8cf47e463dd38b37408ec00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401659"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql"></a>sys. pdw_materialized_view_column_distribution_properties (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Visualizza le informazioni di distribuzione per le colonne in una vista materializzata.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID dell'oggetto a cui appartiene la colonna. |  
|column_id|**int**|ID della colonna.|  
|distribution_ordinal|**tinyint**|0 = non è una colonna di distribuzione.</br> 1 = SQL Data Warehouse utilizza questa colonna per distribuire la vista materializzata.|
 
## <a name="permissions"></a>Autorizzazioni 

È richiesta l'autorizzazione VIEW DATABASE STATE.

## <a name="see-also"></a>Vedere anche

[Ottimizzazione delle prestazioni con vista materializzata](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[Crea vista MATERIALIZZAta come SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[MODIFICARE la vista MATERIALIZZAta &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[SPIEGA &#40;&#41;Transact-SQL](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys. pdw_materialized_view_distribution_properties &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys. pdw_materialized_view_mappings &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;&#41;Transact-SQL](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse e Parallel data warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Visualizzazioni di sistema supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Istruzioni T-SQL supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
