---
title: Quali sono i pool di dati?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di dati in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ba296a504ae4a6656941c408e7b7a0c96a83c97d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783092"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>Quali sono i pool di dati in un cluster di big data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo del *pool di dati di SQL Server* in un cluster di big data di SQL Server 2019 (anteprima). Le sezioni seguenti descrivono l'architettura e la funzionalità di un pool di dati SQL.

## <a name="data-pool-architecture"></a>Architettura di pool di dati

Un pool di dati è costituito da uno o più istanze del pool di dati SQL Server. Istanze del pool di dati SQL forniscono un archivio permanente SQL Server per il cluster. Un pool di dati viene utilizzato per inserire i dati dalla query SQL o i processi Spark. Per garantire prestazioni migliori in grandi set di dati, i dati in un pool di dati viene distribuiti in partizioni tra le istanze del pool di dati SQL membro.

## <a name="scale-out-data-marts"></a>Scalabilità orizzontale data mart

I pool di dati consentono la creazione di tipo scale-out data mart, in cui i dati esterni da più origini vengono inseriti in pool di dati. Poiché i dati viene distribuiti in istanze del pool di dati, le query parallele sui dati curati sono più efficienti.

![Data mart di dati di tipo scale-out](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere le risorse seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
