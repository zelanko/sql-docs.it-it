---
title: Salvataggio permanente dei dati in Kubernetes
titleSuffix: SQL Server big data clusters
description: Informazioni sul funzionamento del salvataggio permanente dei dati in un cluster Big Data di SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 87f0e82d0e12656bb7a06be1951874b656dbf4b0
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532393"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Salvataggio permanente dei dati con un cluster Big Data di SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

I [volumi permanenti](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) offrono un modello plug-in per l'archiviazione in Kubernetes. Il modo in cui viene fornita archiviazione è astratto rispetto al modo in cui viene utilizzata. Di conseguenza, è possibile usare la propria risorsa di archiviazione a disponibilità elevata e collegarla al cluster Big Data di SQL Server. In questo modo, si ottiene il controllo completo sul tipo di archiviazione, sulla disponibilità e sulle prestazioni necessari. Kubernetes supporta vari tipi di soluzioni di archiviazione, tra cui dischi/file di Azure, NFS, archiviazione locale e altro ancora.

## <a name="configure-persistent-volumes"></a>Configurare volumi permanenti

Un cluster Big Data di SQL Server utilizza questi volumi permanenti tramite [classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/). È possibile creare classi di archiviazione diverse per diversi tipi di archiviazione e specificarle in fase di distribuzione del cluster Big Data. È possibile configurare la classe di archiviazione e la dimensione dell'attestazione di volume permanente da usare per uno scopo specifico a livello di pool. Un cluster Big Data di SQL Server crea [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con il nome della classe di archiviazione specificato per ogni componente che richiede volumi permanenti. Monta quindi i volumi permanenti corrispondenti nel pod. 

Ecco alcuni aspetti importanti di cui tenere conto quando si pianifica la configurazione dell'archiviazione per il cluster Big Data:

- Per una corretta distribuzione del cluster Big Data, è necessario verificare che sia disponibile la quantità necessaria di volumi permanenti. Se si esegue la distribuzione in un cluster del servizio Azure Kubernetes e si usa una delle classi di archiviazione predefinite (`default` o `managed-premium`), queste classi supportano il provisioning dinamico per i volumi permanenti. Di conseguenza, non è necessario creare in anticipo i volumi permanenti, ma è necessario assicurarsi che i nodi di lavoro disponibili nel cluster del servizio Azure Kubernetes possano collegare il numero necessario di dischi come volumi permanenti per la distribuzione. A seconda delle [dimensioni delle macchine virtuali](/azure/virtual-machines/linux/sizes/) specificate per i nodi di lavoro, ogni nodo può collegare un determinato numero di dischi. Per un cluster con dimensioni predefinite (senza disponibilità elevata), sono necessari almeno 24 dischi. Se si abilita la disponibilità elevata o si aumentano i pool, è necessario assicurare almeno due volumi permanenti per ogni replica aggiuntiva, indipendentemente dalla risorsa che si intende aumentare.

- Se lo strumento di provisioning dell'archiviazione per la classe di archiviazione fornita nella configurazione non supporta il provisioning dinamico, è necessario creare in anticipo i volumi permanenti. Ad esempio, lo strumento di provisioning `local-storage` non consente il provisioning dinamico. Vedere questo [script di esempio](https://github.com/microsoft/sql-server-samples/tree/cu1-bdc/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) per informazioni su come eseguire questa operazione in un cluster Kubernetes distribuito con `kubeadm`.

- Quando si distribuisce un cluster Big Data, è possibile configurare la stessa classe di archiviazione perché venga usata da tutti i componenti del cluster. Tuttavia, come procedura consigliata per una distribuzione di produzione, diversi componenti richiederanno configurazioni di archiviazione diverse per gestire i vari carichi di lavoro in termini di dimensioni o velocità effettiva. È possibile sovrascrivere la configurazione dell'archiviazione predefinita specificata nel controller per ognuna delle istanze master di SQL Server e per i pool di dati e di archiviazione. Questo articolo fornisce alcuni esempi su come eseguire questa operazione.

- Dalla versione SQL Server 2019 CU1 non è possibile modificare l'impostazione di configurazione dell'archiviazione dopo la distribuzione. Sono incluse non solo qualsiasi modifica alle dimensioni dell'attestazione di volume permanente per ogni istanza, ma anche la scalabilità delle operazioni in seguito alla distribuzione. Di conseguenza, la pianificazione del layout di archiviazione prima della distribuzione del cluster Big Data è un aspetto molto importante.

- A causa della natura della distribuzione in Kubernetes come applicazioni in contenitori e dell'uso di funzionalità come set con stato e archiviazione permanente, Kubernetes garantisce che i pod vengano riavviati in caso di problemi di integrità e collegati alla stessa risorsa di archiviazione permanente. Tuttavia, in caso di errori del nodo e se il pod deve essere riavviato in un altro nodo, aumenta il rischio di non disponibilità se l'archiviazione è locale per il nodo in errore. Per ovviare a questo rischio, è necessario configurare ridondanza aggiuntiva e abilitare [funzionalità di disponibilità elevata](deployment-high-availability.md) oppure usare l'archiviazione con ridondanza remota. Ecco una panoramica delle opzioni di archiviazione per i diversi componenti nei cluster Big Data.

| Risorse | Tipo di archiviazione per i dati | Tipo di archiviazione per i log |  Note |
|---|---|---|--|
| Istanza master di SQL Server | Archiviazione con ridondanza locale (repliche >= 3) o remota (replica = 1) | Archiviazione locale | Un'implementazione basata su set con stato in cui i pod restano negli stessi nodi evita che il riavvio o eventuali errori temporanei causino la perdita di dati. |
| Pool di calcolo | Archiviazione locale* | Archiviazione locale | Dati utente non archiviati. |
| Pool di dati | Archiviazione con ridondanza locale/remota | Archiviazione locale | Usare l'archiviazione con ridondanza remota se il pool di dati non può essere ricreato da altre origini dati.  |
| Pool di archiviazione (HDFS) | Archiviazione con ridondanza locale/remota | Archiviazione locale | La replica HDFS è abilitata. |
| Pool Spark | Archiviazione locale* | Archiviazione locale | Dati utente non archiviati. |
| Controllo (controldb, metricsdb, logsdb)| Archiviazione con ridondanza remota | Archiviazione locale | Essenziale per l'uso di ridondanza a livello di archiviazione per i metadati del cluster Big Data. |

> [!IMPORTANT]
> È necessario verificare che i componenti correlati al controllo usino l'archiviazione con ridondanza remota. Il pod `controldb-0` ospita un'istanza di SQL Server con database che archiviano tutti i metadati sugli stati del servizio cluster, diverse impostazioni e così via. La mancata disponibilità di questa istanza provocherà problemi di integrità in altri servizi dipendenti nel cluster.

## <a name="configure-big-data-cluster-storage-settings"></a>Configurare le impostazioni di archiviazione del cluster Big Data

Analogamente ad altre personalizzazioni, è possibile specificare le impostazioni di archiviazione nei file di configurazione del cluster in fase di distribuzione per ogni pool nel file di configurazione `bdc.json` e per i servizi di controllo nel file `control.json`. Se le specifiche del pool non includono impostazioni di configurazione dell'archiviazione, verranno usate le impostazioni di archiviazione di controllo per tutti gli altri componenti, tra cui l'istanza master di SQL Server (risorsa `master`), HDFS (risorsa `storage-0`) o il pool di dati. Questo è un esempio della sezione di configurazione dell'archiviazione che è possibile includere nella specifica:

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

> [!WARNING]
> L'esecuzione senza archiviazione permanente può funzionare in un ambiente di test, ma può causare il mancato funzionamento del cluster. Al riavvio del pod, i metadati del cluster e/o i dati utente andranno persi in modo permanente. Non è consigliabile usare questa configurazione per l'esecuzione. 

La sezione [Configurare l'archiviazione](#config-samples) contiene altri esempi su come configurare le impostazioni di archiviazione per la distribuzione del cluster Big Data di SQL Server.

## <a name="aks-storage-classes"></a>Classi di archiviazione del servizio Azure Kubernetes

Il servizio Azure Kubernetes include [due classi di archiviazione predefinite](/azure/aks/azure-disks-dynamic-pv/), `default` e `managed-premium` insieme allo strumento di provisioning dinamico per entrambe. È possibile specificare una delle due per creare una classe di archiviazione personalizzata per la distribuzione del cluster Big Data con archiviazione permanente abilitata. Per impostazione predefinita, il file di configurazione predefinito del cluster per `aks-dev-test` del servizio Azure Kubernetes include configurazioni dell'archiviazione permanente per l'uso della classe di archiviazione `default`.

> [!WARNING]
> I volumi permanenti creati con le classi di archiviazione predefinite `default` e `managed-premium` usano il criterio di recupero *Delete*. Di conseguenza, quando si elimina il cluster Big Data di SQL Server, vengono eliminati anche le attestazioni di volumi permanenti e quindi i volumi permanenti. È possibile creare classi di archiviazione personalizzate usando lo strumento di provisioning `azure-disk` con un criterio di recupero `Retain`, come mostrato in [questo](/azure/aks/concepts-storage/#storage-classes) articolo.

## <a name="storage-classes-for-kubeadm-clusters"></a>Classi di archiviazione per cluster `kubeadm` 

I cluster Kubernetes distribuiti con `kubeadm` non includono una classe di archiviazione predefinita. È necessario creare classi di archiviazione personalizzate e volumi permanenti usando l'archiviazione locale o lo strumento di provisioning preferito, ad esempio [Rook](https://github.com/rook/rook). In questo caso, è necessario impostare `className` sulla classe di archiviazione configurata. 

> [!NOTE]
>  Nel file di configurazione della distribuzione predefinito per kubeadm (`kubeadm-dev-test` o `kubeadm-prod`) non è specificato alcun nome di classe di archiviazione per l'archiviazione di dati e log. Prima della distribuzione, è necessario personalizzare il file di configurazione e impostare il valore di className, altrimenti le convalide precedenti alla distribuzione non riusciranno. La distribuzione prevede anche un passaggio di convalida che controlla l'esistenza della classe di archiviazione, ma non i volumi permanenti necessari. È necessario assicurarsi di creare volumi sufficienti in base alla scala del cluster. Per le dimensioni minime predefinite del cluster (scalabilità predefinita, nessuna disponibilità elevata), è necessario creare almeno 24 volumi permanenti. [Qui](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) è disponibile un esempio di come creare volumi permanenti tramite uno strumento di provisioning locale.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizzare le configurazioni di archiviazione per ogni pool

Per tutte le personalizzazioni, è necessario innanzitutto creare una copia del file di configurazione predefinito che si vuole usare. Ad esempio, il comando seguente crea una copia dei file di configurazione della distribuzione `aks-dev-test` in una sottodirectory denominata `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Vengono creati due file, `bdc.json` e `control.json`, che possono essere personalizzati modificandoli manualmente oppure usando il comando `azdata bdc config`. È possibile usare una combinazione di librerie jsonpath e jsonpatch per fornire modi per modificare i file di configurazione.


### <a id="config-samples"></a> Configurare il nome della classe di archiviazione e/o le dimensioni delle attestazioni

Per impostazione predefinita, la dimensione delle attestazioni di volume permanente di cui è stato effettuato il provisioning per ognuno dei pod di cui è stato effettuato il provisioning nel cluster è 10 GB. È possibile aggiornare questo valore in base ai carichi di lavoro in esecuzione in un file di configurazione personalizzato prima della distribuzione del cluster.

L'esempio seguente aggiorna la dimensione delle attestazioni di volume permanente a 32Gi nel file `control.json`. Se non viene sostituita a livello di pool, questa impostazione verrà applicata a tutti i pool:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

L'esempio seguente mostra come modificare la classe di archiviazione per il file `control.json`:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Un'altra opzione consiste nel modificare manualmente il file di configurazione personalizzato o usare il file di patch JSON, come nell'esempio seguente, che modifica la classe di archiviazione per il pool di archiviazione. Creare un file `patch.json` con questo contenuto:

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

Applicare il file di patch. Usare il comando `azdata bdc config patch` per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file `patch.json` a un file di configurazione della distribuzione di destinazione `custom.json`.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per la documentazione completa sui volumi in Kubernetes, vedere la [documentazione di Kubernetes sui volumi](https://kubernetes.io/docs/concepts/storage/volumes/).

Per altre informazioni sulle distribuzioni di un cluster Big Data di SQL Server, vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md).
