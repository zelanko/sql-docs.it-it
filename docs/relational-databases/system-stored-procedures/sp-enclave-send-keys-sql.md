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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661355"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Invia tutte le chiavi di crittografia della colonna abilitata per l'enclave nel database all'enclave utilizzata da [Always Encrypted con enclavi &#40;sicure motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintassi  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argomenti

Questo stored procedure non dispone di argomenti.

## <a name="return-value"></a>Valore restituito

Questo stored procedure non restituisce alcun valore.
  
## <a name="result-sets"></a>Set di risultati

Questa stored procedure non include set di risultati.
  
## <a name="remarks"></a>Note

**sp_enclave_send_keys** Invia le chiavi di crittografia della colonna abilitata per l'enclave all'enclave se vengono soddisfatte tutte le condizioni seguenti:

- L'enclave è abilitata nell'istanza di SQL Server.
- **sp_enclave_send_keys** è stato richiamato da un'applicazione che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un driver client, che supporta always Encrypted con enclavi sicure usando una connessione di database con Always Encrypted e calcoli enclave abilitati.

## <a name="permissions"></a>Permissions

 Richiedere le autorizzazioni **Visualizza definizione chiave di crittografia della colonna** e **Visualizza tutte le definizioni della chiave master della colonna** nel database.  
  
## <a name="examples"></a>Esempi  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Vedere anche

 [Always Encrypted con enclavi sicure &#40;motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Esercitazione: Creazione e utilizzo di indici su colonne abilitate per l'enclave mediante crittografia casuale](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Richiamare le operazioni di indicizzazione utilizzando le chiavi di crittografia della colonna](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Indici nelle colonne abilitate per l'enclave usando la crittografia casuale](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Considerazioni per la migrazione di database e AlwaysOn](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
