---
title: Sys.dm_fts_index_keywords_position_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: feaf2a222df364a41e51969a2c95a978f2d0a289
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900959"
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>sys.dm_fts_index_keywords_position_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulla posizione di parola chiave in documenti indicizzati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argomenti  
 db_id('*database_name*')  
 Una chiamata per il [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) (funzione). Questa funzione accetta un nome di database e restituisce l'ID del database, quali sys.dm_fts_index_keywords_position_by_document Usa per individuare il database specificato.  
  
 object_id('*table_name*')  
 Una chiamata per il [object_id ()](../../t-sql/functions/object-id-transact-sql.md) (funzione). Tale funzione accetta un nome di tabella e restituisce l'ID della tabella che contiene l'indice full-text da controllare.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|keyword|**varbinary(128)**|Stringa binaria che rappresenta la parola chiave.|  
|display_term|**nvarchar(4000)**|Formato leggibile della parola chiave derivato dal formato interno archiviato nell'indice full-text.|  
|column_id|**int**|ID della colonna utilizzata per eseguire l'indicizzazione full-text della parola chiave corrente.|  
|document_id|**bigint**|ID della riga o del documento utilizzato per eseguire l'indicizzazione full-text del termine corrente. L'ID corrisponde al valore della chiave full-text della riga o del documento specificato.|  
|position|**int**|La posizione della parola chiave del documento.|  
  
## <a name="remarks"></a>Note  
 Utilizzare DMV per identificare la posizione delle parole indicizzate nei documenti indicizzati. Questa DMV può essere utilizzata per risolvere un problema quando **DM fts_index_keywords_by_document** indica parole presenti nell'indice full-text, ma quando si esegue una query utilizzando le parole, non viene restituito il documento.  
  
## <a name="permissions"></a>Permissions  
 Sono necessarie l'autorizzazione SELECT per le colonne analizzate dall'indice full-text e le autorizzazioni CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite parole chiave dall'indice full-text del `Production.Document` tabella del `AdventureWorks` database di esempio.  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 È possibile aggiungere un predicato di altri columns_id come nella query di esempio seguente, per isolare ulteriormente le posizioni.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)   
 [Migliorare le prestazioni degli indici Full-Text](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [Funzioni di ricerca semantica e ricerca full-Text &#40;Transact-SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Funzioni e viste a gestione dinamica la ricerca semantica e ricerca full-Text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Ricerca full-Text e semantica Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
