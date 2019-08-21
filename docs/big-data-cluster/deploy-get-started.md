---
title: Attività iniziali
titleSuffix: SQL Server big data clusters
description: Informazioni sui passaggi e sulle risorse per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] la distribuzione (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 323394f9590551528ce9e9dfdf1fb97c7d1c2225
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653397"
---
# <a name="get-started-with-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Introduzione a[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce una panoramica della distribuzione [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)di. È stato ideato per offrire i concetti principali e un quadro generale per la comprensione degli altri articoli sulla distribuzione inclusi in questa sezione. I passaggi di distribuzione specifici variano in base alla piattaforma scelta per il client e il server.

> [!TIP]
> Per ottenere rapidamente un ambiente con Kubernetes e Big Data cluster distribuiti per semplificare le proprie funzionalità, usare uno degli script di esempio a cui si fa riferimento nella [sezione Scripts](#scripts). Dopo la distribuzione, per gestire il cluster usare gli [strumenti client](#tools) nella sezione seguente.

## <a id="tools"></a> Strumenti client

I cluster Big data richiedono un set specifico di strumenti client. Prima di distribuire un cluster Big Data in Kubernetes, è necessario installare gli strumenti seguenti:

| Strumento | Descrizione |
|---|---|
| **azdata** | Distribuisce e gestisce cluster Big Data. |
| **kubectl** | Crea e gestisce il cluster Kubernetes sottostante. |
| **Azure Data Studio** | Interfaccia grafica per l'uso del cluster Big Data. |
| **Estensione di SQL Server 2019** | Estensione di Azure Data Studio che abilita le funzionalità dei cluster Big Data. |

Per scenari diversi sono necessari altri strumenti. Ogni articolo descriverà gli strumenti necessari come prerequisiti per l'esecuzione di un'attività specifica. Per un elenco completo degli strumenti e dei collegamenti di installazione, vedere [Installare strumenti per Big Data di SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

I cluster Big Data vengono distribuiti come serie di contenitori intercorrelati gestiti in [Kubernetes](https://kubernetes.io/docs/home). È possibile ospitare Kubernetes in diversi modi. Anche se esiste già un ambiente Kubernetes, è necessario esaminare i requisiti correlati per i cluster Big Data.

- **Servizio Azure Kubernetes**: il servizio Azure Kubernetes permette di distribuire un cluster Kubernetes gestito in Azure. È possibile gestire solo i nodi agente. Con il servizio Azure Kubernetes non è necessario effettuare il provisioning del proprio hardware per il cluster. È facile usare anche uno [script Python](quickstart-big-data-cluster-deploy.md) o un [notebook di distribuzione](deploy-notebooks.md) per creare il cluster del servizio Azure Kubernetes e distribuire il cluster Big Data in un unico passaggio. Per altre informazioni sulla configurazione di AKS per una distribuzione Big Data cluster, vedere [configurare il servizio Azure [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Kubernetes per](deploy-on-aks.md)le distribuzioni.

- **Più computer**: è possibile distribuire Kubernetes anche in più computer Linux, che possono essere server fisici o macchine virtuali. È possibile usare lo strumento [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) per creare il cluster Kubernetes. È possibile usare uno [script Bash](deployment-script-single-node-kubeadm.md) per automatizzare questo tipo di distribuzione. Questo metodo funziona correttamente se è già presente un'infrastruttura che si vuole usare per il cluster Big Data. Per altre informazioni sull'uso di distribuzioni di **kubeadm** con Big Data cluster, vedere [configurare Kubernetes in più computer [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] per](deploy-with-kubeadm.md)le distribuzioni.

- **minikube**: minikube permette di eseguire Kubernetes in locale in un unico server. Si tratta di un'opzione utile per provare i cluster Big Data o se è necessario usarli in uno scenario di test o sviluppo. Per altre informazioni sull'uso di minikube, vedere la [documentazione di minikube](https://kubernetes.io/docs/setup/minikube/). Per requisiti specifici per l'uso di minikube con cluster Big Data, vedere [Configurare minikube per le distribuzioni di cluster Big Data di SQL Server 2019](deploy-on-minikube.md).

## <a name="deploy-a-big-data-cluster"></a>Distribuire un cluster Big Data

Dopo aver configurato Kubernetes, è possibile distribuire un cluster Big Data con il comando `azdata bdc create`. Per la distribuzione è possibile adottare diversi approcci.

- Se si esegue la distribuzione in un ambiente di sviluppo e test, è possibile scegliere di usare una delle [configurazioni predefinite](deployment-guidance.md#deploy) fornite da **azdata**.

- Per personalizzare la distribuzione, è possibile creare e usare [file di configurazione della distribuzione](deployment-guidance.md#configfile) propri.

- Per un'installazione completamente automatica, è possibile passare tutte le altre impostazioni in variabili di ambiente. Per altre informazioni, vedere [Distribuzioni automatiche](deployment-guidance.md#unattended).


## <a id="scripts"></a>Script di distribuzione

Gli script di distribuzione permettono di distribuire cluster Kubernetes e Big Data in un unico passaggio. Spesso forniscono anche valori predefiniti per le impostazioni dei cluster Big Data. È possibile personalizzare qualsiasi script di distribuzione creando la propria versione, per configurare la distribuzione del cluster Big Data in modo diverso.

Attualmente sono disponibili gli script di distribuzione seguenti:

- [Script Python: distribuire un cluster Big Data nel servizio Azure Kubernetes](quickstart-big-data-cluster-deploy.md)
- [Script Bash: distribuire un cluster Big Data in un cluster kubeadm a nodo singolo](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>Notebook di distribuzione

È possibile distribuire un cluster Big Data anche eseguendo un notebook di Azure Data Studio. Per altre informazioni su come usare un notebook per la distribuzione nel servizio Azure Kubernetes, vedere l'articolo seguente:

- [Distribuire un cluster Big Data con notebook di Azure Data Studio](deploy-notebooks.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito correttamente un cluster Big Data, [connettersi al cluster](connect-to-big-data-cluster.md) e valutare se [caricare dati di esempio](tutorial-load-sample-data.md) da usare con diverse procedure dettagliate.
