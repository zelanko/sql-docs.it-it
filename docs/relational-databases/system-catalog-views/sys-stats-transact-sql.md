---
title: Sys. Stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5150dfbccb6998c69151ca4cf02d9fe88a222830
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856009"
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una riga per ogni oggetto statistiche presente per le tabelle, gli indici e le viste indicizzate nel database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ogni indice ha una riga di statistiche con lo stesso nome e ID (**index_id** = **stats_id**), ma non tutte le righe delle statistiche dispone di un indice corrispondente.  
  
 La vista del catalogo [Sys. stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) fornisce informazioni statistiche per ogni colonna nel database. Per altre informazioni sulle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto a cui appartengono le statistiche.|  
|**name**|**sysname**|Nome delle statistiche. Valore univoco all'interno dell'oggetto.|  
|**stats_id**|**int**|ID delle statistiche. Valore univoco all'interno dell'oggetto.<br /><br />Se le statistiche corrispondono a un indice, il *stats_id* valore è identico il *index_id* valore il [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista del catalogo.|  
|**auto_created**|**bit**|Indica se le statistiche sono state create automaticamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = le statistiche non sono state create automaticamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = le statistiche sono state create automaticamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**user_created**|**bit**|Indica se le statistiche sono state create da un utente.<br /><br /> 0 = le statistiche non sono state create da un utente.<br /><br /> 1 = le statistiche sono state create da un utente.|  
|**no_recompute**|**bit**|Indica se le statistiche sono state create con il **NORECOMPUTE** opzione.<br /><br /> 0 = le statistiche non sono state create con il **NORECOMPUTE** opzione.<br /><br /> 1 = le statistiche sono state create con il **NORECOMPUTE** opzione.|  
|**has_filter**|**bit**|0 = le statistiche non dispongono di un filtro e vengono calcolate in tutte le righe.<br /><br /> 1 = le statistiche dispongono di un filtro e vengono calcolate solo in righe che soddisfanno la definizione del filtro.|  
|**filter_definition**|**nvarchar(max)**|Espressione per il subset di righe incluso nelle statistiche filtrate.<br /><br /> NULL = statistiche non filtrate.|  
|**is_temporary**|**bit**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se le statistiche sono temporanee. Le statistiche temporanee supportano database secondari di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] abilitati per l'accesso in sola lettura.<br /><br /> 0 = le statistiche non sono temporanee.<br /><br /> 1 = le statistiche sono temporanee.|  
|**is_incremental**|**bit**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se le statistiche sono create come statistiche incrementali.<br /><br /> 0 = le statistiche non sono incrementali.<br /><br /> 1 = le statistiche sono incrementali.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti vengono restituite tutte le statistiche e colonne delle statistiche per la tabella `HumanResources.Employee`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Statistiche](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
