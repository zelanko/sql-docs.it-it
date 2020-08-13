---
title: Controllo degli accessi in base al ruolo di Kubernetes
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive come i cluster Big Data di SQL Server usano il controllo degli accessi in base al ruolo con Kubernetes.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d2e3f379402f16f32020f9cd34103919f13a30c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552976"
---
# <a name="kubernetes-rbac-model--impact-on-users-managing-bdc"></a>Modello di controllo degli accessi in base al ruolo di Kubernetes e impatto sugli utenti che gestiscono i cluster BDC

La sezione seguente illustra le autorizzazioni necessarie per gli utenti che gestiscono i cluster Big Data (BDC).

> [!NOTE]
> Per altre risorse sul modello di controllo degli accessi in base al ruolo di Kubernetes, vedere [Using RBAC Authorization - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) (Uso dell'autorizzazione di controllo degli accessi in base al ruolo - Kubernetes) e [Using RBAC to define and apply permissions - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html) (Uso del controllo degli accessi in base al ruolo per definire e applicare le autorizzazioni - OpenShift).

## <a name="role-required-for-deployment"></a>Ruolo necessario per la distribuzione

Il cluster BDC usa gli account del servizio (ad esempio `sa-mssql-controller` o `master`) per orchestrare il provisioning dei pod, dei servizi, della disponibilità elevata, del monitoraggio del cluster e così via. Quando viene avviata la distribuzione del cluster BDC (ad esempio, `azdata bdc create`), `azdata` esegue le operazioni seguenti:

1. Verifica se lo spazio dei nomi specificato esiste.
2. Se non esiste, ne crea uno e applica l'etichetta `MSSQL_CLUSTER`.
3. Crea l'account del servizio `sa-mssql-controller`.
4. Crea un ruolo `<namespaced>-admin` con autorizzazioni complete per lo spazio dei nomi o il progetto ma non con autorizzazioni a livello di cluster.
5. Crea un'assegnazione di tale account del servizio al ruolo.

Una volta completati questi passaggi, viene effettuato il provisioning dei pod del piano di controllo e l'account del servizio distribuisce la parte restante del cluster Big Data.  

Di conseguenza, l'utente che esegue la distribuzione deve avere le autorizzazioni per:

- Elencare gli spazi dei nomi nel cluster (1).
- Applicare una patch allo spazio dei nomi nuovo o esistente con l'etichetta (2).
- Creare l'account del servizio `sa-mssql-controller`, il ruolo `<namespaced>-admin` e l'associazione di ruolo (3-5).

Il ruolo `admin` predefinito non dispone di queste autorizzazioni, pertanto l'utente che distribuisce il cluster Big Data deve disporre almeno delle autorizzazioni di amministratore a livello di spazio dei nomi.

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>Ruolo del cluster necessario per la raccolta di metriche di pod e nodi

A partire da SQL Server 2019 CU5, Telegraf richiede un account del servizio con autorizzazioni di ruolo a livello di cluster per raccogliere le metriche relative a pod e nodi. Durante la distribuzione (o l'aggiornamento delle distribuzioni esistenti), viene effettuato un tentativo di creare l'account del servizio e il ruolo del cluster necessari. Se tuttavia l'utente che distribuisce il cluster o esegue l'aggiornamento non dispone di autorizzazioni sufficienti, la distribuzione (o l'aggiornamento) verrà comunque completata con un avviso. In questo caso, le metriche di pod e nodi non verranno raccolte. L'utente che distribuisce il cluster deve rivolgersi a un amministratore del cluster per creare il ruolo e l'account del servizio (prima o dopo la distribuzione o l'aggiornamento). Una volta creati, vengono usati dal cluster BDC. 

Ecco uno script che mostra come creare gli artefatti necessari:

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

L'account del servizio, il ruolo del cluster e l'associazione del ruolo del cluster possono essere creati prima o dopo la distribuzione del cluster BDC. Kubernetes aggiorna automaticamente l'autorizzazione per l'account del servizio Telegraf. Se questi artefatti vengono creati come una distribuzione di pod, verrà visualizzato un ritardo di pochi minuti nelle metriche di pod e nodi raccolte.

> [!NOTE]
> SQL Server 2019 CU5 ha introdotto due opzioni di funzionalità per controllare la raccolta di metriche di pod e nodi. Per impostazione predefinita, questi parametri sono impostati su true in tutte le destinazioni dell'ambiente, ad eccezione di OpenShift, in cui viene eseguito l'override del valore predefinito. 

È possibile personalizzare queste impostazioni nella sezione relativa alla sicurezza del file di configurazione della distribuzione `control.json`:

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

Se queste impostazioni sono impostate su `false`, il flusso di lavoro di distribuzione del cluster BDC non tenterà di creare l'account del servizio, il ruolo del cluster e l'associazione per Telegraf.
