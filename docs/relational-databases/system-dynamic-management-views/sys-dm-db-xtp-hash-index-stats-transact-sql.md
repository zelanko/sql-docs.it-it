---
title: sys.dm_db_xtp_hash_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2bbaaaa6770c5644da227c7e64a9ff9e0fc2c13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026844"
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Queste statistiche sono utili per la comprensione e l'ottimizzazione del numero di bucket. Possono anche essere utilizzate per rilevare i casi in cui la chiave di indice ha molti duplicati.  
  
 Una lunghezza media della catena elevata indica che è stato eseguito l'hashing nello stesso bucket di molte righe. Questa situazione potrebbe verificarsi:  
  
-   Se il numero di bucket vuoti è insufficiente o le lunghezze media e massima della catena sono simili, è probabile che il numero totale di bucket sia troppo basso. Per questo motivo, viene eseguito l'hashing nello stesso bucket di molte chiavi di indice.  
  
-   Se il numero di bucket vuoti è elevato o la lunghezza massima della catena è elevata rispetto alla lunghezza media della catena, è probabile che esistano molte righe con valori di chiave di indice duplicati o che vi sia uno scostamento nei valori della chiave. L'hashing di tutte le righe con lo stesso valore di chiave di indice viene eseguito nello stesso bucket, pertanto in questo bucket la lunghezza della catena è piuttosto elevata.  
  
Le catene molto lunghe possono influire significativamente sulle prestazioni delle operazioni DML sulle singole righe, incluse SELECT e INSERT. Le catene corte associate a un numero di bucket vuoto elevato indicano un valore bucket_count troppo elevato. Ne consegue un calo delle prestazioni delle analisi degli indici.  
  
> [!WARNING]
> **DM db_xtp_hash_index_stats** analizza l'intera tabella. Pertanto, se sono presenti tabelle di grandi dimensioni nel database **DM db_xtp_hash_index_stats** potrebbe richiedere molto tempo esecuzione.  
  
Per altre informazioni, vedere [Hash Indexes for Memory-Optimized Tables indici](../../relational-databases/sql-server-index-design-guide.md#hash_index).  
  
|Nome colonna|type|Descrizione|  
|-----------------|----------|-----------------|  
|object_id|**int**|ID oggetto della tabella padre.|  
|xtp_object_id|**bigint**|ID della tabella con ottimizzazione per la memoria.|  
|index_id|**int**|ID indice.|  
|total_bucket_count|**bigint**|Numero totale di bucket di hash nell'indice.|  
|empty_bucket_count|**bigint**|Numero totale di bucket di hash vuoti nell'indice.|  
|avg_chain_length|**bigint**|La lunghezza media della riga concatena tutti i bucket di hash nell'indice.|  
|max_chain_length|**bigint**|Lunghezza massima delle catene di righe nel bucket di hash.|  
|xtp_object_id|**bigint**|L'ID di oggetto OLTP in memoria corrispondente alla tabella con ottimizzazione per la memoria.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il server.  

## <a name="examples"></a>Esempi  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>R. Risoluzione dei problemi relativi al numero di bucket dell'indice hash

La query seguente può essere utilizzata per risolvere il numero di bucket dell'indice hash di una tabella esistente. La query restituisce statistiche sulla percentuale di bucket vuoti e lunghezza della catena per tutti gli indici hash nelle tabelle utente.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

Per informazioni dettagliate su come interpretare i risultati della query, vedere [risoluzione dei problemi di indici Hash per tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) .  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. Statistiche dell'indice hash per le tabelle interne

Alcune funzionalità di usare le tabelle interne che consentono di sfruttare gli indici hash, ad esempio gli indici columnstore nelle tabelle ottimizzate per la memoria. La query seguente restituisce statistiche per gli indici hash in tabelle interne in cui sono collegate alle tabelle utente.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

Si noti che non è possibile modificare il valore di BUCKET_COUNT dell'indice per le tabelle interne, pertanto l'output di questa query deve essere considerata informativo solo. Non è richiesta alcuna azione.  

Questa query non è previsto per restituire tutte le righe, a meno che non si usa una funzionalità che sfrutta gli indici hash nelle tabelle interne. La tabella con ottimizzazione per la memoria seguente contiene un indice columnstore. Dopo la creazione di questa tabella, si vedrà gli indici hash per le tabelle interne.

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>Vedere anche  
 [Memoria-con ottimizzazione per la tabella viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
