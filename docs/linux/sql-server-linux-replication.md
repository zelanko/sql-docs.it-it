---
title: Replica di SQL Server in Linux
description: Questo articolo descrive la replica di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b049866d9752485cb1b9eb609404a3bd86f28a41
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065187"
---
# <a name="sql-server-replication-on-linux"></a>Replica di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce la replica di SQL Server per le istanze di SQL Server in Linux.

Configurare la replica in Linux con le [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md) di SQL Server Management Studio (SSMS).

Un'istanza di SQL Server può far parte di qualsiasi ruolo di replica:

* Server di pubblicazione
* Database di distribuzione
* Sottoscrittore

Uno schema di replica può combinare diverse piattaforme di sistema operativo. Uno schema di replica può ad esempio includere un'istanza di SQL Server in Linux per il server di pubblicazione e il database di distribuzione e i sottoscrittori possono includere istanze di SQL Server in Windows e in Linux.

Le istanze di SQL Server in Linux possono far parte di qualsiasi tipo di replica.

* Transazionale
* Merge
* Snapshot

Per informazioni dettagliate sulla replica, vedere la [documentazione della replica di SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Caratteristiche supportate

Per [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] sono supportate le funzionalità di replica seguenti:

* Replica snapshot
* Replica transazionale
* Replica di tipo merge
* Replica peer-to-peer
* Replica con porte non predefinite <!--Add link to explanation-->
* Replica con autenticazione AD
* Configurazioni di replica in Windows e Linux
* Aggiornamenti immediati per la replica transazionale

## <a name="limitations"></a>Limitazioni

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] non supporta le funzionalità seguenti:

* Sottoscrittori di aggiornamenti immediati
* Pubblicazione Oracle

## <a name="next-steps"></a>Passaggi successivi

[Configurare la replica di SQL Server in Linux](sql-server-linux-replication-tutorial-tsql.md)

[Esempio: configurare la replica di SQL Server in Linux](sql-server-linux-replication-configure.md)
