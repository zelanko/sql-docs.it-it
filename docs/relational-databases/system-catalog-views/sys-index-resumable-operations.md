---
title: index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c934c2fe8357cb4d37484984998edfcb7219c649
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122659"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**index_resumable_operations** è una vista di sistema che monitora e controlla lo stato di esecuzione corrente per la ricompilazione dell'indice ripristinabile.  
**Si applica a**: SQL Server 2017 e Azure SQL Database
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto a cui appartiene (non ammette valori null) dell'indice.|  
|**index_id**|**int**|ID dell'indice (non ammette valori null). **index_id** è univoco solo all'interno dell'oggetto.|
|**name**|**sysname**|Nome dell'indice. **nome** è univoco solo all'interno dell'oggetto.|  
|**sql_text**|**nvarchar(max)**|Testo dell'istruzione DDL T-SQL|
|**last_max_dop**|**smallint**|Ultimo MAX_DOP, inteso utilizzato (predefinito = 0)|
|**partition_number**|**int**|Numero di partizione all'interno dell'indice o heap di appartenenza. Per gli indici e tabelle non partizionate oppure nel caso tutte le partizioni sono in fase di ricompilazione, il valore di questa colonna è NULL.|
|**state**|**tinyint**|Stato operativo per operazioni su indici ripristinabili:<br /><br />0 = in esecuzione<br /><br />1=Pause|
|**state_desc**|**nvarchar(60)**|Descrizione dello stato operativo per l'indice ripristinabile (in esecuzione o sospesa)|  
|**start_time**|**datetime**|Ora di inizio operazione indice (non ammette valori null)|
|**last_pause_time**|**datatime**| Operazione sull'indice ora ultima pausa (ammette valori null). NULL se l'operazione è in esecuzione e mai in pausa.|
|**total_execution_time**|**int**|Tempo totale di esecuzione dall'ora di inizio in pochi minuti (non ammette valori null)|
|**percent_complete**|**real**|Indice operazione lo stato di avanzamento completamento in % (non ammette valori null).|
|**page_count**|**bigint**|Numero totale di pagine di indice allocate per l'operazione di compilazione per il nuovo indice e gli indici di mapping (non ammette valori null).

## <a name="permissions"></a>Permissions

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="example"></a>Esempio

 Elenca tutte le operazioni di ricompilazione dell'indice ripristinabile che sono nello stato di sospensione.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>Vedere anche

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [Viste del catalogo](catalog-views-transact-sql.md)
- [Viste del catalogo dell'oggetto](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](querying-the-sql-server-system-catalog-faq.md)
