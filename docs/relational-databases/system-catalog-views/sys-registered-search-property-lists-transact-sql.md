---
title: sys.registered_search_property_lists (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 89636150a5925d3f1d2c77d0462666d369492010
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946498"
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni elenco delle proprietà di ricerca nel database corrente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|ID dell'elenco di proprietà.|  
|**name**|**sysname**|Nome dell'elenco di proprietà.|  
|**create_date**|**datetime**|Data di creazione dell'elenco di proprietà.|  
|**modify_date**|**datetime**|Data dell'ultima modifica apportata all'elenco di proprietà mediante un'istruzione ALTER.|  
|**principal_id**|**int**|Proprietario dell'elenco di proprietà.|  
  
## <a name="remarks"></a>Note  
 Per altre informazioni, vedere [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permissions  
 La visibilità dei metadati negli elenchi delle proprietà di ricerca è limitata a quelle di proprietà dell'utente o per cui è stata concessa qualche autorizzazione REFERENCE.  
  
> [!NOTE]  
>  Il proprietario dell'elenco delle proprietà di ricerca può concedere autorizzazioni REFERENCE o CONTROL per l'elenco. Gli utenti con autorizzazione CONTROL possono inoltre concedere l'autorizzazione REFERENCE ad altri utenti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzati l'ID e il nome degli elenchi delle proprietà di ricerca nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
