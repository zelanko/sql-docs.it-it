---
title: Configurare e usare Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: bda4d41d4f2a9c92dca2d41b959ad4c4b32a1c79
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594470"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configurare e usare Always Encrypted con enclave sicuri 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) estende la funzionalità [Always Encrypted](always-encrypted-database-engine.md) esistente per abilitare funzionalità più avanzate per i dati sensibili, mantenendo i dati riservati. Questo articolo elenca le attività comuni per la configurazione e l'uso della funzionalità.

Per un'esercitazione che illustra come iniziare rapidamente a usare Always Encrypted con enclave sicuri, vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Configurare l'ambiente per supportare gli enclave e l'attestazione
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Configurazione del servizio Sorveglianza host per Always Encrypted in SQL Server](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server).

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gestire le chiavi per Always Encrypted con enclave sicuri
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Gestire le chiavi per Always Encrypted con enclave sicuri - Panoramica](always-encrypted-enclaves-manage-keys.md)
- [Effettuare il provisioning delle chiavi abilitate per l'enclave](always-encrypted-enclaves-provision-keys.md)
- [Ruotare le chiavi abilitate per l'enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>Configurare le colonne con Always Encrypted con enclave sicuri
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Configurare la crittografia delle colonne sul posto usando Always Encrypted con enclave sicuri - Panoramica](always-encrypted-enclaves-configure-encryption.md)
- [Configurare la crittografia delle colonne sul posto con Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Abilitare Always Encrypted con enclave sicuri per le colonne crittografate esistenti](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> Per un'esercitazione dettagliata su come configurare l'ambiente di test e provare le funzionalità di Always Encrypted con enclave sicuri in SSMS, vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Eseguire query delle colonne usando Always Encrypted con enclave sicuri
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Eseguire query delle colonne usando Always Encrypted con enclave sicuri - Panoramica](always-encrypted-enclaves-query-columns.md)
- [Eseguire query delle colonne usando Always Encrypted con enclave sicuri con SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Creare e usare indici sulle colonne abilitate per l'enclave
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Creare e usare indici in colonne usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Sviluppare applicazioni usando Always Encrypted con enclave sicuri
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Sviluppare applicazioni usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-client-development.md)
