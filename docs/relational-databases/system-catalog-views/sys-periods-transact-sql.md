---
title: sys. periods (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: stevestein
ms.author: sstein
ms.openlocfilehash: eea7709c67eab0dc9fe1890135f9ae03225cdff2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68068088"
---
# <a name="sysperiods-transact-sql"></a>sys. periods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tabella per cui sono stati definiti periodi.  
  
|Intestazione della colonna|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|name|**sysname**|Nome del periodo|  
|period_type|**tinyint**|Valore numerico che rappresenta il tipo di periodo:<br /><br /> 1 = periodo di tempo di sistema|  
|period_type_desc|**nvarchar(60)**|Descrizione testuale del tipo di colonna:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|ID della tabella contenente la colonna period_type|  
|start_column_id|**int**|ID della colonna che definisce il limite del periodo inferiore|  
|end_column_id|**int**|ID della colonna che definisce il limite del periodo superiore|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste del catalogo oggetti &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. all_columns &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys. system_columns &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query sul catalogo di sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)  
  
  
