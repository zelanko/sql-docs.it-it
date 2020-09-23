---
title: Che cos'è il pool di archiviazione?
titleSuffix: SQL Server big data clusters
description: Informazioni sul ruolo del pool di archiviazione di SQL Server in un cluster Big Data di SQL Server 2019 e sull'architettura e le funzionalità di un pool di archiviazione SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd7a38d555cbf6e2f64743f0907fbfbbdec4d41f
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87806467"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>Che cos'è il pool di archiviazione ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive il ruolo del *pool di archiviazione di SQL Server* in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di archiviazione SQL.

## <a name="storage-pool-architecture"></a>Architettura dei pool di archiviazione

Il pool di archiviazione è formato da nodi di archiviazione costituiti da SQL Server in Linux, Spark, and HDFS. Tutti i nodi di archiviazione in un cluster Big Data di SQL Server sono membri di un cluster HDFS.

![Architettura dei pool di archiviazione](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilità

I nodi di archiviazione sono responsabili delle attività seguenti:

- Inserimento di dati tramite Spark.
- Archiviazione dei dati in HDFS (formato parquet e testo delimitato). HDFS fornisce anche la persistenza dei dati, tenendo conto che i dati HDFS vengono distribuiti tra tutti i nodi di archiviazione del cluster Big Data di SQL Server.
- Accesso ai dati tramite gateway HDFS ed endpoint SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Architettura Microsoft dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
