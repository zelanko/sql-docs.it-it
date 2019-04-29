---
title: sys.fulltext_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a96249e8b1ba5d0fc6ac39fab7cf1f8ac00aba3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007545"
---
# <a name="sysfulltextindexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una riga per indice full-text di un oggetto in formato di tabella.  

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto a cui appartiene l'indice full-text.|  
|**unique_index_id**|**int**|ID dell'indice univoco non full-text corrispondente utilizzato per mettere in relazione l'indice full-text e le righe.|  
|**fulltext_catalog_id**|**int**|ID del catalogo full-text in cui si trova l'indice full-text.|  
|**is_enabled**|**bit**|1 = L'indice full-text è abilitato.|  
|**change_tracking_state**|**char(1)**|Stato del rilevamento delle modifiche.<br /><br /> M = Manuale<br /><br /> A = Automatico<br /><br /> O = Disattivato|  
|**change_tracking_state_desc**|**nvarchar(60)**|Descrizione dello stato del rilevamento delle modifiche.<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|Ultima ricerca per indicizzazione (popolamento) completata dall'indice full-text.|  
|**crawl_type**|**char(1)**|Tipo dell'ultima ricerca per indicizzazione o di quella corrente.<br /><br /> F = Ricerca per indicizzazione completa<br /><br /> I = Ricerca per indicizzazione incrementale basata su timestamp<br /><br /> U = Ricerca per indicizzazione di aggiornamento, in base alle notifiche<br /><br /> P = La ricerca per indicizzazione è stata sospesa|  
|**crawl_type_desc**|**nvarchar(60)**|Descrizione dell'ultima ricerca per indicizzazione o di quella corrente.<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|Inizio dell'ultima ricerca per indicizzazione o di quella corrente.<br /><br /> NULL = Nessuno.|  
|**crawl_end_date**|**datetime**|Fine dell'ultima ricerca per indicizzazione o di quella corrente.<br /><br /> NULL = Nessuno.|  
|**incremental_timestamp**|**binary(8)**|Valore di timestamp utilizzato per la successiva ricerca per indicizzazione incrementale.<br /><br /> NULL = Nessuno.|  
|**stoplist_id**|**int**|ID del [stoplist](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) associato con questo indice full-text.|  
|**data_space_id**|**int**|Filegroup in cui si trova l'indice full-text.|  
|**property_list_id**|**int**|ID dell'elenco delle proprietà di ricerca associato all'indice full-text specifico. NULL indica che non vi è alcun elenco delle proprietà di ricerca associato all'indice full-text. Per ottenere ulteriori informazioni su questo elenco di proprietà di ricerca, usare il [Sys. registered_search_property_lists &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) vista del catalogo.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato un indice full-text nella tabella `HumanResources.JobCandidate` del database di esempio `AdventureWorks2012`. Nell'esempio viene restituito l'ID dell'oggetto della tabella, l'ID dell'elenco delle proprietà di ricerca e l'ID dell'elenco di parole non significative utilizzato dall'indice full-text.  
  
> [!NOTE]  
>  Per l'esempio di codice che crea l'indice full-text, vedere la sezione "Esempi" di [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Creazione e gestione di indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
