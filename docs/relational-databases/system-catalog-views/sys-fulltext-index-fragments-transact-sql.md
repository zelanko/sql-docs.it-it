---
title: sys.fulltext_index_fragments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 818457ae809b6dec653d6d546fc36b75a27fbf6d
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945556"
---
# <a name="sysfulltextindexfragments-transact-sql"></a>sys.fulltext_index_fragments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Un indice full-text utilizza tabelle interne chiamate *frammenti indice full-text* per memorizzare i dati di indice invertito. Questa vista può essere utilizzata per eseguire una query sui metadati relativi a tali frammenti. Nella vista è contenuta una riga per ogni frammento di indice full-text presente in ogni tabella contenente un indice full-text.  
 
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|table_id|**int**|ID oggetto della tabella che contiene il frammento di indice full-text.|  
|fragment_object_id|**int**|ID oggetto della tabella interna associata al frammento.|  
|fragment_id|**int**|ID logico del frammento di indice full-text. L'ID è univoco per tutti i frammenti della tabella.|  
|TIMESTAMP|**timestamp**|Timestamp associato alla creazione del frammento. I timestamp dei frammenti più recenti sono più grandi dei timestamp di frammenti più vecchi.|  
|data_size|**int**|Dimensione logica del frammento, espressa in byte.|  
|row_count|**int**|Numero di righe singole nel frammento.|  
|status|**int**|Stato del frammento. I valori possibili sono:<br /><br /> 0 = Appena creato e non ancora utilizzato.<br /><br /> 1 = Utilizzato per operazioni di inserimento durante il popolamento o l'unione di un indice full-text.<br /><br /> 4 = Chiuso. Pronto per le query<br /><br /> 6 = Utilizzato per l'input unione e pronto per le query.<br /><br /> 8 = Contrassegnato per l'eliminazione. Non verrà utilizzato per le query e l'unione dell'origine.<br /><br /> Stato di 4 o 6 indica che il frammento fa parte dell'indice full-text logico e un possibile effettuarvi; in altre parole, si tratta di un *queryable* frammento.|  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare la vista del catalogo sys.fulltext_index_fragments per eseguire una query sul numero di frammenti compresi in un indice full-text. Se si verifica un rallentamento nell'esecuzione delle query full-text, è possibile utilizzare sys.fulltext_index_fragments per eseguire query per il numero di frammenti di tipo queryable (stato = 4 o 6) nell'indice full-text, come segue:  
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 Se esistono molti frammenti di tipo queryable, Microsoft consiglia di riorganizzare il catalogo full-text che contiene l'indice full-text per unire i frammenti. Per riorganizzare un utilizzo di catalogo full-text [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* REORGANIZE. Per riorganizzare, ad esempio, un catalogo full-text denominato `ftCatalog` nel database `AdventureWorks2012`, immettere:  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Popolamento degli indici full-text](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
