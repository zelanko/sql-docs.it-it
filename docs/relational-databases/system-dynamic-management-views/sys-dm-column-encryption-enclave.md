---
title: sys. dm_column_encryption_enclave (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d10bef0df04501c177086b6c89b3f67dec3bab10
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "73599244"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Restituisce i contatori delle prestazioni per l'enclave protetta per Always Encrypted. Per altre informazioni, vedere [Always Encrypted con enclave sicuri](../security/encryption/always-encrypted-enclaves.md).

Se l'enclave è configurata ed è stata inizializzata correttamente dopo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l'ultimo riavvio di, la vista contiene esattamente una riga. Se l'enclave non è configurato o non è stato inizializzato correttamente, la vista non restituisce alcuna riga. 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|Numero corrente di sessioni client che utilizzano l'enclave.|  
|current_column_encryption_key_count|**int**|Conteggio delle chiavi di crittografia della colonna attualmente contenute nell'enclave.|  
|current_memory_size_kb|**bigint**|Dimensioni memoria enclave in KB|  
|total_evicted_session_count|**bigint**|Conteggio totale delle sessioni dell'enclave eliminate dall'ultimo riavvio del server.|   
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'autorizzazione `VIEW SERVER STATE`.   
  
## <a name="examples"></a>Esempi  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare il tipo di enclave per l'opzione di configurazione del server Always Encrypted](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
