---
title: sys. pdw_nodes_column_store_segments (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/28/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: julieMSFT
ms.author: jrasnick
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bea8e0d51b2918d7280f4afdb8b9d02f6b757827
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401674"
---
# <a name="syspdw_nodes_column_store_segments-transact-sql"></a>sys. pdw_nodes_column_store_segments (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Contiene una riga per ogni colonna in un indice columnstore.

| Nome colonna                 | Tipo di dati  | Descrizione                                                  |
| :-------------------------- | :--------- | :----------------------------------------------------------- |
| **partition_id**            | **bigint** | Indica l'ID della partizione. Valore univoco all'interno di un database.     |
| **hobt_id**                 | **bigint** | ID dell'heap o dell'indice ad albero B (HoBT) per la tabella a cui appartiene l'indice columnstore. |
| **column_id**               | **int**    | ID della colonna columnstore.                                |
| **segment_id**              | **int**    | ID del segmento della colonna. Per compatibilità con le versioni precedenti, il nome della colonna continua a essere chiamato segment_id anche se si tratta dell'ID rowgroup. È possibile identificare in modo univoco un segmento utilizzando <hobt_id, partition_id, column_id>, <segment_id>. |
| **Versione**                 | **int**    | Versione del formato del segmento di colonna.                        |
| **encoding_type**           | **int**    | Tipo di codifica usato per il segmento:<br /><br /> 1 = VALUE_BASED-non stringa/binario senza dizionario (simile a 4 con alcune varianti interne)<br /><br /> 2 = colonna VALUE_HASH_BASED-non stringa/binaria con valori comuni nel dizionario<br /><br /> 3 = colonna STRING_HASH_BASED-String/Binary con valori comuni nel dizionario<br /><br /> 4 = STORE_BY_VALUE_BASED-non stringa/binario senza dizionario<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-String/Binary senza dizionario<br /><br /> Tutte le codifiche sfruttano i vantaggi della codifica di bit e di lunghezza, quando possibile. |
| **row_count**               | **int**    | Numero di righe nel gruppo di righe.                             |
| **has_nulls**               | **int**    | 1 se il segmento di colonna contiene valori Null.                     |
| **base_id**                 | **bigint** | ID valore di base se viene utilizzato il tipo di codifica 1.  Se non viene utilizzato il tipo di codifica 1, base_id viene impostato su 1. |
| **magnitude**               | **float**  | Magnitude se viene utilizzato il tipo di codifica 1.  Se non viene utilizzato il tipo di codifica 1, magnitude viene impostato su 1. |
| **primary__dictionary_id**  | **int**    | ID del dizionario primario. Un valore diverso da zero punta al dizionario locale per questa colonna nel segmento corrente (ad esempio, rowgroup). Il valore-1 indica che non esiste alcun dizionario locale per questo segmento. |
| **secondary_dictionary_id** | **int**    | ID del dizionario secondario. Un valore diverso da zero punta al dizionario locale per questa colonna nel segmento corrente (ad esempio, rowgroup). Il valore-1 indica che non esiste alcun dizionario locale per questo segmento. |
| **min_data_id**             | **bigint** | ID dati minimo nel segmento di colonna.                       |
| **max_data_id**             | **bigint** | ID dati massimo nel segmento di colonna.                       |
| **null_value**              | **bigint** | Valore utilizzato per rappresentare i valori Null.                               |
| **on_disk_size**            | **bigint** | Dimensioni del segmento in byte.                                    |
| **pdw_node_id**             | **int**    | Identificatore univoco di un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo. |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Unire sys. pdw_nodes_column_store_segments ad altre tabelle di sistema per determinare il numero di segmenti columnstore per ogni tabella logica.

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name ;
```

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione **View Server state** .

## <a name="see-also"></a>Vedere anche

[SQL Data Warehouse e Parallel data warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
[CREARE un indice COLUMNStore &#40;&#41;Transact-SQL](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
[sys. pdw_nodes_column_store_row_groups &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
[sys. pdw_nodes_column_store_dictionaries &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)
