---
title: Configurare Azure Kubernetes Service
titleSuffix: SQL Server big data clusters
description: Informazioni su come configurare Azure Kubernetes Service (AKS) per le distribuzioni di cluster (anteprima) di SQL Server 2019 dei big Data.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 51c7dbf8e50f6c3537a2a4171720c160c444471d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797870"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Configurare Azure Kubernetes Service per le distribuzioni di cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come configurare Azure Kubernetes Service (AKS) per le distribuzioni di cluster (anteprima) di SQL Server 2019 dei big Data.

Servizio contenitore di AZURE rende più semplice creare, configurare e gestire un cluster di macchine virtuali che sono preconfigurate con un cluster Kubernetes per eseguire applicazioni in contenitori. In questo modo è possibile usare le competenze esistenti o disegnare su un consistente e crescente bagaglio di competenze della community, distribuire e gestire le applicazioni basate su contenitore in Microsoft Azure.

Questo articolo descrive i passaggi per la distribuzione di Kubernetes nel servizio contenitore di AZURE tramite la CLI di Azure. Se non hai una sottoscrizione di Azure, creare un account gratuito prima di iniziare.

> [!TIP] 
> Per un esempio di script python che consente di distribuire cluster di big data sia servizio contenitore di AZURE e SQL Server, vedere [Guida introduttiva: Distribuire SQL Server in Azure Kubernetes Service (AKS) del cluster dei big data](quickstart-big-data-cluster-deploy.md).

## <a name="prerequisites"></a>Prerequisiti

- [Distribuire gli strumenti dei big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Comando di Azure**

- Versione minima 1.10 per il server di Kubernetes. Per AKS, è necessario usare `--kubernetes-version` parametro per specificare una versione diversa da quella predefinita.

- Per un'esperienza ottimale durante la convalida di scenari di base sul servizio contenitore di AZURE, usare:
   - 8 Vcpu in tutti i nodi
   - 32 GB di memoria per ogni macchina virtuale
   - 24 o più collegati dischi in tutti i nodi

   > [!TIP]
   > Infrastruttura di Azure offre più opzioni di dimensioni per le macchine virtuali, vedere [qui](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) per le selezioni nell'area di cui si prevede di distribuire.

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Un gruppo di risorse di Azure è un gruppo logico in Azure le risorse vengono distribuite e gestite. Questa procedura, accede ad Azure e crea un gruppo di risorse per il cluster AKS.

1. Al prompt dei comandi, eseguire il comando seguente e seguire le istruzioni per eseguire l'accesso alla sottoscrizione di Azure:

    ```azurecli
    az login
    ```

1. Se si hanno più sottoscrizioni, è possibile visualizzare tutte le sottoscrizioni eseguendo il comando seguente:

   ```azurecli
   az account list
   ```

1. Se si desidera modificare una sottoscrizione diversa è possibile eseguire questo comando:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Creare un gruppo di risorse con il **creare il gruppo di az** comando. L'esempio seguente crea un gruppo di risorse denominato `sqlbigdatagroup` nella `westus2` posizione.

   ```azurecli
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>Creare un cluster Kubernetes

1. Creare un cluster Kubernetes nel servizio contenitore di AZURE con il [az aks create](https://docs.microsoft.com/cli/azure/aks) comando. L'esempio seguente crea un cluster Kubernetes denominato *kubcluster* con un nodo dell'agente Linux di dimensioni **Standard_L8s**. Assicurarsi di che creare il cluster AKS nello stesso gruppo di risorse usato nelle sezioni precedenti.

    ```azurecli
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_L8s \
    --node-count 1 \
    --kubernetes-version 1.12.8
    ```

   È possibile aumentare o ridurre il numero di nodi agente Kubernetes modificando la `--node-count <n>` in cui `<n>` è il numero di nodi di agenti da usare. Questo non include il nodo master Kubernetes, che viene gestito in background dal servizio contenitore di AZURE. L'esempio precedente Usa solo un singolo nodo per scopi di valutazione.

   Dopo alcuni minuti, il comando viene completato e restituisce le informazioni in formato JSON sul cluster.

1. Salvare l'output JSON ottenuto dal comando precedente per un uso successivo.

## <a name="connect-to-the-cluster"></a>Connettersi al cluster

1. Per configurare kubectl per la connessione al cluster Kubernetes, eseguire la [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando. Questo passaggio Scarica credenziali e consente di configurare l'interfaccia della riga di comando per usarli kubectl.

   ```azurecli
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. Per verificare la connessione al cluster, usare il [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando per restituire un elenco dei nodi del cluster.  L'esempio seguente mostra l'output se fosse necessario 1 master e 3 nodi agente.

   ```
   kubectl get nodes
   ```

## <a name="next-steps"></a>Passaggi successivi

I passaggi descritti in questo articolo è configurato un cluster Kubernetes nel servizio contenitore di AZURE. Il passaggio successivo consiste nel distribuire SQL Server 2019 dei big data per il cluster. Per altre informazioni su come distribuire i cluster di big data, vedere l'articolo seguente:

[Come distribuire i cluster di big data di SQL Server in Kubernetes](deployment-guidance.md)
