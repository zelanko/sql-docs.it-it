---
title: Sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a86c559adeeca787ac0e278eed5fb832b8c00bfd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537901"
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni set di righe che tiene traccia di dati interne per gli indici columnstore nelle tabelle basate su disco. Questi set di righe sono interni agli indici columnstore e track eliminato righe, i mapping di rowgroup e differenziali archiviano i rowgroup. Consentono di tenere traccia dei dati per ciascuno di essi per ogni partizione della tabella; ogni tabella contiene almeno una partizione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ricrea i set di righe ogni volta che viene ricompilato l'indice columnstore.   
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|ID di partizione per questa partizione. Valore univoco all'interno di un database.|  
|object_id|**int**|ID oggetto per la tabella contenente la partizione.|  
|index_id|**int**|ID dell'indice per l'indice columnstore definito nella tabella.<br /><br /> 1 = indice columnstore cluster<br /><br /> 2 = indice columnstore non cluster|  
|partition_number|**int**|Il numero di partizione.<br /><br /> 1 = prima partizione di una tabella partizionata o la singola partizione di una tabella non partizionata.<br /><br /> 2 = seconda partizione e così via.|  
|internal_object_type|**tinyint**|Oggetti set di righe che tengono traccia dei dati interne per l'indice columnstore.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP - l'indice bitmap tiene traccia delle righe che sono contrassegnate come eliminate dal columnstore. La bitmap è per ogni rowgroup, poiché le partizioni possono avere le righe in più rowgroup. Le righe siano che siano ancora fisicamente presenti e occuperà spazio nel columnstore.<br /><br /> COLUMN_STORE_DELTA_STORE - gruppi di punti vendita di righe, dette rowgroup, che non sono state compresse nell'archiviazione a colonne. Ogni partizione della tabella può avere zero o più rowgroup deltastore.<br /><br /> COLUMN_STORE_DELETE_BUFFER - per la gestione delle eliminazioni per gli indici columnstore non cluster aggiornabili. Quando una query consente di eliminare una riga della tabella rowstore sottostante, del buffer di eliminazione rileva l'eliminazione dal columnstore. Quando il numero di righe eliminate supera 1048576, vengono uniti in delete bitmap con sfondo thread di processo Tuple-Mover o da un comando Reorganize esplicito.  In qualsiasi momento nel tempo, l'unione tra la bitmap di eliminazione e buffer di eliminazione rappresenta eliminate tutte le righe.<br /><br /> COLUMN_STORE_MAPPING_INDEX - utilizzato solo quando l'indice columnstore cluster include un indice non cluster secondario. Esegue il mapping delle chiavi di indice non cluster per il corretto rowgroup e l'ID di riga nel columnstore. Archivia solo le chiavi per le righe da spostare in un gruppo di righe diverso; Ciò si verifica quando un rowgroup differenziale viene compresso nel columnstore e quando un'operazione di unione unisce le righe da due diversi rowgroup.|  
|Row_group_id|**int**|ID del rowgroup deltastore. Ogni partizione della tabella può avere zero o più rowgroup deltastore.|  
|hobt_id|**bigint**|ID dell'oggetto set di righe interno. Si tratta di una chiave valida per l'unione con altre viste a gestione dinamica per ottenere altre informazioni sulle caratteristiche fisiche del set di righe interno.|  
|rows|**bigint**|Numero approssimativo di righe nella partizione.|  
|data_compression|**tinyint**|Lo stato di compressione per il set di righe:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|Lo stato di compressione per ogni partizione. I valori possibili per le tabelle rowstore sono NONE, ROW e PAGE. I valori possibili per le tabelle columnstore sono COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Osservazioni generali  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Crea nuovi indici interna columnstore nuovamente ogni volta che crea o si ricompila un indice columnstore.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. Visualizzare tutti i set di righe interno per una tabella  
 In questo esempio restituisce tutti i set di righe columnstore interno per una tabella. È anche possibile usare hobt_id per trovare altre informazioni sul set di righe specifico.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
