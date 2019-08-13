---
title: Che cos'è il pool di archiviazione?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di archiviazione di un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 58e6f16a088d6dc6c1fc6bd32297e7bd698acbbf
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958653"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>Che cos'è il pool di archiviazione (cluster Big Data di SQL Server)?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo dei *pool di archiviazione di SQL Server* in un cluster Big Data di SQL Server 2019 (anteprima). Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di archiviazione SQL.

## <a name="storage-pool-architecture"></a>Architettura dei pool di archiviazione

Il pool di archiviazione è formato da nodi di archiviazione costituiti da SQL Server in Linux, Spark, and HDFS. Tutti i nodi di archiviazione in un cluster Big Data di SQL Server sono membri di un cluster HDFS.

![Architettura dei pool di archiviazione](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilità

I nodi di archiviazione sono responsabili delle attività seguenti:

- Inserimento di dati tramite Spark.
- Archiviazione dei dati in HDFS (formato parquet). HDFS fornisce anche la persistenza dei dati, tenendo conto che i dati HDFS vengono distribuiti tra tutti i nodi di archiviazione del cluster Big Data di SQL Server.
- Accesso ai dati tramite gateway HDFS ed endpoint SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere le risorse seguenti:

- [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Architettura dei cluster Big Data di Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
