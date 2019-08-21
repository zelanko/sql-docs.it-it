---
title: Che cos'è il controller?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il controller di un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 643cb2b4e252e1818940bda2be54917c23cefe06
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652281"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>Che cos'è il controller in un cluster Big Data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Il controller ospita la logica di base per la distribuzione e la gestione di un cluster Big Data. Si occupa di tutte le interazioni con Kubernetes, le istanze di SQL Server che fanno parte del cluster e altri componenti come HDFS e Spark.

Il servizio controller fornisce le funzionalità di base seguenti:

- Gestione del ciclo di vita del cluster: bootstrap del cluster ed eliminazione e aggiornamento delle configurazioni
- Gestione delle istanze master di SQL Server
- Gestione dei pool di calcolo, dati e archiviazione
- Esposizione degli strumenti di monitoraggio per osservare lo stato del cluster
- Esposizione degli strumenti di risoluzione dei problemi per rilevare e correggere problemi imprevisti
- Gestione della sicurezza del cluster:
  - Protezione degli endpoint del cluster
  - Gestione di utenti e ruoli
  - Configurazione delle credenziali per la comunicazione all'interno del cluster

## <a name="deploying-the-controller-service"></a>Distribuzione del servizio controller

Il controller viene distribuito e ospitato nello stesso spazio dei nomi Kubernetes in cui il cliente vuole compilare un cluster Big Data. Questo servizio viene installato da un amministratore di Kubernetes durante il bootstrap del cluster, usando l'utilità della riga di comando **azdata**. Per ulteriori informazioni, vedere [Introduzione a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deploy-get-started.md).

Il flusso di lavoro di implementazione disporrà su Kubernetes un cluster Big Data di SQL Server completamente funzionale che include tutti i componenti descritti nell'articolo [Panoramica](big-data-cluster-overview.md). Il flusso di lavoro di bootstrap crea innanzitutto il servizio controller che, una volta distribuito, coordina l'installazione e la configurazione della restante parte dei servizi dei pool master, di calcolo, di dati e di archiviazione.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gestione del cluster tramite il servizio controller

È possibile gestire il cluster tramite il servizio controller usando uno dei comandi **azdata**. Se si distribuiscono oggetti Kubernetes aggiuntivi, come i pod, nello stesso spazio dei nomi, questi non vengono gestiti o monitorati dal servizio controller. È anche possibile usare i comandi **kubectl** per gestire il cluster a livello di Kubernetes. Per ulteriori informazioni, vedere [monitoraggio e risoluzione [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]dei problemi ](cluster-troubleshooting-commands.md).

Il controller e gli oggetti Kubernetes (set con stato, pod, segreti e così via) creati per un cluster Big Data si trovano in uno spazio dei nomi Kubernetes dedicato. L'amministratore del cluster concederà al servizio controller l'autorizzazione Kubernetes per gestire tutte le risorse all'interno di questo spazio dei nomi.  Il criterio di controllo degli accessi in base al ruolo per questo scenario viene configurato automaticamente come parte della distribuzione iniziale del cluster tramite **azdata**.

### <a name="azdata"></a>azdata

**azdata** è un'utilità della riga di comando scritta in Python che permette agli amministratori del cluster di eseguire il bootstrap e la gestione di cluster Big Data tramite API REST esposte dal servizio controller.

## <a name="controller-service-security"></a>Sicurezza del servizio controller

Tutte le comunicazioni con il servizio controller avvengono tramite un'API REST su HTTPS. Un certificato autofirmato verrà generato automaticamente in fase di bootstrap. 

L'autenticazione all'endpoint del servizio controller si basa su nome utente e password. Queste credenziali vengono sottoposte a provisioning in fase di bootstrap del cluster usando l'input per le variabili di ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.

> [!NOTE]
> È necessario fornire una password conforme ai [requisiti di complessità delle password di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md)
- [Workshop: Architettura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
