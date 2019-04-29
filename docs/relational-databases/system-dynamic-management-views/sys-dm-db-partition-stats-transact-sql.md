---
title: sys.dm_db_partition_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0221361bb3b2bb33748b20353c71931e07568f3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025110"
---
# <a name="sysdmdbpartitionstats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni relative al conteggio di pagine e righe per ogni partizione nel database corrente.  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **DM pdw_nodes_db_partition_stats**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|ID della partizione. Valore univoco all'interno di un database. Questo è lo stesso valore di **partition_id** nel **Sys. Partitions** vista del catalogo|  
|**object_id**|**int**|ID oggetto della tabella o della vista indicizzata a cui appartiene la partizione.|  
|**index_id**|**int**|ID dell'heap o dell'indice a cui appartiene la partizione.<br /><br /> 0 = heap<br /><br /> 1 = Indice cluster<br /><br /> > 1 = indice non cluster|  
|**partition_number**|**int**|Numero di partizione in base 1 all'interno dell'indice o heap.|  
|**in_row_data_page_count**|**bigint**|Numero di pagine utilizzate per l'archiviazione di dati all'interno di righe nella partizione specifica. Se la partizione è inclusa in un heap, il valore corrisponde al numero di pagine di dati nell'heap. Se la partizione è inclusa in un indice, il valore corrisponde al numero di pagine nel livello foglia. (Le pagine non foglia nell'albero B non incluse nel conteggio). Le pagine IAM (Index Allocation Map) non sono inclusi in entrambi i casi. Sempre 0 per un indice columnstore con ottimizzazione per la memoria xVelocity.|  
|**in_row_used_page_count**|**bigint**|Numero totale di pagine utilizzate per archiviare e gestire i dati all'interno di righe nella partizione corrente. Questo conteggio include pagine non foglia dell'albero B, le pagine IAM e tutte le pagine incluse nel **in_row_data_page_count** colonna. Sempre 0 per un indice columnstore.|  
|**in_row_reserved_page_count**|**bigint**|Numero totale di pagine riservate per l'archiviazione e la gestione dei dati all'interno di righe nella partizione corrente, indipendentemente dal fatto che le pagine siano utilizzate o meno. Sempre 0 per un indice columnstore.|  
|**lob_used_page_count**|**bigint**|Numero di pagine utilizzate per archiviare e gestire out-of-row **testo**, **ntext**, **immagine**, **varchar (max)**, **nvarchar (max)** , **varbinary (max)**, e **xml** colonne all'interno della partizione. Le pagine IAM sono incluse.<br /><br /> Numero totale di oggetti LOB utilizzati per archiviare e gestire un indice columnstore nella partizione.|  
|**lob_reserved_page_count**|**bigint**|Numero totale di pagine riservate per l'archiviazione e la gestione di out-of-row **testo**, **ntext**, **immagine**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, e **xml** colonne all'interno della partizione, indipendentemente dal fatto che le pagine sono in uso o non. Le pagine IAM sono incluse.<br /><br /> Numero totale di oggetti LOB riservati per l'archiviazione e la gestione di un indice columnstore nella partizione.|  
|**row_overflow_used_page_count**|**bigint**|Numero di pagine utilizzate per archiviare e gestire l'overflow della riga **varchar**, **nvarchar**, **varbinary**, e **sql_variant** colonne all'interno della partizione. Le pagine IAM sono incluse.<br /><br /> Sempre 0 per un indice columnstore.|  
|**row_overflow_reserved_page_count**|**bigint**|Numero totale di pagine riservate per l'archiviazione e la gestione di overflow della riga **varchar**, **nvarchar**, **varbinary**, e **sql_variant** colonne all'interno della partizione, indipendentemente dal fatto che le pagine sono in uso o non. Le pagine IAM sono incluse.<br /><br /> Sempre 0 per un indice columnstore.|  
|**used_page_count**|**bigint**|Numero totale di pagine utilizzate per la partizione, Calcolato come **in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**.|  
|**reserved_page_count**|**bigint**|Numero totale di pagine riservate per la partizione Calcolato come **in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**.|  
|**row_count**|**bigint**|Numero approssimato di righe nella partizione.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
|**distribution_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Id numerico univoco associata alla distribuzione.|  
  
## <a name="remarks"></a>Note  
 **DM db_partition_stats** Visualizza informazioni sullo spazio usato per archiviare e gestire i dati LOB di dati in righe e i dati di overflow della riga per tutte le partizioni in un database. Viene visualizzata una riga per partizione.  
  
 I conteggi su cui si basa l'output vengono inseriti nella cache in memoria oppure archiviati su disco in varie tabelle di sistema.  
  
 I dati all'interno di righe, i dati LOB e i dati di overflow della riga rappresentano tre unità di allocazione che compongono una partizione. Il [Sys. allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) vista del catalogo è possibile eseguire query per i metadati relativi a ogni unità di allocazione nel database.  
  
 Se un heap o un indice non è partizionato, esso è composto da una partizione (con numero di partizione = 1). Per tale heap o indice viene pertanto restituita solo una riga. Il [Sys. Partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) vista del catalogo è possibile eseguire query per i metadati relativi a ogni partizione di tutte le tabelle e indici di un database.  
  
 Il conteggio totale relativo a una tabella specifica o un indice specifico può essere ottenuto tramite l'aggiunta dei conteggi per tutte le partizioni rilevanti.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per eseguire query di **DM db_partition_stats** vista a gestione dinamica. Per altre informazioni sulle autorizzazioni sulle viste a gestione dinamica, vedere [funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>A. Restituzione di tutti i conteggi per tutte le partizioni di tutti gli indici e heap in un database  
 Nell'esempio seguente vengono visualizzati tutti i conteggi per tutte le partizioni di tutti gli indici e heap nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. Restituzione di tutti i conteggi per tutte le partizioni di una tabella e dei relativi indici  
 Nell'esempio seguente vengono visualizzati tutti i conteggi per tutte le partizioni della tabella `HumanResources.Employee` e dei relativi indici.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. Restituzione del numero totale di pagine utilizzate e del numero totale di righe per un heap o un indice cluster  
 Nell'esempio seguente vengono restituiti il numero totale di pagine utilizzate e il numero totale di righe per l'heap o l'indice cluster della tabella `HumanResources.Employee`. Poiché per impostazione predefinita la tabella `Employee` non è partizionata, la somma include solo una partizione.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


