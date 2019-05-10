---
title: Supporto per GPU e TensorFlow
titleSuffix: SQL Server big data clusters
description: Distribuire un cluster di big data con supporto GPU e usare TensorFlow nei notebook di Studio dei dati di Azure.
author: inchiosa
ms.author: marinch
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2d31736ee4dd68857e3afce678b6dd806701a82b
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774948"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>Distribuire un cluster di big data con supporto GPU ed eseguire TensorFlow

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo illustra come distribuire un cluster di big data in Azure Kubernetes Service (AKS) che supportano pool di nodi abilitate per GPU per carichi di lavoro a elevato utilizzo di calcolo. È quindi possibile eseguire notebook di esempio in Azure Data Studio di cui eseguire la classificazione delle immagini con TensorFlow per GPU.

## <a name="prerequisites"></a>Prerequisiti

- [Gli strumenti dei big data](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **Estensione di SQL Server 2019**
  - **Comando di Azure**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>Creare un cluster del servizio contenitore di AZURE

La procedura seguente usa il comando di Azure per creare un cluster servizio contenitore di AZURE che supporta le GPU.

1. Al prompt dei comandi, eseguire il comando seguente e seguire le istruzioni per accedere alla sottoscrizione di Azure:

    ```azurecli
    az login
    ```

1. Creare un gruppo di risorse con il **creare il gruppo di az** comando. L'esempio seguente crea un gruppo di risorse denominato `sqlbigdatagroupgpu` nella `eastus` posizione.

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. Creare un cluster Kubernetes nel servizio contenitore di AZURE con il [az aks create](https://docs.microsoft.com/cli/azure/aks) comando. L'esempio seguente crea un cluster Kubernetes denominato `gpucluster` nella `sqlbigdatagroupgpu` gruppo di risorse.

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6s_v3 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.9 --location eastus
   ```

   > [!NOTE]
   > In questo cluster Usa la **Standard_NC6s_v3** [dimensioni delle macchine virtuali ottimizzate per la GPU](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu), ovvero una delle macchine virtuali specializzate disponibili con GPU singole o più GPU NVIDIA. Per altre informazioni, vedere [utilizzo GPU per carichi di lavoro a elevato utilizzo di calcolo in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/gpu-cluster).

1. Per configurare kubectl per la connessione al cluster Kubernetes, eseguire la [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando.

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>Applicare manifesto YAML

1. Uso **kubectl** per creare uno spazio dei nomi Kubernetes denominato `gpu-resources`.

   ```bash
   kubectl create namespace gpu-resources
   ```

1. Salvare il contenuto del file YAML seguente in un file denominato **nvidia-device-plugin-ds.yaml**. Salvare questo nella directory di lavoro nel computer che si esegue **kubectl** da.

   Aggiornamento di `image: nvidia/k8s-device-plugin:1.11` metà il manifesto in modo che corrisponda alla versione di Kubernetes. Ad esempio, se il cluster AKS esegue Kubernetes versione 1.12, aggiornare il tag `image: nvidia/k8s-device-plugin:1.12`.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. Usare ora il kubectl apply comando per creare il DaemonSet. **NVIDIA-device-plugin-ds.yaml** deve essere nella directory di lavoro quando si esegue il comando seguente:

   ```bash
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>Distribuire il cluster di big data

Per distribuire un cluster di big data di SQL Server 2019 (anteprima) che supporta le GPU, è necessario distribuire da un registro docker specifico e un archivio. Le seguenti variabili di ambiente sono diverse per una distribuzione di GPU:

| Variabile di ambiente | Value |
|---|---|
| **DOCKER_REGISTRY** | `marinchcreus3.azurecr.io` |
| **DOCKER_REPOSITORY** | `ctp25-8-0-61-gpu` |
| **DOCKER_USERNAME** | `<your username, gpu-specific credentials provided by Microsoft>` |
| **DOCKER_PASSWORD** | `<your password, gpu-specific credentials provided by Microsoft>` |

Uso **mssqlctl** per distribuire il cluster, selezionare la configurazione del servizio contenitore di Azure-dev-test.json e specificare valori personalizzati quando richiesto.

```bash
mssqlctl cluster create
```

> [!TIP]
> Il nome predefinito del cluster di big data è `mssql-cluster`.

È anche possibile personalizzare ulteriormente la distribuzione mediante il passaggio di un file di configurazione di distribuzione personalizzato. Per altre informazioni, vedere la [Guida alla distribuzione](deployment-guidance.md#customconfig).

## <a name="run-the-tensorflow-example"></a>Eseguire l'esempio TensorFlow

Il notebook due esempi seguenti illustra due immagini classificazione modelli di training in un singolo nodo del cluster Spark usando TensorFlow per GPU.

| Download di notebook | Descrizione |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | Usa 8 CUDA, CUDNN 6 e TensorFlow 1.4.0.  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | Usa TensorFlow 1.12.0 CUDA 9 e CUDNN 7. |

Inserire il file di notebook appropriato nel computer locale e quindi aprire ed eseguirlo in Studio dati di Azure usando il kernel di PySpark3. A meno che non si dispone di un'esigenza specifica per una versione precedente di CUDA o TensorFlow, scegliere CUDA 9/CUDNN 7/TensorFlow 1.12.0. Per altre informazioni su come usare i notebook con cluster di big data, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md).

> [!NOTE]
> Si noti che i notebook di installare il software nei percorsi di sistema. Ciò è possibile poiché i notebook attualmente eseguono con i privilegi root in CTP 2.5.

Dopo aver installato le librerie di GPU NVIDIA e TensorFlow per GPU, i notebook elenco dispositivi GPU disponibili. È quindi adatta e valutare un modello TensorFlow in modo che riconosca utilizzando il set di dati MNIST di cifre scritte a mano. Dopo aver verificato lo spazio su disco disponibile, scaricare ed eseguire l'esempio di classificazione immagini CIFAR 10 dal [ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git). Eseguendo l'esempio di 10 CIFAR in cluster con GPU diverse, è possibile osservare l'incremento della velocità offerta da ogni generazione di GPU disponibili in Azure.

## <a name="clean-up-resources"></a>Pulire le risorse

Per eliminare il cluster di big data, usare il comando seguente:

```bash
mssqlctl cluster delete --name gpubigdatacluster
```

Il comando precedente non rimuove il cluster AKS. Per eliminare il cluster AKS e le risorse è associate, usare il comando seguente:

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data 2019 Server SQL (anteprima), vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
