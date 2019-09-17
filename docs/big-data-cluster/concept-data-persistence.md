---
title: Salvataggio permanente dei dati in Kubernetes
titleSuffix: SQL Server big data clusters
description: Informazioni sul funzionamento del salvataggio permanente dei dati in un cluster Big Data di SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb6d87803c0a3839afd8dbd1333b52c3abcc4518
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878744"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Salvataggio permanente dei dati con un cluster Big Data di SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

I [volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) offrono un modello plug-in per l'archiviazione in Kubernetes. Il modo in cui viene fornita archiviazione è astratto rispetto al modo in cui viene utilizzata. Di conseguenza, è possibile usare la propria risorsa di archiviazione a disponibilità elevata e collegarla al cluster Big Data di SQL Server. In questo modo, si ottiene il controllo completo sul tipo di archiviazione, sulla disponibilità e sulle prestazioni necessari. Kubernetes supporta vari tipi di soluzioni di archiviazione, tra cui dischi/file di Azure, NFS, archiviazione locale e altro ancora.

## <a name="configure-persistent-volumes"></a>Configurare volumi permanenti

Un cluster Big Data di SQL Server utilizza questi volumi permanenti tramite [classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/). È possibile creare classi di archiviazione diverse per diversi tipi di archiviazione e specificarle in fase di distribuzione del cluster Big Data. È possibile configurare la classe di archiviazione e la dimensione dell'attestazione di volume permanente da usare per uno scopo specifico a livello di pool. Crea un cluster di big data server [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con il nome della classe di archiviazione specificato per ogni componente che richiede volumi permanenti. Monta quindi i volumi permanenti corrispondenti nel pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurare le impostazioni di archiviazione del cluster Big Data

Analogamente ad altre personalizzazioni, è possibile specificare le impostazioni di archiviazione nei file di configurazione del cluster al momento della distribuzione per ogni pool nel file di configurazione **BDC. JSON** e per i servizi di controllo nel file **Control. JSON** . Se non sono presenti impostazioni di configurazione dell'archiviazione nelle specifiche del pool, le impostazioni di archiviazione del controllo verranno usate **per tutti gli altri componenti**, tra cui SQL Server Master (risorsa**Master** ), HDFS (risorsa**storage-0** ) o dati piscina. Questo è un esempio della sezione di configurazione dell'archiviazione che è possibile includere nella specifica:

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

La distribuzione del cluster Big Data userà l'archiviazione permanente per archiviare i dati, i metadati e i log per diversi componenti. È possibile personalizzare le dimensioni delle attestazioni di volumi permanenti create come parte della distribuzione. Come procedura consigliata, si consiglia di usare classi di archiviazione con un *criterio di recupero* [Retain](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> Nella versione CTP 3.2 non è possibile modificare l'impostazione di configurazione dell'archiviazione dopo la distribuzione. Inoltre, è supportata solo la modalità di accesso `ReadWriteOnce` per l'intero cluster.

> [!WARNING]
> L'esecuzione senza archiviazione permanente può funzionare in un ambiente di test, ma può causare il mancato funzionamento del cluster. Al riavvio del pod, i metadati del cluster e/o i dati utente andranno persi in modo permanente. Non è consigliabile usare questa configurazione per l'esecuzione. 

La sezione [Configurare l'archiviazione](#config-samples) contiene altri esempi su come configurare le impostazioni di archiviazione per la distribuzione del cluster Big Data di SQL Server.

## <a name="aks-storage-classes"></a>Classi di archiviazione del servizio Azure Kubernetes

Il servizio Azure Kubernetes include [due classi di archiviazione predefinite](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv), **default** e **managed-premium**, insieme allo strumento di provisioning dinamico per entrambe. È possibile specificare una delle due per creare una classe di archiviazione personalizzata per la distribuzione del cluster Big Data con archiviazione permanente abilitata. Per impostazione predefinita, il file di configurazione del cluster predefinito per *aks-dev-test* del servizio Azure Kubernetes include configurazioni di archiviazione permanente per usare la classe di archiviazione **default**.

> [!WARNING]
> I volumi permanenti creati con le classi di archiviazione predefinite **default** e **managed-premium** usano il criterio di recupero *Delete*. Di conseguenza, quando si elimina il cluster Big Data di SQL Server, vengono eliminati anche le attestazioni di volumi permanenti e quindi i volumi permanenti. È possibile creare classi di archiviazione personalizzate usando lo strumento di provisioning **azure-disk** con un criterio di recupero *Retain*, come mostrato in [questo](https://docs.microsoft.com/azure/aks/concepts-storage#storage-classes) articolo.


## <a name="minikube-storage-class"></a>Classe di archiviazione di minikube

minikube include una classe di archiviazione predefinita denominata **standard**, insieme al relativo strumento di provisioning dinamico. Il file di configurazione predefinito per *minikube-dev-test* di minikube include le impostazioni di configurazione dell'archiviazione nella specifica del piano di controllo. Le stesse impostazioni verranno applicate a tutte le specifiche dei pool. È anche possibile personalizzare una copia di questo file e usarla per la distribuzione del cluster Big Data in minikube. È possibile modificare manualmente il file personalizzato e le dimensioni delle attestazioni di volumi permanenti per pool specifici in base ai carichi di lavoro che si vuole eseguire. In alternativa, vedere la sezione [Configurare l'archiviazione](#config-samples) per alcuni esempi su come eseguire le modifiche tramite comandi *azdata*.

## <a name="kubeadm-storage-classes"></a>Classi di archiviazione di kubeadm

kubeadm non include una classe di archiviazione predefinita. È necessario creare classi di archiviazione personalizzate e volumi permanenti usando l'archiviazione locale o lo strumento di provisioning preferito, ad esempio [Rook](https://github.com/rook/rook). In questo caso, è necessario impostare **className** sulla classe di archiviazione configurata. 

> [!NOTE]
>  Nel file di configurazione della distribuzione predefinito per *kubeadm kubeadm-dev-test* non è stato specificato alcun nome di classe di archiviazione per l'archiviazione di dati e log. Prima della distribuzione, è necessario personalizzare il file di configurazione e impostare il valore di className, altrimenti le convalide precedenti alla distribuzione non riusciranno. La distribuzione prevede anche un passaggio di convalida che controlla l'esistenza della classe di archiviazione, ma non i volumi permanenti necessari. È necessario assicurarsi di creare volumi sufficienti in base alla scala del cluster. Nella versione CTP 3.1 per le dimensioni predefinite del cluster è necessario creare almeno 23 volumi. [Qui](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) è disponibile un esempio di come creare volumi permanenti tramite uno strumento di provisioning locale.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizzare le configurazioni di archiviazione per ogni pool

Per tutte le personalizzazioni, è necessario innanzitutto creare una copia del file di configurazione predefinito che si vuole usare. Ad esempio, il comando seguente crea una copia dei file di configurazione della distribuzione per *aks-dev-test* in una sottodirectory denominata `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Verranno creati due file, **BDC. JSON** e **Control. JSON** , che possono essere personalizzati modificando manualmente oppure è possibile usare il comando **azdata BDC config** . È possibile usare una combinazione di librerie jsonpath e jsonpatch per fornire modi per modificare i file di configurazione.


### <a id="config-samples"></a> Configurare il nome della classe di archiviazione e/o le dimensioni delle attestazioni

Per impostazione predefinita, la dimensione delle attestazioni di volume permanente di cui è stato effettuato il provisioning per ognuno dei pod di cui è stato effettuato il provisioning nel cluster è 10 GB. È possibile aggiornare questo valore in base ai carichi di lavoro in esecuzione in un file di configurazione personalizzato prima della distribuzione del cluster.

L'esempio seguente aggiorna la dimensione delle attestazioni di volume permanente a 32Gi nel file **control.json**. Se non viene sostituita a livello di pool, questa impostazione verrà applicata a tutti i pool:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

L'esempio seguente mostra come modificare la classe di archiviazione per il file **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Un'altra opzione consiste nel modificare manualmente il file di configurazione personalizzato o usare il file di patch JSON, come nell'esempio seguente, che modifica la classe di archiviazione per il pool di archiviazione. Creare un file *patch.json* con questo contenuto:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

Applicare il file di patch. Usare il comando **azdata bdc config patch** per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file patch.json a un file di configurazione della distribuzione di destinazione custom.json.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per la documentazione completa sui volumi in Kubernetes, vedere la [documentazione di Kubernetes sui volumi](https://kubernetes.io/docs/concepts/storage/volumes/).

Per altre informazioni sulle distribuzioni di un cluster Big Data di SQL Server, vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md).

