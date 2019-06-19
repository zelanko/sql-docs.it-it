---
title: Disponibilità elevata per i contenitori di SQL Server
description: Questo articolo presenta la disponibilità elevata per i contenitori di SQL Server
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 93e377fc187968b031438ccd896e29b7ebff4144
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713200"
---
# <a name="high-availability-for-sql-server-containers"></a>Disponibilità elevata per i contenitori di SQL Server

Creare e gestire le istanze di SQL Server in modo nativo in Kubernetes.

Distribuire SQL Server in contenitori docker gestiti da [Kubernetes](https://kubernetes.io/). In Kubernetes, un contenitore con un'istanza di SQL Server possa ripristinare automaticamente nel caso in cui un nodo del cluster ha esito negativo. Per la disponibilità più affidabile, configurare SQL Server Always On gruppo di disponibilità con istanze di SQL Server in contenitori in un cluster Kubernetes. Questo articolo confronta le due soluzioni.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Confrontare le versioni di SQL Server in Kubernetes

SQL Server 2017 offre un'immagine Docker che possono essere distribuiti in Kubernetes. È possibile configurare l'immagine con un'attestazione di volume permanente Kubernetes (attestazione di volume permanente). Kubernetes consente di monitorare il processo di SQL Server nel contenitore. Se il nodo, pod, contenitore o processo ha esito negativo, Kubernetes automaticamente avvia un'altra istanza e la riconnessione alla risorsa di archiviazione.

SQL Server 2019 (anteprima) introduce un'architettura più affidabile con una Kubernetes StatefulSet. Kubernetes Orchestra le istanze di SQL Server in immagini del contenitore che fanno parte di un SQL Server gruppo di disponibilità AlwaysOn. Questo modello offre il monitoraggio dell'integrità migliorate, più veloce, l'offload backup e il recupero scalabilità orizzontale in lettura.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contenitore con l'istanza di SQL Server in Kubernetes

Include il supporto per Kubernetes 1.6 e versioni successive [ *classi di archiviazione*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [ *attestazioni di volume permanente*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)e il [  *Tipo di volume di disco di Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

In questa configurazione, Kubernetes svolgerà il ruolo dell'agente di orchestrazione del contenitore. 

![Diagramma del cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

Nel diagramma precedente `mssql-server` è un'istanza di SQL Server (contenitore) in un [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Oggetto [set di repliche](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) assicura che il pod viene recuperato automaticamente dopo un errore di nodo. Applicazioni di connettono al servizio. In questo caso, il servizio rappresenta un servizio di bilanciamento del carico che ospita un indirizzo IP che rimane invariata dopo l'errore del `mssql-server`.

Kubernetes Orchestra le risorse del cluster. Quando un nodo che ospita un contenitore di istanza di SQL Server non riesce, avvia un nuovo contenitore con un'istanza di SQL Server e la collega alla stessa archiviazione permanente.

SQL Server 2017 e versioni successive supporto dei contenitori in Kubernetes.

Per creare un contenitore in Kubernetes, vedere [distribuire un contenitore di SQL Server in Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Un gruppo di disponibilità SQL Server Always On nei contenitori di SQL Server in Kubernetes

2019 di SQL Server supporta i gruppi di disponibilità in contenitori in Kubernetes. Per i gruppi di disponibilità, distribuire il Server SQL [Kubernetes operatore](https://coreos.com/blog/introducing-operators.html) al cluster Kubernetes. L'operatore consente di creare pacchetti, distribuire e gestire le istanze di SQL Server e il gruppo di disponibilità in un cluster.

![Gruppo di disponibilità nel contenitore Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Nell'immagine precedente, un cluster kubernetes di quattro nodi ospita un gruppo di disponibilità con tre repliche. La soluzione include i componenti seguenti:

* Kubernetes [ *distribuzione*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). La distribuzione include l'operatore e una mappa di configurazione. La distribuzione viene descritto l'immagine del contenitore, software e le istruzioni necessarie per distribuire le istanze di SQL Server per il gruppo di disponibilità.

* Tre nodi, ognuno dei quali ospita un [ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). L'oggetto StatefulSet contiene un pod. Ogni pod contiene:
  * Un contenitore di SQL Server in esecuzione un'istanza di SQL Server.
  * Un supervisore `mcr.microsoft.com/mssql/ha` per gestire il gruppo di disponibilità.

* Due [ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) correlate al gruppo di disponibilità. Il ConfigMaps forniscono informazioni su:
  * La distribuzione per l'operatore.
  * Gruppo di disponibilità.

 * Volumi permanenti per ogni istanza di SQL Server forniscono la risorsa di archiviazione per i file di dati e di log.

Inoltre, il cluster memorizza [ *segreti* ](https://kubernetes.io/docs/concepts/configuration/secret/) per le password, certificati, chiavi e altre informazioni riservate.

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>Confrontare la disponibilità elevata di SQL Server in contenitori con e senza il gruppo di disponibilità

La tabella seguente confronta le funzionalità a disponibilità elevata SQL Server in contenitori in Kubernetes con e senza un gruppo di disponibilità:

| |Con un gruppo di disponibilità | Istanza di contenitore autonoma<br/> Nessun gruppo di disponibilità
|:------|:------|:------
|Recupero automatico dagli errori di nodo | Yes | Yes
|Recuperare automaticamente da un errore di pod | Yes | Yes
|Accelerare il failover |Yes |
|Ripristinare automaticamente dall'errore dell'istanza SQL Server | Yes | 
|Recupero automatico dagli errori di controllo integrità database | Yes | 
|Fornire le repliche di sola lettura | Yes |
|Replica secondaria di backup | Yes | 
|Viene eseguito come un oggetto StatefulSet | Yes | 

Una differenza fondamentale è che il tempo di ripristino (o failover) è più velocemente con un gruppo di disponibilità rispetto a una singola istanza di SQL Server in un contenitore. Questo miglioramento è perché il gruppo di disponibilità SQL Server mantiene le repliche secondarie in altri nodi del cluster. In caso di failover, una replica secondaria è selezionata e alzare al livello primario. Le applicazioni connesse al servizio vengono reindirizzate alla nuova replica primaria.

Senza il gruppo di disponibilità, quando Kubernetes rileva un failover, è necessario creare il contenitore, connetterla alla risorsa di archiviazione e vengono riconnesse le applicazioni connesse al servizio. Il tempo di failover esatta dipende in cui è stato il failover, e come è stato rilevato. 

In genere, il tempo di failover per un gruppo di disponibilità viene misurato in secondi, mentre il tempo di failover per singola istanza per il ripristino di un contenitore può essere fino a 10 minuti.

## <a name="next-steps"></a>Passaggi successivi

Per distribuire i contenitori di SQL Server in Azure Kubernetes Service (AKS), vedere gli esempi seguenti:

* [Distribuire SQL Server nel contenitore Docker](sql-server-linux-configure-docker.md)
* [Distribuire un contenitore di SQL Server in Kubernetes](tutorial-sql-server-containers-kubernetes.md)
* [Gruppi di disponibilità per i contenitori di SQL Server](sql-server-ag-kubernetes.md)

