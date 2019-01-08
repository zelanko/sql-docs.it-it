---
title: Persistenza dei dati in Kubernetes
titleSuffix: SQL Server 2019 big data clusters
description: Informazioni sul funzionamento di persistenza dei dati in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 75cf78e7c73ad61e5e28ed6f0707639899d8ec19
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207670"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistenza dei dati con cluster di big data di SQL Server in Kubernetes

[Volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) offrono un modello di plug-in archiviazione in Kubernetes in cui come archiviazione viene fornita è che sono state completate ricavati dall'utilizzo della risorsa. Pertanto, è possibile portare il proprio archiviazione a disponibilità elevata e inserirlo in cluster di cluster di SQL Server i big Data. Ciò offre il controllo completo sul tipo di archiviazione, disponibilità e prestazioni necessari. Kubernetes supporta vari tipi di soluzioni di archiviazione, tra cui dischi/file di Azure, NFS, risorsa di archiviazione locale e altro ancora.

## <a name="configure-persistent-volumes"></a>Configurare volumi permanenti

Il modo in cui il cluster di big data di SQL Server utilizza questi volumi permanenti consiste nell'usare [classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/). È possibile creare classi di archiviazione diversi per tipi diversi di archiviazione e specificarli al momento della distribuzione di cluster dei big Data. È possibile configurare la classe di archiviazione da usare per quale scopo (pool). Crea cluster di big data server&#41 [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con il nome della classe di archiviazione specificato per ogni pod necessari volumi permanenti. Quindi consente di montare i volumi permanenti corrispondenti nel pod.

> [!NOTE]
> Per la versione CTP 2.2, solo `ReadWriteOnce` modalità di accesso per l'intero cluster è supportata.

## <a name="deployment-settings"></a>Impostazioni di distribuzione

Per usare un archivio permanente durante la distribuzione, configurare il **USE_PERSISTENT_VOLUME** e **STORAGE_CLASS_NAME** variabili di ambiente prima dell'esecuzione `mssqlctl create cluster` comando. **USE_PERSISTENT_VOLUME** è impostata su `true` per impostazione predefinita. È possibile sostituire il valore predefinito e impostarlo su `false` e, in questo caso, il cluster di big data di SQL Server usa punti di montaggio emptyDir. 

> [!WARNING]
> L'esecuzione senza un archivio permanente può lavorare in un ambiente di test, ma potrebbero verificarsi in un cluster non funzionali. Al riavvio del pod, i dati dei metadati e/o utente del cluster andranno perse definitivamente.

Se si imposta il flag su true, è necessario specificare anche **STORAGE_CLASS_NAME** come parametro in fase di distribuzione.

## <a name="aks-storage-classes"></a>Classi di archiviazione servizio contenitore di AZURE

Servizio contenitore di AZURE viene fornito con [due classi di archiviazione predefinite](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **predefinita** e **gestiti premium** insieme dinamico strumento di provisioning per loro. È possibile specificare uno di questi due o creare la propria classe di archiviazione per la distribuzione di cluster di big data con abilitata l'archiviazione permanente.

## <a name="minikube-storage-class"></a>Classe di archiviazione Minikube

Minikube dotato di una classe di archiviazione predefinito denominata **standard** insieme a un strumento di provisioning dinamico appositamente. Si noti che in minikube, se `USE_PERSISTENT_VOLUME=true` (impostazione predefinita), è inoltre necessario sostituire il valore predefinito per il **STORAGE_CLASS_NAME** variabile di ambiente perché il valore predefinito è diverso. Impostare il valore su `standard`: 

In Windows, usare il comando seguente:

```cmd
SET STORAGE_CLASS_NAME=standard
```

In Linux, usare il comando seguente:

```cmd
export STORAGE_CLASS_NAME=standard
```

In alternativa, è possibile eliminare con volumi permanenti in minikube impostando `USE_PERSISTENT_VOLUME=false`.

## <a name="kubeadm"></a>Kubeadm

Kubeadm non viene fornito con una classe di archiviazione predefinito. È possibile scegliere di creare le classi di archiviazione con archiviazione locale o strumento di provisioning preferito, ad esempio e i volumi permanenti [torre](https://github.com/rook/rook). In tal caso, imposterebbe il **STORAGE_CLASS_NAME** alla classe di archiviazione è stato configurato. In alternativa, è possibile impostare `USE_PERSISTENT_VOLUME=false` negli ambienti di test, ma si noti l'avviso precedente nel **impostazioni distribuzione** sezione di questo articolo.  

## <a name="on-premises-cluster"></a>Cluster locale

I cluster locali ovviamente non vengono forniti con qualsiasi classe di archiviazione predefinito, pertanto è necessario configurare [volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[strumenti di provisioning](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/) in anticipo e quindi usare la corrispondente classi di archiviazione durante la distribuzione di cluster di SQL Server i big Data.

## <a name="customize-storage-size-for-each-pool"></a>Personalizzare le dimensioni di archiviazione per ogni pool
Per impostazione predefinita, le dimensioni del volume permanente sottoposta a provisioning per ognuno dei POD effettuato il provisioning del cluster sono 6 GB. Questa opzione è configurabile impostando la variabile di ambiente `STORAGE_SIZE` su un valore diverso. Ad esempio, è possibile eseguire comando seguente per impostare il valore su 10 GB, prima di eseguire il `mssqlctl create cluster command`.

```bash
export STORAGE_SIZE=10Gi
```

È anche possibile diverse configurazioni per le impostazioni di archiviazione permanente tale nome di classe di archiviazione e le dimensioni di volume permanente per i diversi pool nel cluster. Ad esempio, è possibile configurare i volumi permanenti distribuiti per il pool di archiviazione da usare una classe di archiviazione diversi e hanno una capacità superiore dall'impostazione di sotto delle variabili di ambiente prima di distribuire il cluster:

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=managed-premium
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

Ecco un elenco completo delle variabili di ambiente relative all'impostazione di un archivio permanente per il cluster di big data di SQL Server:

| Variabile di ambiente | Valore predefinito | Descrizione |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` Per utilizzare attestazioni Volume permanente Kubernetes per l'archiviazione di pod. `false` usare l'archiviazione temporanea host per l'archiviazione di pod. |
| **STORAGE_CLASS_NAME** | predefiniti | Se `USE_PERSISTENT_VOLUME` è `true` viene indicato il nome della classe di archiviazione Kubernetes da usare. |
| **STORAGE_SIZE** | Gi 6 | Se `USE_PERSISTENT_VOLUME` è `true`, indica le dimensioni di volume permanente per ogni pod. |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Per utilizzare attestazioni Volume permanente Kubernetes per i POD nel pool di dati. `false` usare l'archiviazione temporanea host per i POD del pool di dati. |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | Indica il nome della classe di archiviazione Kubernetes da usare per i volumi permanenti associati i POD del pool di dati.|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |Indica le dimensioni di volume permanente per ogni pod nel pool di dati. |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Per utilizzare attestazioni Volume permanente Kubernetes per i POD nel pool di archiviazione. `false` usare l'archiviazione temporanea host per i POD del pool di archiviazione.|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates associati il nome della classe di archiviazione Kubernetes da usare per i volumi permanenti con i POD del pool di archiviazione. |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | Indica le dimensioni di volume permanente per ogni pod nel pool di archiviazione. |

## <a name="next-steps"></a>Passaggi successivi

Per una documentazione completa sui volumi in Kubernetes, vedere la [documentazione di Kubernetes in volumi](https://kubernetes.io/docs/concepts/storage/volumes/).

Per altre informazioni sulla distribuzione di cluster di big data di SQL Server, vedere [come distribuire SQL Server del cluster di big data in Kubernetes](deployment-guidance.md).

