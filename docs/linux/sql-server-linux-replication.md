---
title: Replica di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive la replica di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ccba701efd1b74076c0eccb083a66382e8ac74b1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805473"
---
# <a name="sql-server-replication-on-linux"></a>Replica di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce la replica di SQL Server per le istanze di SQL Server in Linux.

Configurare la replica in Linux con SQL Server Management Studio (SSMS) [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

Può far parte di un'istanza di SQL Server in qualsiasi ruolo replica:

* Server di pubblicazione
* Database di distribuzione
* Sottoscrittore

Uno schema di replica può combinarsi e corrispondere piattaforme del sistema operativo. Ad esempio, uno schema di replica può includere un'istanza di SQL Server in Linux per server di pubblicazione e server di distribuzione e sottoscrittori sono istanze di SQL Server in Windows, nonché di Linux.

Istanze di SQL Server in Linux possono partecipare a un tipo di replica.

* Transazionale
* Merge
* Snapshot

Per informazioni dettagliate sulla replica, vedere [documentazione di SQL Server replica](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Caratteristiche supportate

Per [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] sono supportate le funzionalità di replica seguenti:

* Replica snapshot
* Replica transazionale
* Replica di tipo merge
* Replica peer-to-Peer
* Replica con porte non predefinite <!--Add link to explanation-->
* Replica con l'autenticazione di AD
* Configurazioni di replica in Windows e Linux
* Aggiornamenti immediati per la replica transazionale

## <a name="limitations"></a>Limitazioni

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] non supporta le funzionalità seguenti:

* Sottoscrittori di aggiornamento immediato
* Pubblicazione Oracle

## <a name="next-steps"></a>Passaggi successivi

[Configurare la replica di SQL Server in Linux](sql-server-linux-replication-tutorial-tsql.md)

[Esempio: Configurare la replica di SQL Server in Linux](sql-server-linux-replication-configure.md)
