---
title: Monitorare e risolvere i problemi
titleSuffix: SQL Server big data clusters
description: Questo articolo include comandi utili per il monitoraggio e risoluzione dei problemi relativi a un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 3914bc088ab8974c92a24131d69590b4353f068e
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994085"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Monitoraggio e risoluzione dei problemi dei cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive alcuni comandi utili di Kubernetes che è possibile usare per monitorare e risolvere i problemi di un cluster di big data di SQL Server 2019 (anteprima). Viene illustrato come visualizzare i dettagli di un pod o altri elementi di Kubernetes che si trovano nel cluster di big data. Questo articolo descrive anche le attività comuni, ad esempio la copia dei file in o da un contenitore in esecuzione uno dei servizi cluster di big data di SQL Server.

> [!TIP]
> Eseguire il comando seguente **kubectl** comandi sul computer client Linux (bash) o Windows (cmd o PS). Richiedono precedente autenticazione nel cluster e un contesto del cluster da eseguire. Per un cluster servizio contenitore di AZURE creato in precedenza, ad esempio, è possibile eseguire `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` per scaricare il file di configurazione del cluster Kubernetes e impostare il contesto del cluster.

## <a name="get-status-of-pods"></a>Ottenere lo stato dei POD

È possibile usare il `kubectl get pods` comando per ottenere lo stato dei POD nel cluster per tutti gli spazi dei nomi o per lo spazio dei nomi del cluster di big data. Le sezioni seguenti mostrano esempi di entrambi.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostra lo stato di tutti i POD nel cluster Kubernetes

Eseguire il comando seguente per ottenere tutti i POD e i relativi stati, tra cui i POD che fanno parte dello spazio dei nomi che SQL Server vengono creati i POD del cluster di big data in:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostra lo stato di tutti i POD nel cluster di big data di SQL Server

Usare il `-n` parametro per specificare uno spazio dei nomi specifico. Si noti che i POD del cluster di SQL Server i big data vengono creati in un nuovo spazio dei nomi creato in fase di bootstrap del cluster in base al nome del cluster specificato nel file di configurazione della distribuzione. Il nome predefinito, `mssql-cluster`, qui viene usato.

```bash
kubectl get pods -n mssql-cluster
```

Si dovrebbe visualizzato un output simile all'elenco seguente per un cluster in esecuzione big data:

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> Durante la distribuzione di POD con un **lo stato** dei **ContainerCreating** ancora riaperto. Se la distribuzione si blocca per qualche motivo, questo può avere un'idea in cui il problema potrebbe essere. Si analizzino i **pronti** colonna. Queste informazioni indicano quanti contenitori è sono avviata nel pod. Si noti che le distribuzioni possono richiedere 30 minuti o più, a seconda della configurazione e la rete. Gran parte di questo tempo viene impiegata per scaricare le immagini del contenitore per i diversi componenti.

## <a name="get-pod-details"></a>Ottenere i dettagli di pod

Eseguire il comando seguente per ottenere una descrizione dettagliata di un pod specifico nell'output di formato JSON. Include informazioni dettagliate, ad esempio il nodo corrente di Kubernetes che il pod viene inserito in, i contenitori in esecuzione all'interno di pod e l'immagine usata per avviare i contenitori. Inoltre, Mostra altri dettagli, ad esempio etichette, stato e salvati in modo permanente le attestazioni di volumi che sono associate i pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

L'esempio seguente mostra i dettagli per il `master-0` pod in un cluster di big data denominato `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Se si sono verificati errori, è possibile incontrare l'errore negli eventi di recenti per i pod.

## <a name="get-pod-logs"></a>Ottenere i log di pod

È possibile recuperare i registri per contenitori in esecuzione in un pod. Il comando seguente recupera i log per tutti i contenitori in esecuzione nel pod denominato `master-0` vengono inseriti in un file denominato `master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> Ottenere lo stato dei servizi

Eseguire il comando seguente per ottenere i dettagli per i servizi cluster di big data. Questi dettagli includono il tipo e gli indirizzi IP associati con le porte e i rispettivi servizi. Si noti che i servizi cluster di SQL Server i big data vengono creati in un nuovo spazio dei nomi creato in fase di bootstrap del cluster in base al nome del cluster specificato nel file di configurazione di distribuzione.

```bash
kubectl get svc -n <namespace_name>
```

L'esempio seguente mostra lo stato per i servizi in un cluster di big data denominato `mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

I servizi seguenti supportano le connessioni esterne per i cluster di big data:

| Servizio | Descrizione |
|---|---|
| **master-svc-external** | Fornisce l'accesso all'istanza master.<br/>(**EXTERNAL-IP, 31433** e il **SA** utente) |
| **controller-svc-external** | Supporta gli strumenti e i client che gestiscono il cluster. |
| **mgmtproxy-svc-external** | Fornisce l'accesso per il [portale di amministrazione Cluster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**:30777/portal) |
| **gateway-svc-external** | Fornisce l'accesso al gateway HDFS/Spark.<br/>(**EXTERNAL-IP** e il **radice** utente) |
| **appproxy-svc-external** | Supporta gli scenari di distribuzione dell'applicazione. |

> [!TIP]
> Si tratta di un modo per visualizzare i servizi con **kubectl**, ma è anche possibile usare `mssqlctl cluster endpoint list` comando per visualizzare tali endpoint. Per altre informazioni, vedere [ottenere gli endpoint del cluster di big data](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Ottenere i dettagli del servizio

Eseguire questo comando per ottenere una descrizione dettagliata di un servizio in formato JSON output. Che include i dettagli come etichette, selettore, indirizzo IP, external-IP (se il servizio è di tipo LoadBalancer), porta e così via.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

Nell'esempio seguente recupera i dettagli per il **master-svc-external** servizio:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Eseguire i comandi in un contenitore

Se gli strumenti esistenti o dell'infrastruttura non consentono di eseguire una determinata attività senza effettivamente in corso nel contesto del contenitore, è possibile accedere al contenitore usando `kubectl exec` comando. Ad esempio, si potrebbe essere necessario verificare se esiste un file specifico, o potrebbe essere necessario riavviare i servizi nel contenitore. 

Usare il `kubectl exec` comando, usare la sintassi seguente:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

Le due sezioni seguenti forniscono due esempi di esecuzione di un comando in un contenitore specifico.

### <a id="restartsql"></a> Accedere a un contenitore specifico e riavviare il processo di SQL Server

Nell'esempio seguente viene illustrato come riavviare il processo di SQL Server nel `mssql-server` contenitore nel `master-0` pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> Accedere a un contenitore specifico e riavviare i servizi in un contenitore
 
Nell'esempio seguente viene illustrato come riavviare tutti i servizi gestiti da **supervisord**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> Copiare i file

Se è necessario copiare i file dal contenitore nel computer locale, usare `kubectl cp` comando con la sintassi seguente:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Analogamente, è possibile usare `kubectl cp` per copiare i file dal computer locale in un contenitore specifico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> Copiare i file da un contenitore

Nell'esempio seguente copia i file di log di SQL Server dal contenitore per il `~/temp/sqlserverlogs` percorso nel computer locale (in questo esempio il computer locale è un client Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> Copiare i file nel contenitore

L'esempio seguente copia il **AdventureWorks2016CTP3.bak** file dal computer locale al contenitore di istanza master di SQL Server (`mssql-server`) nella `master-0` pod. Il file viene copiato il `/tmp` directory nel contenitore. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> Eliminazione forzata un pod
 
Non è consigliabile forzare l'eliminazione un pod. Ma per il test di disponibilità, resilienza o la persistenza dei dati, è possibile eliminare un pod per simulare un errore di pod con il `kubectl delete pods` comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

L'esempio seguente elimina il pod del pool di archiviazione, `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> Ottenere l'indirizzo IP di pod
 
Per la risoluzione dei problemi, potrebbe essere necessario ottenere l'indirizzo IP del nodo di che un pod in esecuzione. Per ottenere l'indirizzo IP, usare il `kubectl get pods` comando con la sintassi seguente:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

L'esempio seguente ottiene l'indirizzo IP del nodo di `master-0` pod è in esecuzione in:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>Portale di amministrazione cluster

Usare la [portale di amministrazione cluster](cluster-admin-portal.md) per monitorare lo stato del cluster di big data. Ad esempio, durante le distribuzioni, è possibile usare la **distribuzione** scheda. È necessario attendere per il **mgmtproxy-svc-external** avvio prima di accedere a questo portale, pertanto non sarà disponibile all'inizio di una distribuzione del servizio.

## <a name="kubernetes-dashboard"></a>Dashboard di Kubernetes

È possibile avviare il dashboard di Kubernetes per altre informazioni sul cluster. Le sezioni seguenti illustrano come avviare il dashboard per Kubernetes nel servizio contenitore di AZURE e per eseguire il bootstrap utilizzando kubeadm Kubernetes.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Avviare il dashboard di quando il cluster è in esecuzione nel servizio contenitore di AZURE

Per avviare il dashboard di Kubernetes eseguire:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se viene visualizzato l'errore seguente: *Impossibile rimanere in ascolto sulla porta 8001 e: Tutti i listener non è stato possibile creare con i seguenti errori: Impossibile creare il listener: Errore di restare in ascolto tcp4 127.0.0.1:8001: > associare: In genere è consentito un solo utilizzo di ogni indirizzo del socket (indirizzo di rete/protocollo/porta). Impossibile creare il listener: Errore di restare in ascolto tcp6: indirizzo [[:: 1]]: 8001: mancante nella porta > risolvere l'errore: Impossibile rimanere in ascolto su una delle porte di richiesta: [{8001 9090}]*, assicurarsi che non è stato avviato il dashboard già da un'altra finestra.

Quando si avvia il dashboard nel browser, è possibile ottenere gli avvisi di autorizzazione a causa di RBAC viene abilitata per impostazione predefinita nei cluster servizio contenitore di AZURE e l'account di servizio utilizzato dal dashboard non dispone delle autorizzazioni sufficienti per accedere a tutte le risorse (ad esempio,  *non è consentito il Pod: Utente "del sistema: serviceaccount:kube-system: kubernetes-dashboard" non è possibile elencare i POD nello spazio dei nomi "default"*). Eseguire il comando seguente per concedere le autorizzazioni necessarie per `kubernetes-dashboard`e quindi riavviare il dashboard:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Avviare il dashboard di quando viene avviato un cluster Kubernetes automaticamente usando kubeadm

Per altre istruzioni su come distribuire e configurare il dashboard del cluster Kubernetes, vedere [la documentazione di Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Per avviare il dashboard di Kubernetes, eseguire questo comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server i big data](big-data-cluster-overview.md).
