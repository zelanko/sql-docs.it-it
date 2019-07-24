---
title: Attività iniziali
titleSuffix: SQL Server big data clusters
description: Informazioni sui passaggi e sulle risorse per la distribuzione di SQL Server cluster 2019 Big Data (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 41dd39c7aa613083f8ff47824ed6238b6f3c61b9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419430"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>Introduzione ai cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce una panoramica della distribuzione di un [cluster SQL Server 2019 Big Data (anteprima)](big-data-cluster-overview.md). È concepito per orientarsi ai concetti e fornire un Framework per comprendere gli altri articoli sulla distribuzione in questa sezione. I passaggi di distribuzione specifici variano in base alle scelte della piattaforma per il client e il server.

## <a id="tools"></a>Strumenti client

I cluster di Big data richiedono un set specifico di strumenti client. Prima di distribuire un cluster Big Data in Kubernetes, è necessario installare gli strumenti seguenti:

| Strumento | Descrizione |
|---|---|
| **azdata** | Distribuisce e gestisce i cluster Big Data. |
| **kubectl** | Crea e gestisce il cluster Kubernetes sottostante. |
| **Azure Data Studio** | Interfaccia grafica per l'uso del cluster Big Data. |
| **Estensione SQL Server 2019** | Azure Data Studio estensione che Abilita Big Data le funzionalità del cluster. |

Per diversi scenari sono necessari altri strumenti. Ogni articolo dovrebbe illustrare gli strumenti prerequisiti per l'esecuzione di un'attività specifica. Per un elenco completo degli strumenti e dei collegamenti di installazione, vedere [Install SQL Server 2019 Big Data Tools](deploy-big-data-tools.md).

## <a name="kubernetes"></a>kubernetes

I cluster di Big data vengono distribuiti come una serie di contenitori intercorrelati gestiti in [Kubernetes](https://kubernetes.io/docs/home). È possibile ospitare Kubernetes in diversi modi. Anche se si dispone già di un ambiente Kubernetes esistente, è necessario esaminare i requisiti correlati per i cluster Big Data.

- **Azure Kubernetes Service (AKS)** : AKS consente di distribuire un cluster Kubernetes gestito in Azure. È possibile gestire e gestire solo i nodi dell'agente. Con AKS non è necessario effettuare il provisioning del proprio hardware per il cluster. È anche facile usare uno [script di distribuzione](quickstart-big-data-cluster-deploy.md) di Big Data cluster per creare il cluster AKS e distribuire il cluster Big data in un unico passaggio. Per altre informazioni sull'uso di AKS con Big Data cluster, vedere [configurare il servizio Azure Kubernetes per le distribuzioni di SQL Server 2019 Big Data cluster (anteprima)](deploy-on-aks.md).

- **Più computer**: È anche possibile distribuire Kubernetes in più computer Linux, che possono essere server fisici o macchine virtuali. Lo strumento [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) può essere usato per creare il cluster Kubernetes. Questo metodo funziona correttamente se si dispone già di un'infrastruttura che si vuole usare per il cluster Big Data. Per altre informazioni sull'uso di distribuzioni di **kubeadm** con Big Data cluster, vedere [configurare Kubernetes in più computer per le distribuzioni di SQL Server 2019 Big Data cluster (anteprima)](deploy-with-kubeadm.md).

- **Minikube**: Minikube consente di eseguire Kubernetes localmente in un singolo server. Si tratta di un'opzione utile se si sta provando Big Data cluster o se è necessario usarla in uno scenario di test o di sviluppo. Per ulteriori informazioni sull'utilizzo di Minikube, vedere la [documentazione di Minikube](https://kubernetes.io/docs/setup/minikube/). Per requisiti specifici per l'uso di Minikube con i cluster di Big Data, vedere [configurare Minikube per le distribuzioni di cluster SQL Server 2019 Big Data](deploy-on-minikube.md).

## <a name="deploy-a-big-data-cluster"></a>Distribuire un cluster Big Data

Dopo la configurazione di Kubernetes, è possibile distribuire un cluster `azdata bdc create` di Big data con il comando. Quando si distribuisce, è possibile adottare diversi approcci.

- Se si esegue la distribuzione in un ambiente di sviluppo e test, è possibile scegliere di usare una delle [configurazioni predefinite](deployment-guidance.md#deploy) fornite da **azdata**.

- Per personalizzare la distribuzione, è possibile creare e usare i [file di configurazione della distribuzione](deployment-guidance.md#configfile).

- Per un'installazione completamente automatica, è possibile passare tutte le altre impostazioni nelle variabili di ambiente. Per ulteriori informazioni, vedere [distribuzioni automatiche](deployment-guidance.md#unattended).

## <a name="deployment-scripts"></a>Script di distribuzione

Gli script di distribuzione consentono di distribuire i cluster Kubernetes e Big Data in un unico passaggio. Spesso forniscono anche valori predefiniti per Big Data impostazioni del cluster. Per un esempio di uno script di distribuzione per Big Data cluster in Azure Kubernetes Service (AKS), vedere l'articolo seguente:

[Distribuire un cluster SQL Server 2019 Big data con uno script di distribuzione (AKS)](quickstart-big-data-cluster-deploy.md).

È possibile personalizzare qualsiasi script di distribuzione creando una versione personalizzata che configura le variabili di ambiente del cluster Big Data in modo diverso.

[Distribuire un cluster SQL Server 2019 Big data con Azure Data Studio notebook](deploy-notebooks.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito correttamente un cluster di Big Data, [connettersi al cluster](connect-to-big-data-cluster.md) e prendere in considerazione il [caricamento dei dati di esempio](tutorial-load-sample-data.md) da usare con diverse procedure dettagliate.