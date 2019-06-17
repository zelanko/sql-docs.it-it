---
title: Che cos'è il pool di archiviazione?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di archiviazione in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7ff8b16ec5f1ea0d1df401cee9657eb8d564863a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782991"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>Che cos'è il pool di archiviazione (cluster di big data di SQL Server)?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo del *pool di archiviazione di SQL Server* in un cluster di big data di SQL Server 2019 (anteprima). Le sezioni seguenti descrivono l'architettura e la funzionalità di un pool di archiviazione SQL.

## <a name="storage-pool-architecture"></a>Architettura del pool di archiviazione

Il pool di archiviazione è costituito da archiviazione di nodi è costituiti da SQL Server in Linux, Spark e HDFS. Tutti i nodi di archiviazione in un cluster di big data SQL sono membri di un cluster HDFS.

![Architettura del pool di archiviazione](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilità

I nodi di archiviazione sono responsabili per:

- Inserimento dei dati tramite Spark.
- Archiviazione dei dati in HDFS (formato Parquet). HDFS offre anche la persistenza dei dati, come i dati HDFS sono distribuiti in tutti i nodi di archiviazione del cluster di big data SQL.
- Accesso ai dati tramite gli endpoint HDFS e SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere le risorse seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
