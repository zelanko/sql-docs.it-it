---
title: Database in memoria | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994999"
---
# <a name="in-memory-database"></a>Database in memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Database in memoria è un termine generico per le funzionalità in SQL Server che consentono di sfruttare le tecnologie basate sulla memoria. Questa pagina continuerà a essere aggiornata a mano a mano che verranno sviluppate nuove funzionalità basate sulla memoria.

## <a name="hybrid-buffer-pool"></a>Pool di buffer ibrido

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il [pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md) consente al motore di database di accedere direttamente alle pagine di dati nei file di database archiviati nei dispositivi con memoria persistente.

## <a name="memory-optimized-tempdb-metadata"></a>Metadati tempdb ottimizzati per la memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce una nuova funzionalità, ovvero i [metadati tempdb ottimizzati per la memoria](./databases/tempdb-database.md#memory-optimized-tempdb-metadata) che rimuove in modo efficace i colli di bottiglia dovuti alla contesa e sblocca un nuovo livello di scalabilità per i carichi di lavoro tempdb elevati.

## <a name="in-memory-oltp"></a>OLTP in memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[OLTP in memoria](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) è la principale tecnologia disponibile in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../includes/sssds-md.md)] per ottimizzare le prestazioni di elaborazione delle transazioni, l'inserimento di dati, il caricamento di dati e gli scenari di dati temporanei.

**Si applica a:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="persistent-memory-support-for-linux"></a>Supporto della memoria persistente per Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] aggiunge il supporto per i dispositivi con memoria persistente per Linux, offrendo il riconoscimento completo dei file di dati e dei log delle transazioni all'interno della [memoria persistente](../linux/sql-server-linux-configure-pmem.md).

**Si applica a:** [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
