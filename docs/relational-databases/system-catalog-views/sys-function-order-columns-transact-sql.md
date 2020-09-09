---
description: sys.function_order_columns (Transact-SQL)
title: sys. function_order_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c7ac555630f4472e5cf58ad9017cdb03643ae2b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546796"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga per ogni colonna che fa parte di un'espressione di **ordinamento** di una funzione con valori di tabella CLR (commmon Language Runtime).  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto (funzione CLR con valori di tabella) nel quale è definito l'ordinamento.|  
|**order_column_id**|**int**|ID della colonna di ordinamento. **order_column_id** è univoco solo all'interno **object_id**.<br /><br /> **order_column_id** rappresenta la posizione di questa colonna nell'ordinamento.|  
|**column_id**|**int**|ID della colonna in **object_id**.<br /><br /> **column_id** è univoco solo all'interno **object_id**.|  
|**is_descending**|**bit**|1 = Direzione di ordinamento decrescente per la colonna di ordinamento.<br /><br /> 0 = Direzione di ordinamento crescente per la colonna di ordinamento.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
