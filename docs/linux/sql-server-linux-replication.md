---
title: Replica di SQL Server in Linux
description: Questo articolo descrive la replica di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: cdd37963a419b33bb84353dee98c928179473bcb
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882647"
---
# <a name="sql-server-replication-on-linux"></a>Replica di SQL Server in Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) e versioni successive supportano la replica di SQL Server per le istanze di SQL Server in Linux.

Configurare la replica in Linux con le [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md) di SQL Server Management Studio (SSMS).

Un'istanza di SQL Server può far parte di qualsiasi ruolo di replica:

* Editore
* Database di distribuzione
* Sottoscrittore

Uno schema di replica può combinare diverse piattaforme di sistema operativo. Uno schema di replica può ad esempio includere un'istanza di SQL Server in Linux per il server di pubblicazione e il database di distribuzione e i sottoscrittori possono includere istanze di SQL Server in Windows e in Linux.

Le istanze di SQL Server in Linux possono far parte di qualsiasi tipo di replica.

* Transazionale
* Snapshot

Per informazioni dettagliate sulla replica, vedere la [documentazione della replica di SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Caratteristiche supportate

Sono supportate le funzionalità di replica seguenti:

* Replica snapshot
* Replica transazionale
* Replica con porte non predefinite <!--Add link to explanation-->
* Replica con autenticazione AD
* Configurazioni di replica in Windows e Linux
* Aggiornamenti immediati per la replica transazionale

## <a name="limitations"></a>Limitazioni

Le funzionalità seguenti non sono supportate:

* Replica di tipo merge
* Replica peer-to-peer
* Pubblicazione Oracle

## <a name="next-steps"></a>Passaggi successivi

[Configurare la replica di SQL Server in Linux](sql-server-linux-replication-tutorial-tsql.md)

[Esempio: configurare la replica di SQL Server in Linux](sql-server-linux-replication-configure.md)
