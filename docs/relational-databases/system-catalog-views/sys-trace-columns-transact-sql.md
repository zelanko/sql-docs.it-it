---
description: sys.trace_columns (Transact-SQL)
title: sys. trace_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_columns
- trace_columns
- trace_columns_TSQL
- sys.trace_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_columns catalog view
ms.assetid: 5c48eb09-9e9b-45dd-b151-ca39b026ece5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7942f17460b0fb7dbdd111ae4657dd12b3d528ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475238"
---
# <a name="systrace_columns-transact-sql"></a>sys.trace_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La vista del catalogo **sys. trace_columns** contiene un elenco di tutte le colonne dell'evento di traccia. Queste colonne non cambiano per una determinata versione di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Per un elenco completo degli eventi di traccia supportati, vedere [SQL Server riferimento alla classe di evento](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] In alternativa, utilizzare le viste del catalogo di Eventi estesi.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**trace_column_id**|**smallint**|ID univoco della colonna.|  
|**nome**|**nvarchar(128)**|Nome univoco della colonna. Questo parametro non è localizzato.|  
|**type_name**|**nvarchar(128)**|Nome del tipo di dati della colonna.|  
|**max_size**|**int**|Dimensioni massime della colonna, in byte.|  
|**is_filterable**|**bit**|Indica se la colonna può essere utilizzata con i filtri.<br /><br /> 0 = False<br /><br /> 1 = True|  
|**is_repeatable**|**bit**|Indica se è possibile fare riferimento alla colonna nei dati di colonne ripetute.<br /><br /> 0 = False<br /><br /> 1 = True|  
|**is_repeated_base**|**bit**|Indica se la colonna viene utilizzata come chiave univoca per fare riferimento a dati ripetuti.<br /><br /> 0 = False<br /><br /> 1 = True|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. Traces &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_categories &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys. trace_events &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys. trace_event_bindings &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys. trace_subclass_values &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
