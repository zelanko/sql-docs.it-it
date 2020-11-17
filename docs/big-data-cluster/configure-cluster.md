---
title: Configurare il cluster
titleSuffix: Configure a SQL Server big data cluster
description: Panoramica della configurazione di un cluster Big Data di SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549990"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>Configurare un cluster Big Data di SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

È possibile configurare le proprietà per l'istanza master di SQL Server, Apache Spark e Apache Hadoop nel cluster Big Data di SQL Server 2019 in fase di distribuzione.

Dopo la distribuzione, i cluster Big Data non supportano la modifica delle proprietà di configurazione.

## <a name="configuration-scopes"></a>Ambiti di configurazione
La configurazione di cluster Big Data prevede due livelli di ambito: `service`e `resource`. Anche la gerarchia delle impostazioni segue in questo ordine, dal più alto al più basso. I componenti BDC accetteranno il valore dell'impostazione definito nell'ambito più basso. Se l'impostazione non è definita in un ambito specificato, erediterà il valore dall'ambito padre superiore.

Ad esempio, è possibile definire il numero predefinito di core che il driver Spark userà nel pool di archiviazione e Sparkhead `resources`. Questa operazione può essere eseguita in due modi: 
- Specificare un valore di core predefinito nell'ambito del servizio `Spark`  
- Specificare un valore di core predefinito nell'ambito della risorsa `storage-0` e `sparkhead`

Nel primo scenario tutte le risorse con ambito inferiore del servizio Spark (pool di archiviazione e Sparkhead) *ereditano* il numero predefinito di core dal valore predefinito del servizio Spark.

Nel secondo scenario ogni risorsa userà il valore definito nel rispettivo ambito.

Se il numero predefinito di core viene configurato sia nell'ambito del servizio sia in quello delle risorse, il valore con ambito risorsa eseguirà l'override del valore con ambito servizio, poiché si tratta dell'ambito **configurato dell'utente** più basso per l'impostazione specificata.

Per informazioni specifiche sulla configurazione, vedere gli articoli appropriati:

Procedura: 
- [Configurare l'istanza master di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)
- [Configurare Apache Spark e Apache Hadoop nei cluster Big Data](configure-spark-hdfs.md)

Riferimento: 
- [Proprietà di configurazione dell'istanza master di SQL Server](reference-config-master-instance.md)
- [Proprietà di configurazione di Apache Spark e Apache Hadoop (HDFS)](reference-config-spark-hadoop.md)
