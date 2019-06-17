---
title: sys.fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 0183694382851f023c9f6863848a3e525cc0b7aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945624"
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni catalogo full-text.  
  
> [!NOTE]  
>  Le colonne seguenti verranno rimosse in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **data_space_id**, **file_id**, e **percorso**. Non utilizzare queste colonne in un nuovo progetto di sviluppo e modificare non appena possibile le applicazioni in cui una di tali colonne è utilizzata.  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|ID del catalogo full-text. Valore univoco all'interno dei cataloghi full-text del database.|  
|NAME|**sysname**|Nome del catalogo. Valore univoco all'interno del database.|  
|percorso|**nvarchar(260)**|Nome della directory del catalogo nel file system.|  
|is_default|**bit**|Catalogo full-text predefinito.<br /><br /> True = Predefinito.<br /><br /> False = Non predefinito.|  
|is_accent_sensitivity_on|**bit**|Impostazione del catalogo relativa alla distinzione tra caratteri accentati/non accentati.<br /><br /> True = Distinzione tra caratteri accentati/non accentati supportata.<br /><br /> False = Distinzione tra caratteri accentati/non accentati non supportata.|  
|data_space_id|**int**|Filegroup in cui è stato creato il catalogo.|  
|file_id|**int**|ID del file full-text associato al catalogo.|  
|principal_id|**int**|ID dell'entità di database a cui appartiene il catalogo full-text.|  
|is_importing|**bit**|Indica se il catalogo full-text viene importato:<br /><br /> 1 = Il catalogo viene importato.<br /><br /> 2 = Il catalogo non viene importato.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
