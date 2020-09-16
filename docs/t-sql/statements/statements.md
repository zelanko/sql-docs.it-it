---
description: istruzioni Transact-SQL
title: Istruzioni | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c89cfff4f1477503650ab8f20ceb636636fb333f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540569"
---
# <a name="transact-sql-statements"></a>istruzioni Transact-SQL

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Un'istruzione SQL è un'unità di lavoro atomica che ha esito completamente positivo o negativo. Un'istruzione SQL è un set di istruzioni costituito da identificatori, parametri, variabili, nomi, tipi di dati e parole riservate SQL che eseguono la compilazione correttamente. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea una transazione *implicita* per un'istruzione SQL se un comando `BeginTransaction` non specifica l'inizio di una transazione. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue sempre il commit di una transazione implicita se l'istruzione riesce e ne esegue il rollback se il comando non riesce.  

Sono disponibili molti tipi di istruzioni. La più importante è probabilmente [SELECT](../queries/select-transact-sql.md), che recupera righe dal database e consente la selezione di una o più righe o colonne da una o più tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo articolo riepiloga le categorie di istruzioni da usare con Transact-SQL (T-SQL) in aggiunta all'istruzione `SELECT`. L'elenco completo delle istruzioni è visualizzato nell'area di navigazione a sinistra.

## <a name="backup-and-restore"></a>Backup e ripristino

Le istruzioni backup e ripristino consentono di creare backup e di eseguire il ripristino dai backup.  Per altre informazioni, vedere [Backup and restore overview](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) (Panoramica su backup e ripristino).

## <a name="data-definition-language"></a>Data Definition Language

Le istruzioni DDL (Data Definition Language) definiscono le strutture dei dati. Usare queste istruzioni per creare, modificare o eliminare le strutture dei dati in un database. Le istruzioni includono:

- ALTER
- Regole di confronto
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>Data Manipulation Language

Le istruzioni Data Manipulation Language (DML) hanno effetto sulle informazioni archiviate nel database. Usare queste istruzioni per inserire, aggiornare e modificare le righe nel database.

- BULK INSERT
- DELETE
- INSERT
- SELECT
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Istruzioni di autorizzazioni

Le istruzioni di autorizzazioni determinano quali utenti e account di accesso possono accedere ai dati ed eseguire operazioni. Per altre informazioni sull'autenticazione e l'accesso, vedere [Centro sicurezza](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Istruzioni di Service Broker

Service Broker è una funzionalità che offre supporto nativo per le applicazioni di messaggistica e accodamento. Per altre informazioni, vedere [Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md).

## <a name="session-settings"></a>Impostazioni sessione

Le istruzioni SET determinano come la sessione corrente gestisce le impsotazioni di runtime. Per una panoramica, vedere [Istruzioni SET](set-statements-transact-sql.md).
