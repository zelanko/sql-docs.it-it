---
title: Che cosa sono i pool di calcolo?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il pool di calcolo di un cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d9ae112369ddad91bec125ec19713040a5aae915
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958803"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>Che cosa sono i pool di calcolo in un cluster Big Data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive il ruolo dei *pool di calcolo di SQL Server* in un cluster Big Data di SQL Server 2019 (anteprima). I pool di calcolo forniscono risorse di calcolo di scale-out per un cluster Big Data. Le sezioni seguenti descrivono l'architettura e le funzionalità di un pool di calcolo.

## <a name="compute-pool-architecture"></a>Architettura dei pool di calcolo

Un pool di calcolo è costituito da uno o più pod di calcolo in esecuzione in Kubernetes. Le operazioni automatiche di creazione e gestione di questi pod sono coordinate dall'[istanza master di SQL Server](concept-master-instance.md). Ogni pod contiene un set di servizi di base e un'istanza del motore di database di SQL Server.

## <a name="scale-out-groups"></a>Gruppi con scalabilità orizzontale

Un pool di calcolo può svolgere la funzione di un gruppo PolyBase di scale-out per query distribuite tra origini dati diverse, ad esempio HDFS, Oracle, MongoDB o Terradata. Usando pod di calcolo in Kubernetes, i cluster Big Data possono automatizzare la creazione e la configurazione di pod di calcolo per gruppi PolyBase di scale-out.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere le risorse seguenti:

- [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Architettura dei cluster Big Data di Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
