---
title: sys.column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: df7698d222c2c2f0f68138eaa5f6289106b97659
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62799873"
---
# <a name="syscolumnstoresegments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Restituisce una riga per ogni segmento di colonna in un indice columnstore. È presente un segmento di colonna per ogni colonna per ogni rowgroup. Ad esempio, una tabella con 10 gruppi di righe e 34 colonne restituisce 340 righe. 
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica l'ID della partizione. Valore univoco all'interno di un database.|  
|**hobt_id**|**bigint**|ID dell'heap o dell'indice ad albero B (HoBT) per la tabella a cui appartiene l'indice columnstore.|  
|**column_id**|**int**|ID della colonna columnstore.|  
|**segment_id**|**int**|ID del rowgroup. Per garantire la compatibilità con le versioni precedenti, il nome della colonna continua a essere chiamato segment_id anche se questo è l'ID del rowgroup. È possibile identificare in modo univoco un segmento usando \<hobt_id, partition_id, column_id >, < segment_id >.|  
|**version**|**int**|Versione del formato del segmento di colonna.|  
|**encoding_type**|**int**|Tipo di codifica utilizzato per il segmento:<br /><br /> 1 = VALUE_BASED - non stringa o binari con alcun dizionario (molto simile a 4 con alcune variazioni interni)<br /><br /> 2 = VALUE_HASH_BASED - colonne non stringa o binari con valori comuni nel dizionario<br /><br /> 3 = STRING_HASH_BASED - colonna stringa/binario con i valori comuni nel dizionario<br /><br /> 4 = STORE_BY_VALUE_BASED - non stringa o binari con alcun dizionario<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED - stringa/binario con alcun dizionario<br /><br /> Tutte le codifiche di sfruttano i vantaggi della compressione di bit e la lunghezza di esecuzione codifica quando possibile.|  
|**row_count**|**int**|Numero di righe nel gruppo di righe.|  
|**has_nulls**|**int**|1 se il segmento di colonna contiene valori Null.|  
|**base_id**|**bigint**|Viene usato l'id di valore di base se il tipo di codifica 1.  Se il tipo di codifica 1 non utilizzato, base_id viene impostato su -1.|  
|**magnitude**|**float**|Magnitude se viene utilizzato il tipo di codifica 1.  Se il tipo di codifica 1 non utilizzato, magnitude viene impostato su -1.|  
|**primary_dictionary_id**|**int**|Un valore pari a 0 rappresenta il dizionario globale. Il valore -1 indica che non vi sia alcun dizionario globale creato per questa colonna.|  
|**secondary_dictionary_id**|**int**|Un valore diverso da zero punta al dizionario locale per la colonna nel segmento corrente (ad esempio il gruppo di righe). Il valore -1 indica che non vi sia alcun dizionario locale per questo segmento.|  
|**min_data_id**|**bigint**|ID dati minimo nel segmento di colonna.|  
|**max_data_id**|**bigint**|ID dati massimo nel segmento di colonna.|  
|**null_value**|**bigint**|Valore utilizzato per rappresentare i valori Null.|  
|**on_disk_size**|**bigint**|Dimensioni del segmento in byte.|  
  
## <a name="remarks"></a>Note  
 Nella query seguente vengono restituite le informazioni sui segmenti di un indice columnstore.  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 Tutte le colonne richiedono almeno **VIEW DEFINITION** autorizzazione per la tabella. Le colonne seguenti restituiscono null a meno che l'utente ha inoltre **seleziona** autorizzazione: has_nulls, base_id, magnitude, min_data_id, max_data_id e null_value.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

