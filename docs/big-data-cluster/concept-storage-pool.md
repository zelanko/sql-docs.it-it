---
title: Che cos'è il pool di archiviazione?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive il pool di archiviazione in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c89ddc5d155af4542b5101e9a6e394effc5d9fd3
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241522"
---
# <a name="what-is-the-storage-pool-sql-server-2019-big-data-clusters"></a>Che cos'è il pool di archiviazione (cluster di SQL Server 2019 dei big Data)?

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

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
