---
title: Supporto per GPU e TensorFlow
titleSuffix: SQL Server 2019 big data clusters
description: Distribuire un cluster di big data con supporto GPU e usare TensorFlow nei notebook di Studio dei dati di Azure.
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 03/14/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f766c343152fa601cc22e59e3385c454ec23879
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58162041"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>Distribuire un cluster di big data con supporto GPU ed eseguire TensorFlow

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
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.7 --location eastus
   ```

   > [!NOTE]
   > In questo cluster Usa la **Standard_NC6** [dimensioni delle macchine virtuali ottimizzate per la GPU](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu), ovvero una delle macchine virtuali specializzate disponibili con GPU singole o più GPU NVIDIA. Per altre informazioni, vedere [utilizzo GPU per carichi di lavoro a elevato utilizzo di calcolo in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/gpu-cluster).

1. Per configurare kubectl per la connessione al cluster Kubernetes, eseguire la [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando.

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>Applicare manifesto YAML

1. Uso **kubectl** per creare uno spazio dei nomi Kubernetes denominato `gpu-resources`.

   ```
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

   ```
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>Distribuire il cluster di big data

Per distribuire un cluster di big data di SQL Server 2019 (anteprima) che supporta le GPU, è necessario distribuire da un registro docker specifico e un archivio. In particolare, si utilizzano valori diversi per **DOCKER_REGISTRY**, **DOCKER_REPOSITORY**, **DOCKER_USERNAME**, **DOCKER_PASSWORD**, e **DOCKER_EMAIL**. Le sezioni seguenti forniscono esempi di come impostare le variabili di ambiente. Usare le sezioni di Windows o Linux a seconda della piattaforma del client che si usa per distribuire il cluster di big data.

### <a name="windows"></a>Windows

   1. Usa una finestra CMD (non PowerShell), configurare le seguenti variabili di ambiente. Non utilizzare le virgolette per racchiudere i valori.

      ```cmd
      SET ACCEPT_EULA=yes
      SET CLUSTER_PLATFORM=aks

      SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
      SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
      SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
      SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

      SET DOCKER_REGISTRY=marinchcreus3.azurecr.io
      SET DOCKER_REPOSITORY=ctp23-8-0-61-gpu
      SET DOCKER_USERNAME=<your username, gpu-specific credentials provided by Microsoft>
      SET DOCKER_PASSWORD=<your password, gpu-specific credentials provided by Microsoft>
      SET DOCKER_EMAIL=<your email address>
      SET DOCKER_PRIVATE_REGISTRY=1
      SET STORAGE_SIZE=10Gi
      ```

   1. Distribuire il cluster di big data:

      ```cmd
      mssqlctl cluster create --name gpubigdatacluster
      ```

### <a name="linux"></a>Linux

   1. Inizializzare le variabili di ambiente seguenti. In bash, è possibile usare le virgolette per racchiudere ogni valore.

      ```bash
      export ACCEPT_EULA=yes
      export CLUSTER_PLATFORM="aks"

      export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
      export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
      export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
      export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

      export DOCKER_REGISTRY="marinchcreus3.azurecr.io"
      export DOCKER_REPOSITORY="ctp23-8-0-61-gpu"
      export DOCKER_USERNAME="<your username, gpu-specific credentials provided by Microsoft>"
      export DOCKER_PASSWORD="<your password, gpu-specific credentials provided by Microsoft>"
      export DOCKER_EMAIL="<your email address>"
      export DOCKER_PRIVATE_REGISTRY="1"
      export STORAGE_SIZE="10Gi"
      ```

   1. Distribuire il cluster di big data:

      ```bash
      mssqlctl cluster create --name gpubigdatacluster
      ```

## <a name="run-the-tensorflow-example"></a>Eseguire l'esempio TensorFlow

Il notebook due esempi seguenti illustra due immagini classificazione modelli di training in un singolo nodo del cluster Spark usando TensorFlow per GPU.

| Download di notebook | Descrizione |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | Usa 8 CUDA, CUDNN 6 e TensorFlow 1.4.0.  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | Usa TensorFlow 1.12.0 CUDA 9 e CUDNN 7. |

Inserire il file di notebook appropriato nel computer locale e quindi aprire ed eseguirlo in Studio dati di Azure usando il kernel di PySpark3. A meno che non si dispone di un'esigenza specifica per una versione precedente di CUDA o TensorFlow, scegliere CUDA 9/CUDNN 7/TensorFlow 1.12.0. Per altre informazioni su come usare i notebook con cluster di big data, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md).

> [!NOTE]
> Si noti che i notebook di installare il software nei percorsi di sistema. Ciò è possibile poiché i notebook vengono attualmente eseguono con i privilegi root in CTP 2.3.

Dopo aver installato le librerie di GPU NVIDIA e TensorFlow per GPU, i notebook elenco dispositivi GPU disponibili. È quindi adatta e valutare un modello TensorFlow in modo che riconosca utilizzando il set di dati MNIST di cifre scritte a mano. Dopo aver verificato lo spazio su disco disponibile, scaricare ed eseguire l'esempio di classificazione immagini CIFAR 10 dal [ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git). Eseguendo l'esempio di 10 CIFAR in cluster con GPU diverse, è possibile osservare l'incremento della velocità offerta da ogni generazione di GPU disponibili in Azure.

## <a name="clean-up-resources"></a>Pulire le risorse

Per eliminare il cluster di big data, usare il comando seguente:

```
mssqlctl cluster delete --name gpubigdatacluster
```

Il comando precedente non rimuove il cluster AKS. Per eliminare il cluster AKS e le risorse è associate, usare il comando seguente:

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data 2019 Server SQL (anteprima), vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).