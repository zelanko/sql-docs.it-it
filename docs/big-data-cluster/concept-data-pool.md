---
title: Che cosa sono i pool di dati?
titleSuffix: SQL Server big data clusters
description: Informazioni sul ruolo del pool di dati di SQL Server in un cluster Big Data di SQL Server e sull'architettura e sulle funzionalità di un pool di dati SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d9eaba636c2567d60dfc62ce37080717e9c32e9
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680576"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>Che cosa sono i pool di dati in un cluster Big Data di SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive il ruolo dei *pool di dati di SQL Server* in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di dati SQL.

Questo video di 5 minuti introduce i pool di dati e mostra come eseguire query sui dati dai pool di dati:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>Architettura dei pool di dati

Un pool di dati è costituito da una o più istanze di pool di dati SQL Server. Le istanze di pool di dati SQL forniscono uno spazio di archiviazione SQL Server permanente per il cluster. I pool di dati vengono usati anche per inserire dati da query SQL o processi Spark. Per garantire prestazioni migliori anche a set di dati di grandi dimensioni, i dati di un pool di dati vengono distribuiti in partizioni tra le istanze dei pool di dati SQL dei membri.

## <a name="scale-out-data-marts"></a>Data mart con scalabilità orizzontale

I pool di dati consentono la creazione di data mart con scalabilità orizzontale, in cui nel pool di dati vengono inseriti i dati esterni provenienti da più origini. I dati vengono distribuiti tra le istanze dei pool di dati e le query parallele sui dati curati risultano quindi più efficienti.

![Data mart con scalabilità orizzontale](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Architettura Microsoft dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
