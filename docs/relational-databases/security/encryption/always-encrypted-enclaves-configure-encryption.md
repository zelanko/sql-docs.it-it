---
title: Configurare la crittografia delle colonne sul posto usando Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d887e428773e6901544422edcb6960e6e9ae0580
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595516"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>Configurare la crittografia delle colonne sul posto usando Always Encrypted con enclave sicuri 
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) supporta le operazioni crittografiche sulle colonne di database sul posto, all'interno di un enclave sicuro in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La crittografia sul posto elimina la necessità di spostare i dati per tali operazioni all'esterno del database, rendendo le operazioni di crittografia più veloci e affidabili. 

> [!NOTE]
> Nonostante i vantaggi della crittografia sul posto a livello di prestazioni, le operazioni di crittografia su tabelle di grandi dimensioni possono richiedere molto tempo e utilizzare un numero significativo di risorse, influendo in modo potenzialmente negativo sulle prestazioni e sulla disponibilità delle applicazioni.

La crittografia sul posto consente anche di attivare operazioni di crittografia usando l'istruzione [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md), impossibile da eseguire senza enclave.

## <a name="prerequisites"></a>Prerequisites
Le operazioni di crittografia supportate e i requisiti per le chiavi di crittografia di colonna, usati per le operazioni, sono:
- Crittografia di una colonna di testo non crittografato. La chiave di crittografia di colonna usata per crittografare la colonna deve essere abilitata per l'enclave.
- Nuova crittografia di una colonna crittografata usando un nuovo tipo di crittografia e/o una nuova chiave di crittografia di colonna. Sia la chiave di crittografia di colonna corrente che la nuova chiave di crittografia di colonna (se diversa da quella corrente) devono essere abilitate per l'enclave.
- Decrittografia di una colonna crittografata: la chiave di crittografia di colonna, che protegge la colonna, deve essere abilitata per l'enclave.

Per informazioni su come assicurarsi che le chiavi di crittografia di colonna siano abilitate per l'enclave, vedere [Gestire le chiavi per Always Encrypted con enclave sicuri](always-encrypted-enclaves-manage-keys.md).

La crittografia sul posto richiede anche un'istanza di SQL Server con un enclave sicuro inizializzato correttamente. Vedere [Configurare il tipo di enclave per l'opzione di configurazione del server Always Encrypted](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md).

Un utente o un'applicazione che attiva operazioni di crittografia deve avere le autorizzazioni per apportare modifiche allo schema nella tabella contenente le colonne interessate e per accedere alle chiavi master delle colonne coinvolte nelle operazioni e ai metadati delle chiavi pertinenti nel database.

È possibile attivare la crittografia sul posto solo usando [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) da SQL Server Management Studio o dall'applicazione personalizzata. Vedere [Configurare la crittografia delle colonne sul posto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md).

> [!NOTE]
> La [procedura guidata Always Encrypted](always-encrypted-wizard.md) e il cmdlet [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/module/sqlserver/set-sqlcolumnencryption) non supportano attualmente la crittografia sul posto e scaricano sempre i dati per le operazioni di crittografia, anche se la configurazione soddisfa i requisiti precedenti. 

## <a name="next-steps"></a>Next Steps
- [Configurare la crittografia delle colonne sul posto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Creare e usare indici in una colonna usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-create-use-indexes.md)
- [Sviluppare applicazioni usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-client-development.md)
