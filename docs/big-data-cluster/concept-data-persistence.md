---
title: Persistenza dei dati in Kubernetes
titleSuffix: SQL Server big data clusters
description: Informazioni sul funzionamento della persistenza dei dati in un cluster SQL Server 2019 Big Data.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419466"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistenza dei dati con SQL Server cluster di Big Data in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

I [volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) forniscono un modello di plug-in per l'archiviazione in Kubernetes. Il modo in cui viene fornita l'archiviazione è astratto dal modo in cui viene utilizzato. Pertanto, è possibile portare il proprio spazio di archiviazione a disponibilità elevata e inserirlo nel cluster SQL Server Big Data. In questo modo si ottiene il controllo completo sul tipo di archiviazione, disponibilità e prestazioni necessari. Kubernetes supporta vari tipi di soluzioni di archiviazione, tra cui dischi/file di Azure, NFS, archiviazione locale e altro ancora.

## <a name="configure-persistent-volumes"></a>Configurare i volumi permanenti

Il modo in cui un cluster SQL Server Big Data utilizza questi volumi persistenti consiste nell'utilizzare [le classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/). È possibile creare classi di archiviazione diverse per diversi tipi di archiviazione e specificarle al momento della distribuzione del cluster Big Data. È possibile configurare la classe di archiviazione e la dimensione di attestazione del volume permanente da usare per lo scopo a livello di pool. Crea un cluster di big data server [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con il nome della classe di archiviazione specificato per ogni componente che richiede volumi permanenti. Quindi monta i volumi persistenti corrispondenti nel pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurare le impostazioni di archiviazione del cluster Big Data

Analogamente ad altre personalizzazioni, è possibile specificare le impostazioni di archiviazione nei file di configurazione del cluster al momento della distribuzione per ogni pool e il piano di controllo. Se non sono presenti impostazioni di configurazione dell'archiviazione nelle specifiche del pool, verranno usate le impostazioni di archiviazione del piano di controllo. Questo è un esempio della sezione di configurazione dell'archiviazione che è possibile includere nella specifica:

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

La distribuzione di Big Data cluster utilizzerà l'archiviazione permanente per archiviare i dati, i metadati e i log per i vari componenti. È possibile personalizzare le dimensioni delle attestazioni del volume permanente create come parte della distribuzione. Come procedura consigliata, si consiglia di usare le classi di archiviazione con un criterio *Mantieni* [richiesta](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> Nella versione CTP 3,2 non è possibile modificare l'impostazione di configurazione dell'archiviazione dopo la distribuzione. Inoltre, è `ReadWriteOnce` supportata solo la modalità di accesso per l'intero cluster.

> [!WARNING]
> L'esecuzione senza archiviazione permanente può funzionare in un ambiente di test, ma potrebbe causare un cluster non funzionante. Al riavvio del Pod, i metadati del cluster e/o i dati utente andranno persi in modo permanente. Non è consigliabile eseguire in questa configurazione. 

La sezione [configurare l'archiviazione](#config-samples) fornisce altri esempi su come configurare le impostazioni di archiviazione per la distribuzione del cluster SQL Server Big Data.

## <a name="aks-storage-classes"></a>Classi di archiviazione AKS

AKS include [due classi di archiviazione](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **predefinite** e **gestite-Premium** insieme al provisioning dinamico. È possibile specificare uno di questi o creare una classe di archiviazione personalizzata per la distribuzione di Big Data cluster con archiviazione permanente abilitata. Per impostazione predefinita, il file di configurazione del cluster incorporato per AKS *AKS-dev-test* include configurazioni di archiviazione permanenti per usare la classe di archiviazione **predefinita** .

> [!WARNING]
> I volumi permanenti creati con le classi di archiviazione **predefinite** e **Managed-Premium** hanno un criterio di rimborso di *Delete*. Quindi, quando si eliminano i SQL Server cluster Big Data, le attestazioni del volume permanente vengono eliminate e anche i volumi persistenti. È possibile creare classi di archiviazione personalizzate usando privioner del **disco di Azure** con un criterio *Mantieni* recupera come illustrato in [questo](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) articolo.


## <a name="minikube-storage-class"></a>Classe di archiviazione Minikube

Minikube viene fornito con una classe di archiviazione predefinita denominata **standard** insieme a un provisioning dinamico. Il file di configurazione predefinito per minikube *minikube-dev-test* include le impostazioni di configurazione dell'archiviazione nella specifica del piano di controllo. Le stesse impostazioni verranno applicate a tutte le specifiche del pool. È anche possibile personalizzare una copia di questo file e usarla per la distribuzione del cluster Big Data in minikube. È possibile modificare manualmente il file personalizzato e modificare le dimensioni delle attestazioni dei volumi permanenti per pool specifici in modo da contenere i carichi di lavoro che si desidera eseguire. In alternativa, vedere la sezione [Configure Storage](#config-samples) per esempi su come eseguire le modifiche usando i comandi *azdata* .

## <a name="kubeadm-storage-classes"></a>Classi di archiviazione Kubeadm

Kubeadm non dispone di una classe di archiviazione incorporata. È necessario creare classi di archiviazione e volumi permanenti usando l'archiviazione locale o il provisioning preferito, ad esempio [Rook](https://github.com/rook/rook). In tal caso, è necessario impostare **ClassName** sulla classe di archiviazione configurata. 

> [!NOTE]
>  Nel file di configurazione della distribuzione incorporato per *kubeadm kubeadm-dev-test* non è stato specificato alcun nome di classe di archiviazione per i dati e l'archiviazione dei log. Prima della distribuzione, è necessario personalizzare il file di configurazione e impostare il valore per ClassName in caso contrario, le convalide di pre-distribuzione avranno esito negativo. La distribuzione prevede inoltre un passaggio di convalida che controlla l'esistenza della classe di archiviazione, ma non per i volumi persistenti necessari. È necessario assicurarsi di creare volumi sufficienti a seconda della scala del cluster. In CTP 3,1, per le dimensioni predefinite del cluster è necessario creare almeno 23 volumi. Di [seguito](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) è riportato un esempio su come creare volumi permanenti usando il provisioner locale.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizzare le configurazioni di archiviazione per ogni pool

Per tutte le personalizzazioni, è necessario innanzitutto creare una copia del file di configurazione predefinito che si desidera utilizzare. Ad esempio, il comando seguente crea una copia dei file di configurazione della distribuzione *AKS-dev-test* in una sottodirectory `custom`denominata:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Verranno creati due file, **cluster. JSON** e **Control. JSON** , che possono essere personalizzati modificando manualmente oppure è possibile usare il comando **azdata BDC config** . È possibile usare una combinazione di librerie jsonpath e jsonpatch per fornire modi per modificare i file di configurazione.


### <a id="config-samples"></a>Configurare il nome della classe di archiviazione e/o le dimensioni delle attestazioni

Per impostazione predefinita, la dimensione delle attestazioni del volume permanente di cui è stato effettuato il provisioning per ognuno dei pod di cui è stato effettuato il provisioning nel cluster è 10 GB. È possibile aggiornare questo valore per gestire i carichi di lavoro in esecuzione in un file di configurazione personalizzato prima della distribuzione del cluster.

Nell'esempio seguente viene aggiornata la dimensione delle attestazioni del volume permanente a 32Gi nel **controllo. jsaon**. Se non viene sottoposto a override a livello di pool, questa impostazione verrà applicata a tutti i pool:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

Nell'esempio seguente viene illustrato come modificare la classe di archiviazione per il file **Control. JSON** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Un'altra opzione consiste nel modificare manualmente il file di configurazione personalizzato o usare patch JSON, come nell'esempio seguente, che modifica la classe di archiviazione per il pool di archiviazione. Creare un file *patch. JSON* con questo contenuto:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

Applicare il file della patch. Usare il comando **azdata BDC config patch** per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file patch. JSON a un file di configurazione della distribuzione di destinazione Custom. JSON.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per la documentazione completa sui volumi in Kubernetes, vedere la [documentazione di Kubernetes sui volumi](https://kubernetes.io/docs/concepts/storage/volumes/).

Per ulteriori informazioni sulla distribuzione di un cluster SQL Server Big Data, vedere [How to deploy SQL Server Big Data cluster on Kubernetes](deployment-guidance.md).

