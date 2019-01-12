---
title: Quali sono i pool di dati?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive il pool di dati in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c3df07da100bf0bbfc0b2238cb4154b4c3a363e3
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241612"
---
# <a name="what-are-data-pools-in-a-sql-server-2019-big-data-cluster"></a>Quali sono i pool di dati in un cluster di SQL Server 2019 big data?

Questo articolo descrive il ruolo del *pool di dati di SQL Server* in un cluster di big data di SQL Server 2019 (anteprima). Le sezioni seguenti descrivono l'architettura e la funzionalità di un pool di dati SQL.

## <a name="data-pool-architecture"></a>Architettura di pool di dati

Un pool di dati è costituito da uno o più istanze del pool di dati SQL Server. Istanze del pool di dati SQL forniscono un archivio permanente SQL Server per il cluster. Un pool di dati viene utilizzato per inserire i dati dalla query SQL o i processi Spark. Per garantire prestazioni migliori in grandi set di dati, i dati in un pool di dati viene distribuiti in partizioni tra le istanze del pool di dati SQL membro.

## <a name="scale-out-data-marts"></a>Scalabilità orizzontale data mart

I pool di dati consentono la creazione di tipo scale-out data mart, in cui i dati esterni da più origini vengono inseriti in pool di dati. Poiché i dati viene distribuiti in istanze del pool di dati, le query parallele sui dati curati sono più efficienti.

![Data mart di dati di tipo scale-out](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
