---
title: sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cb87d2d5677085edc8e6bd998f20c3c45013823
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262085"
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Restituisce [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) informazioni del log delle transazioni. Si noti che nell'output della tabella vengono combinati tutti i file di log delle transazioni. Ogni riga nell'output rappresenta un VLF nel log delle transazioni e fornisce le informazioni rilevanti per tale VLF nel log.

## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>Argomenti  
 *database_id* | NULL | IMPOSTAZIONE PREDEFINITA  
 ID del database. *database_id* è di tipo **int**. Gli input validi sono il numero di ID di un database, NULL o predefinito. Il valore predefinito è NULL. NULL e DEFAULT sono valori equivalenti nel contesto del database corrente.
 
 Specificare NULL per restituire le informazioni VLF del database corrente.

 La funzione predefinita [DB_ID](../../t-sql/functions/db-id-transact-sql.md) può essere specificato. Quando si usa `DB_ID` senza specificare un nome di database, il livello di compatibilità del database corrente deve essere maggiore o uguale a 90.  

## <a name="table-returned"></a>Tabella restituita  

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID del database.|
|file_id|**smallint**|Id file del log delle transazioni.|  
|vlf_begin_offset|**bigint** |Offset di posizione di [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) dall'inizio del file di log delle transazioni.|
|vlf_size_mb |**float** |[file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) dimensione in MB, arrotondato a 2 cifre decimali.|     
|vlf_sequence_number|**bigint** |[file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) progressivo nell'ordine creato. Utilizzato per identificare in modo univoco VLF nel file di log.|
|vlf_active|**bit** |Indica se [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) sia o meno in uso. <br />0 - file di log Virtuali non è in uso.<br />1 - VLF è attivo.|
|vlf_status|**int** |Stato del [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). I valori possibili includono <br />0 - file di log Virtuali non è attivo <br />1 - VLF è inizializzato ma non utilizzati <br /> 2 - VLF è attivo.|
|vlf_parity|**tinyint** |Parità della [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Utilizzato internamente per determinare la fine del log all'interno di un file di log Virtuali.|
|vlf_first_lsn|**nvarchar(48)** |[Sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del primo record di log nel [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_create_lsn|**nvarchar(48)** |[Sequenza numero di log (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del log di record che ha creato la [file di log virtuale (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_encryptor_thumbprint|**varbinary(20)**| **Si applica a:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> Indica l'identificazione digitale del componente di crittografia del VLF se il file di log Virtuali vengono crittografati usando [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md), in caso contrario, NULL. |

## <a name="remarks"></a>Note
Il `sys.dm_db_log_info` funzione a gestione dinamica sostituisce il `DBCC LOGINFO` istruzione.    
 
## <a name="permissions"></a>Permissions  
Richiede il `VIEW DATABASE STATE` autorizzazione nel database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>R. Metodo database in un'istanza di SQL Server con numero elevato di file di log virtuali
La query seguente identifica i database con più di 100 file di log virtuali nei file di log, che possono influenzare il tempo di avvio, ripristino e ripristino di database.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Determinare la posizione dell'ultimo `VLF` nel log delle transazioni prima della compattazione del file di log

La query seguente è utilizzabile per determinare la posizione dell'ultimo VLF attive prima di eseguire shrinkfile nel log delle transazioni per determinare se è possibile ridurre del log delle transazioni.

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>Vedere anche  
[Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Viste a gestione dinamica relative ai database &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

