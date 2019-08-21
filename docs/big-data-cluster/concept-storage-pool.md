---
title: Che cos'è il pool di archiviazione?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di archiviazione di un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ead6c2ceeecbdfb3466bd4475978b139a0d2ddde
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652240"
---
# <a name="what-is-the-storage-pool-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Che cos'è il pool di[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]archiviazione ()?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo del *pool di archiviazione SQL Server* in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di archiviazione SQL.

## <a name="storage-pool-architecture"></a>Architettura dei pool di archiviazione

Il pool di archiviazione è formato da nodi di archiviazione costituiti da SQL Server in Linux, Spark, and HDFS. Tutti i nodi di archiviazione in un cluster Big Data di SQL Server sono membri di un cluster HDFS.

![Architettura dei pool di archiviazione](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilità

I nodi di archiviazione sono responsabili delle attività seguenti:

- Inserimento di dati tramite Spark.
- Archiviazione dei dati in HDFS (formato parquet). HDFS fornisce anche la persistenza dei dati, tenendo conto che i dati HDFS vengono distribuiti tra tutti i nodi di archiviazione del cluster Big Data di SQL Server.
- Accesso ai dati tramite gateway HDFS ed endpoint SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md)
- [Workshop: Architettura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
