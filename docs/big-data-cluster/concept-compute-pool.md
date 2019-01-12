---
title: Quali sono i pool di calcolo?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive il pool di calcolo in un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: d1e028781735b257b82f839571da5400c36c1e10
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241952"
---
# <a name="what-are-compute-pools-in-a-sql-server-2019-big-data-cluster"></a>Quali sono i pool di calcolo in un cluster di SQL Server 2019 big data?

Questo articolo descrive il ruolo del *pool di calcolo di SQL Server* in un cluster di big data anteprima di SQL Server 2019. I pool di calcolo offrono le risorse di calcolo a scalabilità orizzontale per un cluster di big data. Le sezioni seguenti descrivono l'architettura e la funzionalità di un pool di calcolo.

## <a name="compute-pool-architecture"></a>Architettura del pool di calcolo

Un pool di calcolo è costituito da uno o più POD in esecuzione in Kubernetes di calcolo. La creazione automatica e la gestione di questi POD è coordinata dal [istanza master di SQL Server](concept-master-instance.md). Ogni pod contiene un set di servizi di base e un'istanza del motore di database di SQL Server.

> [!NOTE]
> CTP 2.2 supporta solo un pool di calcolo singolo per ogni cluster.

## <a name="scale-out-groups"></a>Gruppi con scalabilità orizzontale

Un pool di calcolo può fungere da un gruppo con scalabilità orizzontale PolyBase per le query distribuite su origini dati differenti, ad esempio HDFS, Oracle, MongoDB o Terradata. Usando i POD di calcolo in Kubernetes, è possono automatizzare i cluster di big data creazione e configurazione di calcolo POD per gruppi con scalabilità orizzontale di PolyBase.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
