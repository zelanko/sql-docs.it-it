---
title: Configurare e usare Always Encrypted con enclave sicuri | Microsoft Docs
description: Informazioni su come configurare e usare Always Encrypted con enclave sicuri in SQL Server per ottenere funzionalità avanzate sui dati sensibili.
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
ms.openlocfilehash: d73d337e750e287066531017710b733c92a312ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627028"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configurare e usare Always Encrypted con enclave sicuri 

[!INCLUDE[SQL Server 2019](../../../includes/applies-to-version/sqlserver2019.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) estende la funzionalità [Always Encrypted](always-encrypted-database-engine.md) esistente per abilitare funzionalità più avanzate per i dati sensibili, mantenendo i dati riservati. Questo articolo elenca le attività comuni per la configurazione e l'uso della funzionalità.

Per un'esercitazione che illustra come iniziare rapidamente a usare Always Encrypted con enclave sicuri, vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Configurare l'ambiente per supportare gli enclave e l'attestazione
Per informazioni dettagliate, vedere gli articoli seguenti:
- [Pianificare l'attestazione del servizio Sorveglianza host](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [Distribuire il servizio Sorveglianza host per [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [Registrare il computer per il servizio Sorveglianza host](./always-encrypted-enclaves-host-guardian-service-register.md)

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
