---
title: sys. fulltext_catalogs (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 87aac3b3791a46e7522993c6909643a75c196f98
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882143"
---
# <a name="sysfulltext_catalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni catalogo full-text.  
  
> [!NOTE]  
>  Le colonne seguenti verranno rimosse in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **data_space_id**, **file_id**e **path**. Non utilizzare queste colonne in un nuovo progetto di sviluppo e modificare non appena possibile le applicazioni in cui una di tali colonne è utilizzata.  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|ID del catalogo full-text. Valore univoco all'interno dei cataloghi full-text del database.|  
|name|**sysname**|Nome del catalogo. Valore univoco all'interno del database.|  
|path|**nvarchar(260)**|Nome della directory del catalogo nel file system.|  
|is_default|**bit**|Catalogo full-text predefinito.<br /><br /> True = Predefinito.<br /><br /> False = Non predefinito.|  
|is_accent_sensitivity_on|**bit**|Impostazione del catalogo relativa alla distinzione tra caratteri accentati/non accentati.<br /><br /> True = Distinzione tra caratteri accentati/non accentati supportata.<br /><br /> False = Distinzione tra caratteri accentati/non accentati non supportata.|  
|data_space_id|**int**|Filegroup in cui è stato creato il catalogo.|  
|file_id|**int**|ID del file full-text associato al catalogo.|  
|principal_id|**int**|ID dell'entità di database a cui appartiene il catalogo full-text.|  
|is_importing|**bit**|Indica se il catalogo full-text viene importato:<br /><br /> 1 = Il catalogo viene importato.<br /><br /> 2 = Il catalogo non viene importato.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
