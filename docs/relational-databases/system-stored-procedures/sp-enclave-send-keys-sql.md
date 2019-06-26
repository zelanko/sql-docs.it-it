---
title: sp_enclave_send_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6540cdd36cccba4f5a7ccb3beddf31ce00cd9107
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394143"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Invia enclave abilitate tutte le colonne delle chiavi di crittografia nel database per l'enclave utilizzato da [Always Encrypted con zone franche sicuri &#40;motore di Database&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintassi  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argomenti

Questa stored procedure non dispone di argomenti.

## <a name="return-value"></a>Valore restituito

Questa stored procedure non restituisce alcun valore.
  
## <a name="result-sets"></a>Set di risultati

Questa stored procedure non dispone di alcun set di risultati.
  
## <a name="remarks"></a>Note

**sp_enclave_send_keys** invia le chiavi di crittografia di colonna abilitata enclave all'enclave se vengono soddisfatte tutte le condizioni seguenti:

- L'enclave è abilitato nell'istanza di SQL Server.
- **sp_enclave_send_keys** è stato richiamato da un'applicazione che usa un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver del client, il supporto di Always Encrypted con zone franche protette utilizzando una connessione di database che contiene i calcoli enclave sia Always Encrypted abilitati.

## <a name="permissions"></a>Permissions

 Richiede la **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** e **VIEW ANY COLUMN MASTER KEY DEFINITION** autorizzazioni nel database.  
  
## <a name="examples"></a>Esempi  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Vedere anche

 [Always Encrypted con zone franche sicuri &#40;motore di Database&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Esercitazione: Creazione e utilizzo di indici nelle colonne basate su enclave tramite la crittografia casuale](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Richiamare operazioni di indicizzazione mediante chiavi di crittografia di colonna memorizzati nella cache](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Indici nelle colonne basate su Enclave usando la crittografia casuale](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Considerazioni per la migrazione del Database e AlwaysOn](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
