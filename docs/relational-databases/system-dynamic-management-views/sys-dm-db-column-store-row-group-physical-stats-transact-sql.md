---
title: sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e5e421935a9642c42a525fe8a25c4c8c9504c97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005013"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Vengono fornite informazioni a livello di gruppo di righe corrente su tutti gli indici columnstore nel database corrente.  
  
 Estende la vista del catalogo [column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella sottostante.|  
|**index_id**|**int**|ID di questo indice columnstore *object_id* tabella.|  
|**partition_number**|**int**|ID della partizione della tabella che contiene *row_group_id*. È possibile utilizzare il partition_number per creare un join di questa DMV a sys.partitions.|  
|**row_group_id**|**int**|ID di questo gruppo di righe. Per le tabelle partizionate, è univoco all'interno della partizione.<br /><br /> -1 per una coda in memoria.|  
|**delta_store_hobt_id**|**bigint**|Hobt_id per un gruppo di righe nell'archivio differenziale.<br /><br /> NULL se il gruppo di righe non è presente nell'archivio differenziale.<br /><br /> NULL per la parte finale di una tabella in memoria.|  
|**state**|**tinyint**|Numero di ID associato *a state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = PER LA RIMOZIONE DEFINITIVA<br /><br /> COMPRESSED è l'unico stato che si applica alle tabelle in memoria.|  
|**state_desc**|**nvarchar(60)**|Descrizione dello stato del gruppo di righe:<br /><br /> INVISIBILI - un gruppo di righe che si sta compilando. Ad esempio: <br />Un gruppo di righe nel columnstore è INVISIBILE, mentre i dati viene compresso. Al termine la compressione è un commutatore metadati viene modificato lo stato della riga di columnstore gruppo da INVISIBILE a COMPRESSED e lo stato del gruppo di righe deltastore da chiuso a per la rimozione definitiva.<br /><br /> Aprire - un gruppo di righe deltastore che sta accettando nuove righe. Un gruppo di righe aperto presenta ancora il formato rowstore e non è stato compresso nel formato columnstore.<br /><br /> CHIUSO - un gruppo di righe nell'archivio differenziale che contiene il numero massimo di righe ed è in attesa per il processo tuple-mover eseguirne la compressione nel columnstore.<br /><br /> COMPRESSI - un gruppo di righe che verrà compressi con la compressione columnstore e archiviato nel columnstore.<br /><br /> Per la rimozione definitiva - un gruppo di righe che era in precedenza nel deltastore e non viene più usato.|  
|**total_rows**|**bigint**|Numero di righe fisiche archiviato nel gruppo di righe. Per i gruppi di righe compressi, questo include le righe eliminate contrassegnate.|  
|**deleted_rows**|**bigint**|Numero di righe archiviate fisicamente in un gruppo di righe compressi che vengono contrassegnati per l'eliminazione.<br /><br /> 0 per i gruppi di righe che sono nell'archivio differenziale.|  
|**size_in_bytes**|**bigint**|Dimensioni combinate, in byte di tutte le pagine di questo gruppo di righe. Questa dimensione non include la dimensione necessaria per archiviare i metadati o i dizionari condivisi.|  
|**trim_reason**|**tinyint**|Motivo che ha attivato il gruppo di righe compressi per avere un valore minore il numero massimo di righe.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 - BULKLOAD<br /><br /> 3 - REORG<br /><br /> 4 - DICTIONARY_SIZE<br /><br /> 5 - MEMORY_LIMITATION<br /><br /> 6 - RESIDUAL_ROW_GROUP<br /><br /> 7  -  STATS_MISMATCH<br /><br /> 8 - SPILLOVER|  
|**trim_reason_desc**|**nvarchar(60)**|Descrizione della *trim_reason*.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: Si è verificato durante l'aggiornamento dalla versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: Il gruppo di righe non è stato tagliato. Il gruppo di righe è stata compressa con il numero massimo di 1,048,476 righe.  Potrebbe essere minore del numero di righe se un subsset delle righe è stato eliminato dopo che è stato chiuso il rowgroup delta<br /><br /> 2 - BULKLOAD: La dimensione del batch di caricamento bulk limitato il numero di righe.<br /><br /> 3 - REORG:  Forzare la compressione come parte del comando REORG.<br /><br /> 4 - DICTIONARY_SIZE: Dimensioni del dizionario aumento delle dimensioni troppo grandi per comprimere tutte le righe contemporaneamente.<br /><br /> 5 - MEMORY_LIMITATION: Non è sufficiente memoria disponibile per comprimere tutte le righe contemporaneamente.<br /><br /> 6 - RESIDUAL_ROW_GROUP:  Chiuso come parte dell'ultimo gruppo di righe con le righe < 1 milione durante l'operazione di compilazione indice<br /><br /> STATS_MISMATCH: Solo per columnstore nella tabella in memoria. Se indicato in modo non corretto stats > = 1 milione di righe qualificati nella parte finale, ma è stato rilevato un numero inferiore, il rowgroup compresso avrà < 1 milione di righe<br /><br /> SPILLOVER: Solo per columnstore nella tabella in memoria. Se della parte finale è > 1 milione di righe qualificati, le ultime righe rimanenti batch vengono compressi se il numero è compreso tra 1 milione e 100 KB|  
|**transition_to_compressed_state**|tinyint|Viene illustrato come questo rowgroup è stato spostato dal deltastore in uno stato compresso nel columnstore.<br /><br /> 1- NOT_APPLICABLE<br /><br /> 2 - INDEX_BUILD<br /><br /> 3 - TUPLE_MOVER<br /><br /> 4 - REORG_NORMAL<br /><br /> 5 - REORG_FORCED<br /><br /> 6 - BULKLOAD<br /><br /> 7 - UNIONE|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE - l'operazione non è applicabile per il deltastore. O, il rowgroup è stato compresso prima dell'aggiornamento a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nel qual caso non viene mantenuta la cronologia.<br /><br /> Creare un indice INDEX_BUILD - o ricompilazione di indici compressi i rowgroup.<br /><br /> TUPLE_MOVER - il processo tuple-mover in esecuzione in background compressi i rowgroup. Ciò si verifica dopo che il rowgroup viene modificato lo stato dallo stato aperto su chiuso.<br /><br /> REORG_NORMAL - l'operazione di riorganizzazione, ALTER INDEX... REORG, spostare i rowgroup CLOSED dal deltastore nel ColumnStore. Ciò si è verificato prima che il motore di tuple ha avuto tempo per spostare i rowgroup.<br /><br /> REORG_FORCED - questo rowgroup è stato aperto nel deltastore ed è stato forzato nel columnstore prima che aveva un numero di righe completo.<br /><br /> BULKLOAD - un'operazione di caricamento bulk compressi i rowgroup direttamente senza usare l'archivio differenziale.<br /><br /> MERGE - un'operazione di unione consolidati uno o più rowgroup in questo rowgroup e quindi eseguita la compressione columnstore.|  
|**has_vertipaq_optimization**|bit|Ottimizzazione Vertipaq ridisporre l'ordine delle righe nel rowgroup per ottenere maggiore compressione migliora la compressione del columnstore. Questa ottimizzazione viene eseguita automaticamente nella maggior parte dei casi. Esistono due casi ottimizzazione Vertipaq non viene usato:<br/>  a. Quando si sposta un rowgroup differenziali nel columnstore e sono presenti uno o più indici non cluster sull'indice columnstore, in questo caso ottimizzazione Vertipaq viene ignorata per ridurre al minimo le modifiche per l'indice di mapping;<br/> b. per gli indici columnstore nelle tabelle ottimizzate per la memoria. <br /><br /> 0 = No<br /><br /> 1 = Sì|  
|**generazione**|bigint|Generazione di gruppo di righe associata a questo gruppo di righe.|  
|**created_time**|datetime2|Ora di orologio per quando è stato creato questo rowgroup.<br /><br /> NULL - per un indice columnstore in una tabella in memoria.|  
|**closed_time**|datetime2|Tempo per cui è stata chiusa questo rowgroup.<br /><br /> NULL - per un indice columnstore in una tabella in memoria.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="results"></a>Risultati  
 Restituisce una riga per ogni gruppo di righe nel database corrente.  
  
## <a name="permissions"></a>Permissions  
 Richiede le autorizzazioni seguenti:  
  
-   Autorizzazione CONTROL per la tabella.  
  
-   Autorizzazione VIEW DATABASE STATE nel database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>R. Calcolare fragmentaton per decidere quando riorganizzare o ricompilare un indice columnstore.  
 Per gli indici columnstore, la percentuale di righe eliminate è un'ottima misura frammentazione in un rowgroup. Quando la frammentazione è 20% o più che si consiglia di rimuovere le righe eliminate.  Per esempi, vedere [deframmentazione degli indici Columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 In questo esempio viene aggiunto **DM db_column_store_row_group_physical_stats** con altri sistemi di tabelle e quindi calcola il `Fragmentation` colonna come una stima dell'efficienza di ogni gruppo di righe nel database corrente.     Per trovare informazioni su una singola tabella, rimuovere il commento trattini davanti il **in cui** clausola e fornire un nome di tabella.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0) AS 'Fragmentation'
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
