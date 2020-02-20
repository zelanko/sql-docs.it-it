---
title: Che cosa sono i pool di dati?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di dati di un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6fdcaf7e54455d40cd3bcdb8c6ec1a1ec3bf75f7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253128"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>Che cosa sono i pool di dati in un cluster Big Data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

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
