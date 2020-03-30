---
title: Eseguire query delle colonne usando Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d0a522d6deb01169189d6f5faaf7ba2f189d1522
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595506"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Eseguire query delle colonne usando Always Encrypted con enclave sicuri
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Questo articolo illustra le considerazioni generali per l'esecuzione di query su colonne crittografate usando un enclave sicuro lato server per [Always Encrypted con enclave sicuri](always-encrypted-enclaves.md). 

I tipi di query seguenti comportano l'uso di un enclave sicuro:
- Query che attivano operazioni di crittografia sul posto usando chiavi abilitate per l'enclave. Vedere [Configurare la crittografia delle colonne sul posto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md).
- *Query avanzate*: confronti di intervalli o operazioni basate su criteri di ricerca su colonne crittografate con la crittografia casuale e le chiavi abilitate per l'enclave.
- Query che creano o aggiornano indici su colonne crittografate con la crittografia casuale e le chiavi abilitate per l'enclave. Per altre informazioni, vedere [Creare e usare indici in colonne usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-create-use-indexes.md).

> [!NOTE]
> Le query avanzate e gli indici sono supportati solo nelle colonne abilitate per l'enclave (colonne crittografate con chiavi di crittografia di colonna abilitate per l'enclave) che usano la crittografia casuale. La crittografia deterministica non supporta le query avanzate o gli indici.

> [!NOTE]
> Le query avanzate su colonne crittografate di tipo stringa di caratteri richiedono che le colonne usino le regole di confronto con un ordinamento binary2 (regole di confronto BIN2). 


## <a name="next-steps"></a>Passaggi successivi
- [Eseguire query delle colonne usando Always Encrypted con enclave sicuri con SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>Vedere anche
- [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)

