---
title: Gestire le chiavi per Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d3968c5c8f04cba8581dfdd44ac847f7010de994
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595626"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gestire le chiavi per Always Encrypted con enclave sicuri
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) estende la gestione delle chiavi per [Always Encrypted](always-encrypted-database-engine.md) introducendo le chiavi abilitate per l'enclave: 

- **Chiave master di colonna abilitata per l'enclave** - Chiave master della colonna creata con la proprietà `ENCLAVE_COMPUTATIONS` specificata nell'oggetto metadati chiave master della colonna all'interno del database. 
- **Chiave di crittografia di colonna abilitata per l'enclave** - Chiave di crittografia di colonna crittografata con una chiave master della colonna abilitata per l'enclave. Solo le chiavi di crittografia di colonna abilitata per l'enclave possono essere usate per i calcoli all'interno di un enclave sicuro lato server. 

Le linee guida e i processi generali per la [gestione delle chiavi Always Encrypted](overview-of-key-management-for-always-encrypted.md) si applicano alla gestione delle chiavi abilitate per l'enclave. 

## <a name="managing-keys"></a>Gestione delle chiavi

Gli articoli seguenti illustrano gli aspetti specifici della gestione delle chiavi abilitate per l'enclave.

- [Effettuare il provisioning delle chiavi abilitate per l'enclave](always-encrypted-enclaves-provision-keys.md)
- [Ruotare le chiavi abilitate per l'enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>Next Steps
- [Effettuare il provisioning delle chiavi abilitate per l'enclave](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>Vedere anche  
- [Panoramica della gestione delle chiavi per Always Encrypted](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
