---
title: Che cosa sono i pool di dati?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di dati di un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f9355508e4d32dd9a6152781fba325ded2fa7425
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958731"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>Che cosa sono i pool di dati in un cluster Big Data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo dei *pool di dati di SQL Server* in un cluster Big Data di SQL Server 2019 (anteprima). Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di dati SQL.

## <a name="data-pool-architecture"></a>Architettura dei pool di dati

Un pool di dati è costituito da una o più istanze di pool di dati SQL Server. Le istanze di pool di dati SQL forniscono uno spazio di archiviazione SQL Server permanente per il cluster. I pool di dati vengono usati anche per inserire dati da query SQL o processi Spark. Per garantire prestazioni migliori anche a set di dati di grandi dimensioni, i dati di un pool di dati vengono distribuiti in partizioni tra le istanze dei pool di dati SQL dei membri.

## <a name="scale-out-data-marts"></a>Data mart con scalabilità orizzontale

I pool di dati consentono la creazione di data mart con scalabilità orizzontale, in cui nel pool di dati vengono inseriti i dati esterni provenienti da più origini. I dati vengono distribuiti tra le istanze dei pool di dati e le query parallele sui dati curati risultano quindi più efficienti.

![Data mart con scalabilità orizzontale](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere le risorse seguenti:

- [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Architettura dei cluster Big Data di Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
