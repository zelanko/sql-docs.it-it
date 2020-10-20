---
title: Che cosa sono i pool di calcolo?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di calcolo di un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/15/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9c3374b0820233e20ee73b85947ed2b8a61847c0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866810"
---
# <a name="what-are-compute-pools-sql-server-big-data-clusters"></a>Che cosa sono i cluster Big Data di SQL Server con pool di calcolo?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive il ruolo dei *pool di calcolo di SQL Server* nei cluster Big Data di SQL Server. I pool di calcolo forniscono risorse di calcolo con scalabilità orizzontale per un cluster Big Data. Vengono usati per l'offload del lavoro di calcolo, o dei set di risultati intermedi, dall'istanza master di SQL Server. Le sezioni seguenti descrivono l'architettura, le funzionalità e gli scenari di utilizzo di un pool di calcolo.

È anche possibile guardare questo video di 5 minuti per un'introduzione ai pool di calcolo:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="compute-pool-architecture"></a>Architettura dei pool di calcolo

Un pool di calcolo è costituito da uno o più pod di calcolo in esecuzione in Kubernetes. Le operazioni automatiche di creazione e gestione di questi pod sono coordinate dall'[istanza master di SQL Server](concept-master-instance.md). Ogni pod contiene un set di servizi di base e un'istanza del motore di database di SQL Server.

![Architettura dei pool di calcolo](media/concept-compute-pool/compute-pool-architecture.png)

## <a name="scale-out-groups"></a>Gruppi con scalabilità orizzontale

Un pool di calcolo può svolgere la funzione di un gruppo con scalabilità orizzontale PolyBase per query distribuite tra origini dati esterne diverse, ad esempio SQL Server, Oracle, MongoDB, Teradata e HDFS. Usando pod di calcolo in Kubernetes, i cluster Big Data possono automatizzare la creazione e la configurazione di pod di calcolo per gruppi PolyBase con scalabilità orizzontale.

## <a name="compute-pool-scenarios"></a>Scenari di pool di calcolo

Il pool di calcolo viene usato nei seguenti scenari:

- Quando le query inviate all'istanza master usano una o più tabelle presenti nel [pool di archiviazione](concept-storage-pool.md).

- Quando le query inviate all'istanza master usano una o più tabelle con distribuzione round robin presenti nel [pool di archiviazione](concept-data-pool.md).

- Quando le query inviate all'istanza master usano tabelle **partizionate** con origini dati esterne di SQL Server, Oracle, MongoDB e Teradata. Per questo scenario, è necessario abilitare l'opzione relativa all'hint per la query (FORCE SCALEOUTEXECUTION).

- Quando le query inviate all'istanza master usano una o più tabelle presenti nella [suddivisione in livelli HDFS](hdfs-tiering.md).

Il pool di calcolo **non** viene usato nei seguenti scenari:

- Quando le query inviate all'istanza master usano una o più tabelle presenti in un cluster Hadoop HDFS esterno.

- Quando le query inviate all'istanza master usano una o più tabelle presenti in Archiviazione BLOB di Azure.

- Quando le query inviate all'istanza master usano tabelle **non partizionate** con origini dati esterne di SQL Server, Oracle, MongoDB e Teradata.

- Quando l'opzione relativa all'hint per la query (DISABLE SCALEOUTEXECUTION) è abilitata.

- Quando le query inviate all'istanza master si applicano ai database presenti nell'istanza master.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Architettura Microsoft dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
