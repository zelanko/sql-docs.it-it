---
title: Gruppi di disponibilità per i contenitori che eseguono Linux
titleSuffix: SQL Server
description: Questo articolo introduce i gruppi di disponibilità nei contenitori di SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e778af484881ae26669d2bac952b568532300c93
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833032"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Gruppi di disponibilità per i contenitori di SQL Server

SQL Server 2019 supporta gruppi di disponibilità in contenitori in un cluster Kubernetes. Per i gruppi di disponibilità, distribuire il Server SQL [Kubernetes operatore](https://coreos.com/blog/introducing-operators.html) al cluster Kubernetes. L'operatore consente di creare pacchetti, distribuire e gestire il gruppo di disponibilità in un cluster.

![Gruppo di disponibilità nel contenitore Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Nell'immagine precedente, un cluster di quattro nodi kubernetes ospitato un gruppo di disponibilità con tre repliche. La soluzione include i componenti seguenti:

* Kubernetes [ *distribuzione*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). La distribuzione include l'operatore e una mappa di configurazione. Queste forniscono l'immagine del contenitore, software e le istruzioni necessarie per distribuire le istanze di SQL Server per il gruppo di disponibilità.

* Tre nodi, ognuno dei quali ospita un [ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). L'oggetto StatefulSet contiene un [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Ogni pod contiene:
  * Un contenitore di SQL Server in esecuzione un'istanza di SQL Server.
  * Un agente del gruppo di disponibilità. 

* Due [ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) correlate al gruppo di disponibilità. Il ConfigMaps forniscono informazioni su:
  * La distribuzione per l'operatore.
  * Gruppo di disponibilità.

 * [*Volumi permanenti* ](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) sono parti di archiviazione. Oggetto *attestazione di volume permanente* (PVC) è una richiesta per l'archiviazione da un utente. Ogni contenitore è associato a un'attestazione di volume permanente per l'archiviazione dati e di log. In Azure Kubernetes Service (AKS), si [creare un'attestazione di volume permanente](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) a automaticamente il provisioning dell'archiviazione basato su una classe di archiviazione.


Inoltre, il cluster memorizza [ *segreti* ](https://kubernetes.io/docs/concepts/configuration/secret/) per le password, certificati, chiavi e altre informazioni riservate.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Distribuire il gruppo di disponibilità in Kubernetes

Per distribuire un gruppo di disponibilità in Kubernetes:

1. Creare il cluster Kubernetes

   Per un gruppo di disponibilità, creare almeno tre nodi per SQL Server oltre a un nodo per il servizio master.

1. Distribuire l'operatore

1. Configurare l'archiviazione

1. Distribuire l'oggetto StatefulSet

   L'operatore è in ascolto per le istruzioni per distribuire l'oggetto StatefulSet. Crea le istanze di SQL Server in tre nodi separati e configurato automaticamente del gruppo di disponibilità con un manager di cluster external.

1. Creare i database e allegarli al gruppo di disponibilità

Per informazioni dettagliate, vedere [i gruppi di disponibilità per i contenitori di SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operatore di SQL Server Kubernetes

Dopo aver distribuito l'operatore, registra una risorsa di SQL Server personalizzata. Usare l'operatore per distribuire questa risorsa.  Ogni risorsa corrisponde a un'istanza di SQL Server e include le proprietà specifiche, ad esempio `sapassword` e `monitoring policy`. L'operatore analizza la risorsa e distribuisce un Kubernetes StatefulSet.

Il StatfulSet contiene:

* contenitore MSSQL-server

* contenitore MSSQL-disponibilità elevata-supervisor

Il codice per l'operatore, supervisor a disponibilità elevata e SQL Server viene compresso in un'immagine Docker denominata `mcr.microsoft.com/mssql/ha`. Questa immagine contiene i file binari seguenti:

* `mssql-operator`

    Questo processo viene distribuito come una distribuzione di Kubernetes distinta. Registra il [risorsa personalizzata di Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) chiamato `SqlServer` (sqlservers.mssql.microsoft.com). Quindi rimane in ascolto per tali risorse viene creato o aggiornato nel cluster Kubernetes. Per ogni evento, crea o aggiorna le risorse di Kubernetes per l'istanza corrispondente (ad esempio l'oggetto StatefulSet, o `mssql-server-k8s-init-sql` processo).

* `mssql-server-k8s-health-agent`

    Il server web serve Kubernetes [probe attività](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) per determinare l'integrità di un'istanza di SQL Server. Monitora l'integrità dell'istanza di SQL Server locale tramite una chiamata `sp_server_diagnostics` e confrontare i risultati con i criteri di monitoraggio.

* `mssql-ha-supervisor`

   Gestisce il certificato del gruppo di disponibilità e l'endpoint. 

* `mssql-server-k8s-ag-agent`
  
    Questo processo consente di monitorare l'integrità di una replica del gruppo di disponibilità in una singola istanza di SQL Server ed esegue i failover.

    Mantiene anche la designazione leader.

* `mssql-server-k8s-init-sql`
  
    Questo Kubernetes [processo](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) applicherà una configurazione DSC a un'istanza di SQL Server. Il processo viene creato dall'operatore ogni volta che una risorsa di SQL Server viene creata o aggiornata. Assicura che l'istanza di SQL Server di destinazione corrispondente per la risorsa personalizzata disponga della configurazione desiderata descritta nelle sezioni della risorsa.

    Ad esempio, se le impostazioni seguenti sono necessari, li completa:
  * Aggiornare la password dell'amministratore di sistema
  * Crea l'account di accesso SQL per gli agenti
  * Crea l'endpoint di mirroring del database

* `mssql-server-k8s-rotate-creds`
  
    Questo processo Kubernetes implementa l'attività di ruotare le credenziali. Creare questo processo per richiedere aggiornamenti per la password dell'account SA, password di accesso SQL agent, cert di mirroring del database, e così via. Viene specificata la password account SA come i parametri del processo. Gli altri vengono generati automaticamente.

* `mssql-server-k8s-failover`

   Un processo di Kubernetes che implementa il flusso di lavoro di failover manuale.

### <a name="notes"></a>Note

Indipendentemente dalla configurazione del gruppo di disponibilità, l'operatore distribuirà sempre il Supervisore a disponibilità elevata. Se la risorsa di SQL Server non è elencato alcun gruppo di disponibilità, l'operatore venga distribuita in questo contenitore.

La versione dell'immagine dell'operatore è identica a quella per l'immagine di SQL Server.

## <a name="next-steps"></a>Passaggi successivi

> [Contenitore di SQL Server in Kubernetes](tutorial-sql-server-containers-kubernetes.md)
