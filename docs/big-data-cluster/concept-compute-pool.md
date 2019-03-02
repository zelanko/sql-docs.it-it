---
title: Quali sono i pool di calcolo?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive il pool di calcolo in un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 272f10cfed8f7cd1b07633b81642323a8c74b6d7
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227133"
---
# <a name="what-are-compute-pools-in-a-sql-server-2019-big-data-cluster"></a>Quali sono i pool di calcolo in un cluster di SQL Server 2019 big data?

Questo articolo descrive il ruolo del *pool di calcolo di SQL Server* in un cluster di big data anteprima di SQL Server 2019. I pool di calcolo offrono le risorse di calcolo a scalabilità orizzontale per un cluster di big data. Le sezioni seguenti descrivono l'architettura e la funzionalità di un pool di calcolo.

## <a name="compute-pool-architecture"></a>Architettura del pool di calcolo

Un pool di calcolo è costituito da uno o più POD in esecuzione in Kubernetes di calcolo. La creazione automatica e la gestione di questi POD è coordinata dal [istanza master di SQL Server](concept-master-instance.md). Ogni pod contiene un set di servizi di base e un'istanza del motore di database di SQL Server.

## <a name="scale-out-groups"></a>Gruppi con scalabilità orizzontale

Un pool di calcolo può fungere da un gruppo con scalabilità orizzontale PolyBase per le query distribuite su origini dati differenti, ad esempio HDFS, Oracle, MongoDB o Terradata. Usando i POD di calcolo in Kubernetes, è possono automatizzare i cluster di big data creazione e configurazione di calcolo POD per gruppi con scalabilità orizzontale di PolyBase.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
