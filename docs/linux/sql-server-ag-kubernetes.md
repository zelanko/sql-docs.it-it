---
title: Gruppi di disponibilità Always On per i contenitori che eseguono Linux
titleSuffix: SQL Server
description: Questo articolo illustra i gruppi di disponibilità nei contenitori di SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910473"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Gruppi di disponibilità Always On per i contenitori di SQL Server

SQL Server 2019 supporta i gruppi di disponibilità nei contenitori in un cluster Kubernetes. Per i gruppi di disponibilità, distribuire l'[operatore Kubernetes](https://coreos.com/blog/introducing-operators.html) di SQL Server nel cluster Kubernetes. L'operatore facilita le operazioni di creazione del pacchetto, distribuzione e gestione del gruppo di disponibilità in un cluster.

![Gruppo di disponibilità nel contenitore Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Nell'immagine riportata sopra, un cluster kubernetes a quattro nodi ospita un gruppo di disponibilità con tre repliche. La soluzione include i componenti seguenti:

* Una [*distribuzione*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) di Kubernetes. La distribuzione include l'operatore e una mappa di configurazione, che forniscono l'immagine del contenitore, il software e le istruzioni necessarie per distribuire le istanze di SQL Server per il gruppo di disponibilità.

* Tre nodi, ognuno dei quali ospita un oggetto [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). L'oggetto StatefulSet contiene un [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Ogni pod contiene:
  * Un contenitore di SQL Server che esegue un'istanza di SQL Server.
  * Un agente del gruppo di disponibilità. 

* Due [*ConfigMap*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) correlati al gruppo di disponibilità. I ConfigMap forniscono informazioni su:
  * La distribuzione per l'operatore.
  * Gruppo di disponibilità.

 * I [*volumi permanenti*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) sono spazi di archiviazione. Una *richiesta di volume permanente* è una richiesta di spazio di archiviazione da parte di un utente. Ogni contenitore è associato a una richiesta di volume permanente per l'archiviazione di dati e log. Nel servizio Azure Kubernetes si [crea una richiesta di volume permanente](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) per effettuare automaticamente il provisioning di spazio di archiviazione in base a una classe di archiviazione.


Inoltre, il cluster archivia i [*segreti*](https://kubernetes.io/docs/concepts/configuration/secret/) per le password, i certificati, le chiavi e altre informazioni riservate.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Distribuire il gruppo di disponibilità in Kubernetes

Per distribuire un gruppo di disponibilità in Kubernetes:

1. Creare il cluster Kubernetes

   Per un gruppo di disponibilità, creare almeno tre nodi per SQL Server più un nodo per il master.

1. Distribuire l'operatore

1. Configurare l'archiviazione

1. Distribuire l'oggetto StatefulSet

   L'operatore resta in ascolto delle istruzioni per la distribuzione dell'oggetto StatefulSet. Crea automaticamente le istanze di SQL Server su tre nodi distinti e configura il gruppo di disponibilità con un gestore cluster esterno.

1. Creare i database e associarli al gruppo di disponibilità

Per la procedura dettagliata, vedere [Gruppi di disponibilità Always On per i contenitori di SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operatore Kubernetes di SQL Server

Dopo la distribuzione, l'operatore registra una risorsa di SQL Server personalizzata. Usare l'operatore per distribuire questa risorsa.  Ogni risorsa corrisponde a un'istanza di SQL Server e include proprietà specifiche come `sapassword` e `monitoring policy`. L'operatore analizza la risorsa e distribuisce un oggetto StatefulSet di Kubernetes.

L'oggetto StatfulSet contiene:

* Contenitore mssql-server

* Contenitore mssql-ha-supervisor

Il codice per l'operatore, il supervisore a disponibilità elevata e SQL Server è incluso in un'immagine Docker denominata `mcr.microsoft.com/mssql/ha`. Questa immagine contiene i valori binari seguenti:

* `mssql-operator`

    Questo processo viene distribuito come distribuzione Kubernetes distinta. Registra la [risorsa personalizzata di Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) denominata `SqlServer` (sqlservers.mssql.microsoft.com). Resta quindi in attesa della creazione o dell'aggiornamento delle risorse nel cluster Kubernetes. Per ogni evento di questo tipo, crea o aggiorna le risorse di Kubernetes per l'istanza corrispondente (ad esempio l'oggetto StatefulSet o il processo `mssql-server-k8s-init-sql`).

* `mssql-server-k8s-health-agent`

    Questo server Web fornisce a Kubernetes [probe di attività](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) per determinare l'integrità di un'istanza di SQL Server. Monitora l'integrità dell'istanza di SQL Server locale chiamando `sp_server_diagnostics` e confrontando i risultati con i criteri di monitoraggio impostati.

* `mssql-ha-supervisor`

   Gestisce il certificato e l'endpoint del gruppo di disponibilità. 

* `mssql-server-k8s-ag-agent`
  
    Questo processo monitora l'integrità di una replica del gruppo di disponibilità su una singola istanza di SQL Server ed esegue i failover.

    Gestisce anche la selezione del leader.

* `mssql-server-k8s-init-sql`
  
    Questo [processo](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) di Kubernetes applica una configurazione dello stato desiderato a un'istanza di SQL Server. Il processo viene creato dall'operatore ogni volta che viene creata o aggiornata una risorsa di SQL Server. Garantisce che l'istanza di SQL Server di destinazione corrispondente alla risorsa personalizzata disponga della configurazione desiderata descritta nella risorsa.

    Ad esempio, se una o più delle impostazioni seguenti sono obbligatorie, le completa:
  * Aggiorna la password dell'amministratore di sistema
  * Crea l'account di accesso SQL per gli agenti
  * Crea l'endpoint DBM

* `mssql-server-k8s-rotate-creds`
  
    Questo processo di Kubernetes implementa l'attività di rotazione delle credenziali. Creare questo processo per richiedere l'aggiornamento della password dell'amministratore di sistema, della password dell'account di accesso SQL per gli agenti, del certificato DBM e così via. La password dell'amministratore di sistema è specificata come parametro del processo. Le altre vengono generate automaticamente.

* `mssql-server-k8s-failover`

   Processo di Kubernetes che implementa il flusso di lavoro di failover manuale.

### <a name="notes"></a>Note

Indipendentemente dalla configurazione del gruppo di disponibilità, l'operatore distribuirà sempre il supervisore a disponibilità elevata. Se la risorsa di SQL Server non elenca alcun gruppo di disponibilità, l'operatore distribuirà comunque questo contenitore.

La versione dell'immagine dell'operatore è identica a quella dell'immagine di SQL Server.

## <a name="next-steps"></a>Passaggi successivi

> [Distribuire un contenitore SQL Server in Kubernetes con il servizio Azure Kubernetes](tutorial-sql-server-containers-kubernetes.md)
