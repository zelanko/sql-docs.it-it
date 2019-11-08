---
title: Eseguire query delle colonne usando Always Encrypted con enclave sicuri con SSMS | Microsoft Docs
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
ms.openlocfilehash: 6bee04f4a794a503b89b73d4ef4a6a1cef897b4b
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595596"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>Eseguire query delle colonne usando Always Encrypted con enclave sicuri con SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Questo articolo descrive come usare SQL Server Management Studio per eseguire query che usano un'enclave sicuro lato server per [Always Encrypted con enclave sicuri](always-encrypted-enclaves.md), tra cui:
- Query che attivano operazioni di crittografia sul posto.
- Query che attivano calcoli avanzati, inclusi i confronti di intervalli o le operazioni basate su criteri di ricerca su colonne crittografate con chiavi abilitate per l'enclave.
- Query che creano o aggiornano indici su colonne crittografate con la crittografia casuale e le chiavi abilitate per l'enclave.  

Per usare SSMS per eseguire query su colonne crittografate usando un enclave sicuro, seguire le istruzioni in [Eseguire query delle colonne usando Always Encrypted con SQL Server Management Studio](always-encrypted-query-columns-ssms.md). Di seguito sono riportate alcune informazioni specifiche degli enclave da tenere presenti:

- È necessario SSMS 18.3 o versione successiva.
- Assicurarsi di eseguire le query in una finestra di query che utilizza un enclave sicuro da una connessione con Always Encrypted e i calcoli dell'enclave abilitati. Per istruzioni dettagliate, vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md) e [Abilitazione e disabilitazione di Always Encrypted per una connessione di database](always-encrypted-query-columns-ssms.md#en-dis).

## <a name="next-steps"></a>Next Steps
- [Sviluppare applicazioni usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Vedere anche  
- [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Configurare la crittografia delle colonne sul posto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Creare e usare indici in colonne usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-create-use-indexes.md)

