---
title: sys.dm_tran_version_store (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d993cd06d555a9d4136274b35242477df1b304e9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262597"
---
# <a name="sysdmtranversionstore-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una tabella virtuale in cui vengono visualizzati tutti i record di versione nell'archivio delle versioni. **DM tran_version_store** è poco efficiente per l'esecuzione perché viene eseguita una query all'intero archivio versioni e l'archivio delle versioni può essere molto grande.  
  
 Ogni record con versione viene archiviato come dato binario con alcune informazioni di rilevamento o stato. Analogamente ai record nelle tabelle di database, i record inclusi nell'archivio delle versioni vengono archiviati in pagine da 8192 byte. In caso di dimensioni superiori a 8192 byte, il record verrà suddiviso in due record distinti.  
  
 Poiché il record con versione viene archiviato come dato binario, non si verificheranno problemi in presenza di diverse regole di confronto di database diversi. Uso **DM tran_version_store** per trovare le versioni precedenti delle righe in rappresentazione binaria in cui si trovano nell'archivio delle versioni.  
  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Numero di sequenza della transazione che genera la versione del record.|  
|**version_sequence_num**|**bigint**|Numero di sequenza del record con versione. Questo valore è univoco all'interno della transazione di generazione della versione.|  
|**database_id**|**int**|ID di database del record con versione.|  
|**rowset_id**|**bigint**|ID del set di righe del record.|  
|**status**|**tinyint**|Indica se un record con versione è stato suddiviso in due record. Se il valore è 0, il record è archiviato in una pagina. Se è 1, il record è suddiviso in due record archiviati in due pagine diverse.|  
|**min_length_in_bytes**|**smallint**|Lunghezza minima del record in byte.|  
|**record_length_first_part_in_bytes**|**smallint**|Lunghezza della prima parte del record con versione, espressa in byte.|  
|**record_image_first_part**|**varbinary(8000)**|Immagine binaria della prima parte del record con versione.|  
|**record_length_second_part_in_bytes**|**smallint**|Lunghezza della seconda parte del record con versione, espressa in byte.|  
|**record_image_second_part**|**varbinary(8000)**|Immagine binaria della seconda parte del record con versione.|  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato uno scenario di test in cui quattro transazioni simultanee, ognuna identificata da un numero di sequenza della transazione (XSN), vengono eseguite in un database con le opzioni ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT impostate su ON. Vengono eseguite le transazioni seguenti:  
  
-   XSN-57 è un'operazione di aggiornamento con isolamento serializzabile.  
  
-   XSN-58 è uguale a XSN-57.  
  
-   XSN-59 è un'operazione di selezione con isolamento dello snapshot.  
  
-   XSN-60 è uguale a XSN-59.  
  
 Viene eseguita la query seguente.  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 L'output indica che XSN-57 ha creato tre versioni di riga da una tabella e che XSN-58 ha creato una versione di riga da un'altra tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
