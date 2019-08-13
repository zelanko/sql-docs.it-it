---
title: Disponibilità elevata per i contenitori di SQL Server
description: Questo articolo illustra la disponibilità elevata per i contenitori di SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077484"
---
# <a name="high-availability-for-sql-server-containers"></a>Disponibilità elevata per i contenitori di SQL Server

Creare e gestire le istanze di SQL Server in modo nativo in Kubernetes.

Distribuire SQL Server in contenitori Docker gestiti da [Kubernetes](https://kubernetes.io/). In Kubernetes un contenitore con un'istanza di SQL Server può essere ripristinato automaticamente in caso di errore di un nodo del cluster. Per una disponibilità più affidabile, è possibile configurare il gruppo di disponibilità Always On di SQL Server con le istanze di SQL Server nei contenitori in un cluster Kubernetes. In questo articolo vengono confrontate le due soluzioni.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Confronto delle versioni di SQL Server in Kubernetes

SQL Server 2017 fornisce un'immagine Docker che può essere distribuita in Kubernetes. È possibile configurare l'immagine con una richiesta di volume persistente Kubernetes. Kubernetes monitora il processo di SQL Server nel contenitore. In caso di problemi di un processo, un pod, un contenitore o un nodo, Kubernetes esegue automaticamente il bootstrap di un'altra istanza ed esegue la riconnessione alla risorsa di archiviazione.

SQL Server 2019 (anteprima) introduce un'architettura più efficiente con un oggetto StatefulSet Kubernetes. Kubernetes orchestra le istanze di SQL Server nelle immagini del contenitore che fanno parte di un gruppo di disponibilità Always On di SQL Server. Questo modello garantisce un monitoraggio dello stato migliorato, un ripristino più veloce, backup di offload e scalabilità orizzontale in lettura.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contenitore con un'istanza di SQL Server in Kubernetes

Kubernetes 1.6 e versioni successive supportano le [*classi di archiviazione*](https://kubernetes.io/docs/concepts/storage/storage-classes/), le [*richieste di volumi persistenti*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) e il [*tipo di volume del disco di Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

In questa configurazione Kubernetes svolge il ruolo di agente di orchestrazione del contenitore. 

![Diagramma del cluster SQL Server in Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

Nel diagramma precedente `mssql-server` è un'istanza di SQL Server (contenitore) in un [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Un [set di repliche](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garantisce che il pod venga automaticamente ripristinato dopo un errore del nodo. Le applicazioni si connettono al servizio. In questo caso, il servizio rappresenta un servizio di bilanciamento del carico che ospita un indirizzo IP che rimane invariato dopo l'errore di `mssql-server`.

Kubernetes orchestra le risorse nel cluster. Quando si verifica un errore in un nodo che ospita un contenitore con un'istanza di SQL Server, viene eseguito il bootstrap di un nuovo contenitore con un'istanza di SQL Server e viene collegato alla stessa risorsa di archiviazione permanente.

SQL Server 2017 e versioni successive supportano i contenitori in Kubernetes.

Per creare un contenitore in Kubernetes, vedere [Distribuire un contenitore SQL Server in Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Gruppo di disponibilità Always On di SQL Server in contenitori di SQL Server in Kubernetes

SQL Server 2019 supporta i gruppi di disponibilità nei contenitori in Kubernetes. Per i gruppi di disponibilità, distribuire l'[operatore Kubernetes](https://coreos.com/blog/introducing-operators.html) di SQL Server nel cluster Kubernetes. L'operatore facilita le operazioni di creazione del pacchetto, distribuzione e gestione delle istanze di SQL Server e del gruppo di disponibilità in un cluster.

![Gruppo di disponibilità nel contenitore Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Nell'immagine riportata sopra, un cluster kubernetes a quattro nodi ospita un gruppo di disponibilità con tre repliche. La soluzione include i componenti seguenti:

* Una [*distribuzione*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) di Kubernetes. La distribuzione include l'operatore e una mappa di configurazione. La distribuzione descrive l'immagine del contenitore, il software e le istruzioni necessarie per distribuire le istanze di SQL Server per il gruppo di disponibilità.

* Tre nodi, ognuno dei quali ospita un oggetto [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). L'oggetto StatefulSet contiene un pod. Ogni pod contiene:
  * Un contenitore di SQL Server che esegue un'istanza di SQL Server.
  * Un supervisore `mcr.microsoft.com/mssql/ha` per gestire il gruppo di disponibilità.

* Due [*ConfigMap*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) correlati al gruppo di disponibilità. I ConfigMap forniscono informazioni su:
  * La distribuzione per l'operatore.
  * Gruppo di disponibilità.

 * I volumi permanenti per ogni istanza di SQL Server forniscono lo spazio di archiviazione per i file di dati e di log.

Inoltre, il cluster archivia i [*segreti*](https://kubernetes.io/docs/concepts/configuration/secret/) per le password, i certificati, le chiavi e altre informazioni riservate.

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>Confronto della disponibilità elevata di SQL Server nei contenitori con e senza il gruppo di disponibilità

Nella tabella seguente vengono confrontate le capacità per la disponibilità elevata di SQL Server nei contenitori in Kubernetes con e senza un gruppo di disponibilità:

| |Con un gruppo di disponibilità | Istanza di contenitore autonoma<br/> Nessun gruppo di disponibilità
|:------|:------|:------
|Ripristino automatico in caso di errore del nodo | Sì | Sì
|Ripristino automatico in caso di errore del pod | Sì | Sì
|Failover più veloce |Sì |
|Ripristino automatico in caso di errore dell'istanza di SQL Server | Sì | 
|Ripristino automatico in caso di errore del controllo di integrità del database | Sì | 
|Fornire repliche di sola lettura | Sì |
|Backup della replica secondaria | Sì | 
|Esecuzione come oggetto StatefulSet | Sì | 

Una differenza fondamentale è che il tempo di ripristino (o di failover) è più rapido con un gruppo di disponibilità rispetto a una singola istanza di SQL Server in un contenitore. Questo miglioramento è dovuto al fatto che il gruppo di disponibilità di SQL Server mantiene repliche secondarie in altri nodi del cluster. Durante il failover, una replica secondaria viene selezionata e alzata di livello come primaria. Le applicazioni connesse al servizio vengono reindirizzate alla nuova replica primaria.

Senza il gruppo di disponibilità, quando Kubernetes rileva un failover, deve creare il contenitore, connetterlo alla risorsa di archiviazione e quindi riconnettere le applicazioni connesse al servizio. Il tempo esatto di failover dipende dal punto in cui si è verificato il failover e dal modo in cui è stato rilevato. 

In genere, il tempo di failover per un gruppo di disponibilità viene misurato in secondi, mentre il tempo di failover per il recupero di un contenitore con una singola istanza può arrivare a 10 minuti.

## <a name="next-steps"></a>Passaggi successivi

Per distribuire contenitori di SQL Server nel servizio Azure Kubernetes, vedere gli esempi seguenti:

* [Distribuire SQL Server in un contenitore Docker](sql-server-linux-configure-docker.md)
* [Distribuire un contenitore di SQL Server in Kubernetes](tutorial-sql-server-containers-kubernetes.md)
* [Gruppi di disponibilità Always On per i contenitori SQL Server](sql-server-ag-kubernetes.md)

