---
title: Che cosa sono i pool di calcolo?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di calcolo in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6156d23fa55690224cd6df82e5f4bafe10e4d1ab
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653089"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>Che cosa sono i pool di calcolo in un cluster Big Data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo dei *pool di calcolo di SQL Server* in un cluster Big Data di SQL Server 2019 (anteprima). I pool di calcolo forniscono risorse di calcolo di scale-out per un cluster Big Data. Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di calcolo.

## <a name="compute-pool-architecture"></a>Architettura dei pool di calcolo

Un pool di calcolo è costituito da uno o più pod di calcolo in esecuzione in Kubernetes. Le operazioni automatiche di creazione e gestione di questi pod sono coordinate dall'[istanza master di SQL Server](concept-master-instance.md). Ogni pod contiene un set di servizi di base e un'istanza del motore di database di SQL Server.

## <a name="scale-out-groups"></a>Gruppi con scalabilità orizzontale

Un pool di calcolo può svolgere la funzione di un gruppo PolyBase di scale-out per query distribuite tra origini dati diverse, ad esempio HDFS, Oracle, MongoDB o Terradata. Usando pod di calcolo in Kubernetes, i cluster Big Data possono automatizzare la creazione e la configurazione di pod di calcolo per gruppi PolyBase di scale-out.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md)
- [Workshop: Architettura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
