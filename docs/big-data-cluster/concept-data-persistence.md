---
title: Persistenza dei dati in Kubernetes
titleSuffix: SQL Server big data clusters
description: Informazioni sul funzionamento di persistenza dei dati in un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: edef0fa21cc2a41785e14f7c96cf3c52b1e0bacb
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472201"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistenza dei dati con cluster di big data di SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) offrono un modello di plug-in per l'archiviazione in Kubernetes. Modo in cui viene fornita un'archiviazione viene astratto dall'utilizzo della risorsa. Pertanto, è possibile portare il proprio archiviazione a disponibilità elevata e inserirlo in cluster di big data di SQL Server. Ciò offre il controllo completo sul tipo di archiviazione, disponibilità e prestazioni necessari. Kubernetes supporta vari tipi di soluzioni di archiviazione, tra cui dischi/file di Azure, NFS, risorsa di archiviazione locale e altro ancora.

## <a name="configure-persistent-volumes"></a>Configurare volumi permanenti

Il modo in cui un cluster di big data di SQL Server utilizza questi volumi permanenti consiste nell'usare [classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/). È possibile creare classi di archiviazione diversi per tipi diversi di archiviazione e specificarli al momento della distribuzione di cluster dei big Data. È possibile configurare la classe di archiviazione e le dimensioni di attestazione di volume permanente da usare per un determinato scopo a livello di pool. Crea un cluster di big data server&#41 [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con il nome della classe di archiviazione specificato per ogni componente che richiede volumi permanenti. Quindi consente di montare i volumi permanenti corrispondenti nel pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurare le impostazioni di archiviazione del cluster di big data

Analogamente ad altre personalizzazioni, è possibile specificare le impostazioni di archiviazione nei file di configurazione del cluster in fase di distribuzione per ogni pool e il piano di controllo. Se non sono presenti impostazioni di configurazione di archiviazione nelle specifiche di pool, verranno usate le impostazioni di archiviazione di piano di controllo. Questo è un esempio della sezione di configurazione di archiviazione che è possibile includere nella specifica:

```json
    "storage": 
    {
        "usePersistentVolume": true,
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

Per usare un archivio permanente durante la distribuzione, impostare i valori delle **usePersistentVolume** chiave *true* e **className** chiave al nome della classe di archiviazione da usare per il rispettivo pool. È anche possibile personalizzare le dimensioni delle attestazioni volume permanente creato come parte della distribuzione. Come procedura consigliata, è consigliabile usare le classi di archiviazione con un *Retain* [recuperare criteri](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> Nella versione CTP 2.5, è possibile modificare archiviazione configurazione impostazione dopo la distribuzione. Inoltre, solo `ReadWriteOnce` modalità di accesso per l'intero cluster è supportata.

> [!WARNING]
> L'esecuzione senza un archivio permanente può lavorare in un ambiente di test, ma potrebbero verificarsi in un cluster non funzionali. Al riavvio del pod, i dati dei metadati e/o utente del cluster andranno perse definitivamente. Non è consigliabile eseguire questa configurazione. 

In questa sezione fornisce altri esempi su come configurare le impostazioni di archiviazione per la distribuzione del cluster SQL Server i big Data.

## <a name="aks-storage-classes"></a>Classi di archiviazione servizio contenitore di AZURE

Servizio contenitore di AZURE viene fornito con [due classi di archiviazione predefinite](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **predefinita** e **gestiti premium** insieme dinamico strumento di provisioning per loro. È possibile specificare uno di questi due o creare la propria classe di archiviazione per la distribuzione di cluster di big data con abilitata l'archiviazione permanente. Per impostazione predefinita, incorporato nel file di configurazione del cluster di aks *aks-dev-test.json* viene fornito con le configurazioni di archiviazione permanente usare **gestiti premium** classe di archiviazione.

> [!WARNING]
> Volumi permanenti creati con **predefinite** classe di archiviazione dispongono di un criterio di recupero dei *eliminare*. In modo che al momento la si elimina il cluster di big data di SQL Server, le attestazioni di volume permanente recuperare anche i volumi eliminati e quindi permanenti. **premium Managed** dispone di un criterio di recupero dei *Mantieni*. È possibile trovare ulteriori informazioni sulle classi di archiviazione nel servizio contenitore di AZURE e le relative configurazioni nelle [ciò](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) articolo.


## <a name="minikube-storage-class"></a>Classe di archiviazione Minikube

Minikube dotato di una classe di archiviazione predefinito denominata **standard** insieme a un strumento di provisioning dinamico appositamente. La configurazione compilata nel file per minikube *minikube-dev-test.json* presenta le impostazioni di configurazione di archiviazione nella specifica di piano di controllo. Le stesse impostazioni verranno applicate a tutte le specifiche di pool. È anche possibile personalizzare una copia di questo file e usarlo per la distribuzione del cluster di big data su minikube. Manualmente, è possibile modificare il file personalizzato e modificare le dimensioni delle attestazioni volumi permanenti per i pool specifici supportare i carichi di lavoro da eseguire. O, per vedere la sezione esempi su come eseguire le modifiche mediante *mssqlctl* comandi.

## <a name="kubeadm-storage-classes"></a>Classi di archiviazione Kubeadm

Kubeadm non viene fornito con una classe di archiviazione predefinito. È necessario creare classi di archiviazione e volumi permanenti con archiviazione locale o strumento di provisioning preferito, ad esempio [torre](https://github.com/rook/rook). In tal caso, imposterebbe il **className** alla classe di archiviazione è stato configurato. 

> [!NOTE]
> In incorporato nel file di configurazione di distribuzione per kubeadm *kubeadm-dev-test.json*, il valore predefinito per **usePersistentVolume** chiave è *true*, pertanto è necessario impostare il valore per la **className** in caso contrario, avrà esito negativo le convalide di pre-distribuzione. La distribuzione ha anche un passaggio di convalida che controlla l'esistenza della classe di archiviazione, ma non per i necessari volumi permanenti. È necessario assicurarsi di che creare sufficiente volumi a seconda della scalabilità del cluster. In CTP2.5, per la dimensione del cluster è necessario creare almeno 23 volumi. [Di seguito](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) è riportato un esempio su come creare volumi permanenti con strumento di provisioning locale.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizzare le configurazioni di archiviazione per ogni pool

Per tutte le personalizzazioni, è innanzitutto necessario creare una copia di incorporato nel file di configurazione da usare. Ad esempio, il comando seguente crea una copia del *aks-dev-test.json* file di configurazione di distribuzione nella directory corrente:

```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```

Quindi, è possibile personalizzare il file config modificandola manualmente oppure è possibile usare *gruppo di sezione di configurazione di cluster mssqlctl* comando. Questo set di comandi Usa una combinazione di librerie jsonpath e jsonpatch per fornire modi per modificare il file di configurazione.

### <a name="configure-size"></a>Configurare le dimensioni

Per impostazione predefinita, la dimensione delle attestazioni volume permanente sottoposta a provisioning per ognuno dei POD effettuato il provisioning del cluster è 10 GB. È possibile aggiornare questo valore per supportare i carichi di lavoro che viene eseguito in un file di configurazione personalizzato prima della distribuzione del cluster.

L'esempio seguente aggiorna solo le dimensioni di volume permanente attestazioni nel pool di archiviazione a 32Gi:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.size=32Gi"
```

L'esempio seguente aggiorna la dimensione di attestazioni di volume permanente per tutti i pool di 32Gi:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type[*])].spec.storage.size=32Gi"
```

### <a name="configure-storage-class"></a>Configura classe di archiviazione

Esempio seguente viene illustrato come modificare la classe di archiviazione per il piano di controllo:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.controlPlace.spec.storage.className=<yourStorageClassName>"
```

Un'altra opzione è necessario modificare manualmente il file di configurazione personalizzato o usare jsonpatch, come nell'esempio seguente che modifica la classe di archiviazione per pool di archiviazione. Creare un *patch.json* file con questo contenuto:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "replicas": 2,
        "type": "Storage",
        "storage": {
          "usePersistentVolume": true,
          "accessMode": "ReadWriteOnce",
          "className": "<yourStorageClassName>",
          "size": "32Gi"
        }
      }
    }
  ]
}
```

Applicare il file della patch. Uso *gruppo di sezione di configurazione di cluster mssqlctl* comando per applicare le modifiche nel file di patch di JSON. Nell'esempio seguente applica il file patch.json un custom.json file configurazione di destinazione distribuzione.

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per una documentazione completa sui volumi in Kubernetes, vedere la [documentazione di Kubernetes in volumi](https://kubernetes.io/docs/concepts/storage/volumes/).

Per altre informazioni sulla distribuzione di un cluster di big data di SQL Server, vedere [come distribuire SQL Server del cluster di big data in Kubernetes](deployment-guidance.md).

