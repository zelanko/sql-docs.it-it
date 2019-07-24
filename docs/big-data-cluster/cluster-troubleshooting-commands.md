---
title: Monitorare e risolvere i problemi
titleSuffix: SQL Server big data clusters
description: Questo articolo fornisce comandi utili per il monitoraggio e la risoluzione dei problemi di un cluster SQL Server 2019 Big Data (anteprima).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419475"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Monitoraggio e risoluzione dei problemi SQL Server cluster Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive diversi comandi di Kubernetes utili che è possibile usare per monitorare e risolvere i problemi relativi a un cluster SQL Server 2019 Big Data (anteprima). Viene illustrato come visualizzare i dettagli approfonditi di un pod o di altri elementi di Kubernetes che si trovano nel cluster Big Data. Questo articolo illustra anche le attività comuni, ad esempio la copia di file in o da un contenitore che esegue uno dei SQL Server Big Data servizi cluster.

> [!TIP]
> Eseguire i comandi **kubectl** seguenti in un computer client Windows (cmd o PS) o Linux (bash). Richiedono l'autenticazione precedente nel cluster e un contesto del cluster per l'esecuzione. Ad esempio, per un cluster AKS creato in precedenza, è `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` possibile eseguire per scaricare il file di configurazione del cluster Kubernetes e impostare il contesto del cluster.

## <a name="get-status-of-pods"></a>Ottenere lo stato dei Pod

È possibile usare il `kubectl get pods` comando per ottenere lo stato dei Pod nel cluster per tutti gli spazi dei nomi o per lo spazio dei nomi del cluster Big Data. Nelle sezioni seguenti vengono illustrati esempi di entrambi.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostra lo stato di tutti i Pod nel cluster Kubernetes

Eseguire il comando seguente per ottenere tutti i pod e i relativi stati, inclusi i pod che fanno parte dello spazio dei nomi in cui vengono creati SQL Server Big Data Pod del cluster:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostra lo stato di tutti i Pod nel cluster SQL Server Big Data

Usare il `-n` parametro per specificare uno spazio dei nomi specifico. Si noti che SQL Server Big Data i pod del cluster vengono creati in un nuovo spazio dei nomi creato in fase di bootstrap del cluster in base al nome del cluster specificato nel file di configurazione della distribuzione. Il nome predefinito, `mssql-cluster`, viene usato qui.

```bash
kubectl get pods -n mssql-cluster
```

Verrà visualizzato un output simile all'elenco seguente per un cluster Big Data in esecuzione:

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
> Durante la distribuzione, i pod con **lo stato** **ContainerCreating** sono ancora in arrivo. Se la distribuzione è bloccata per qualsiasi motivo, è possibile che si possa fornire un'idea del problema. Osservare anche la colonna **Ready** . Indica il numero di contenitori avviati nel pod. Si noti che le distribuzioni possono richiedere oltre 30 minuti, a seconda della configurazione e della rete. Gran parte di questo tempo è dedicato al download delle immagini del contenitore per diversi componenti.

## <a name="get-pod-details"></a>Ottenere i dettagli del Pod

Eseguire il comando seguente per ottenere una descrizione dettagliata di un pod specifico nell'output in formato JSON. Sono inclusi i dettagli, ad esempio il nodo Kubernetes corrente su cui si trova il Pod, i contenitori in esecuzione all'interno del Pod e l'immagine usata per il bootstrap dei contenitori. Mostra anche altri dettagli, ad esempio etichette, stato e volumi salvati in modo permanente, che sono associati al Pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

Nell'esempio seguente vengono illustrati i dettagli `master-0` per il pod in un cluster `mssql-cluster`Big Data denominato:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Se si verificano errori, è talvolta possibile visualizzare l'errore negli eventi recenti per il pod.

## <a name="get-pod-logs"></a>Ottenere i log Pod

È possibile recuperare i log per i contenitori in esecuzione in un pod. Il comando seguente recupera i log per tutti i contenitori in esecuzione nel pod `master-0` denominato e li restituisce a un nome `master-0-pod-logs.txt`file:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>Ottenere lo stato dei servizi

Eseguire il comando seguente per ottenere i dettagli per i servizi del cluster Big Data. Questi dettagli includono il tipo e gli indirizzi IP associati ai rispettivi servizi e porte. Si noti che SQL Server Big Data servizi cluster vengono creati in un nuovo spazio dei nomi creato in fase di bootstrap del cluster in base al nome del cluster specificato nel file di configurazione della distribuzione.

```bash
kubectl get svc -n <namespace_name>
```

Nell'esempio seguente viene illustrato lo stato dei servizi in un cluster Big Data `mssql-cluster`denominato:

```bash
kubectl get svc -n mssql-cluster
```

I servizi seguenti supportano connessioni esterne al cluster Big Data:

| Service | Descrizione |
|---|---|
| **master-svc-external** | Consente di accedere all'istanza master.<br/>(**External-IP, 31433** e l'utente **sa** ) |
| **controller-svc-external** | Supporta strumenti e client che gestiscono il cluster. |
| **gateway-svc-external** | Consente di accedere al gateway HDFS/Spark.<br/>(**External-IP** e l'utente **root** ) |
| **appproxy-svc-external** | Supportare scenari di distribuzione di applicazioni. |

> [!TIP]
> Questo è un modo per visualizzare i servizi con **kubectl**, ma è anche possibile usare `azdata bdc endpoint list` il comando per visualizzare questi endpoint. Per altre informazioni, vedere [ottenere Big Data endpoint del cluster](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Ottenere i dettagli del servizio

Eseguire questo comando per ottenere una descrizione dettagliata di un servizio in formato JSON output. Includerà dettagli quali etichette, selettore, IP, External-IP (se il servizio è di tipo LoadBalancer), porta e così via.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

Nell'esempio seguente vengono recuperati i dettagli per il servizio **Master-SVC-External** :

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Eseguire comandi in un contenitore

Se gli strumenti esistenti o l'infrastruttura non consentono di eseguire un'attività specifica senza essere effettivamente presenti nel contesto del contenitore, è possibile accedere al contenitore usando `kubectl exec` il comando. Ad esempio, potrebbe essere necessario controllare se esiste un file specifico o potrebbe essere necessario riavviare i servizi nel contenitore. 

Per utilizzare il `kubectl exec` comando, utilizzare la sintassi seguente:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

Le due sezioni seguenti forniscono due esempi di esecuzione di un comando in un contenitore specifico.

### <a id="restartsql"></a>Accedere a un contenitore specifico e riavviare SQL Server processo

Nell'esempio seguente viene illustrato come riavviare il processo di SQL Server nel `mssql-server` contenitore `master-0` nel pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>Accedere a un contenitore specifico e riavviare i servizi in un contenitore
 
Nell'esempio seguente viene illustrato come riavviare tutti i servizi gestiti da supervisore: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>Copia file

Se è necessario copiare i file dal contenitore nel computer locale, usare `kubectl cp` il comando con la sintassi seguente:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Analogamente, è possibile `kubectl cp` usare per copiare i file dal computer locale in un contenitore specifico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>Copia i file da un contenitore

Nell'esempio seguente vengono copiati i file di log SQL Server dal contenitore `~/temp/sqlserverlogs` al percorso nel computer locale (in questo esempio il computer locale è un client Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>Copia i file nel contenitore

Nell'esempio seguente il file **AdventureWorks2016CTP3. bak** viene copiato dal computer locale al contenitore dell'istanza master di SQL Server`mssql-server`() nel `master-0` pod. Il file viene copiato `/tmp` nella directory nel contenitore. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>Forzare l'eliminazione di un pod
 
Non è consigliabile forzare l'eliminazione di un pod. Tuttavia, per verificare la disponibilità, la resilienza o la persistenza dei dati, è possibile eliminare un pod per simulare `kubectl delete pods` un errore di Pod con il comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

Nell'esempio seguente viene eliminato il pod del pool `storage-0-0`di archiviazione:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>Ottieni IP Pod
 
Ai fini della risoluzione dei problemi, potrebbe essere necessario ottenere l'indirizzo IP del nodo su cui è attualmente in esecuzione un pod. Per ottenere l'indirizzo IP, usare il `kubectl get pods` comando con la sintassi seguente:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

L'esempio seguente ottiene l'indirizzo IP del nodo in cui è `master-0` in esecuzione il pod:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Dashboard di Kubernetes

È possibile avviare il dashboard di Kubernetes per altre informazioni sul cluster. Le sezioni seguenti illustrano come avviare il dashboard per Kubernetes in AKS e per Kubernetes bootstrap con kubeadm.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Avviare il dashboard quando il cluster è in esecuzione in AKS

Per avviare l'esecuzione del dashboard Kubernetes:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Se viene ricevuto il seguente errore: *Impossibile restare in ascolto sulla porta 8001: Non è stato possibile creare tutti i listener con i seguenti errori: Non è possibile creare il listener: Errore Listen TCP4 127.0.0.1:8001: > bind: In genere è consentito un solo utilizzo di ogni indirizzo socket (protocollo/indirizzo di rete/porta). Non è possibile creare il listener: Errore di ascolto TcP6: Indirizzo [[:: 1]]: 8001: porta mancante nell'errore di > Indirizzo: Non è possibile restare in attesa su una delle porte richieste: [{8001 9090*}]. Assicurarsi che il dashboard non sia già stato avviato da un'altra finestra.

Quando si avvia il dashboard nel browser, è possibile ricevere avvisi di autorizzazione perché il controllo degli accessi in base al ruolo è abilitato per impostazione predefinita nei cluster AKS e l'account del servizio usato dal dashboard non dispone di autorizzazioni sufficienti per accedere  *a tutte le risorse, ad esempio Pod non consentito: L'utente "System: ServiceAccount: Kube-System: kubernetes-Dashboard" non è in grado di elencare i*Pod nello spazio dei nomi "default"). Eseguire il comando seguente per concedere le autorizzazioni necessarie a `kubernetes-dashboard`e quindi riavviare il Dashboard:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Avviare il dashboard quando il cluster Kubernetes viene avviato con kubeadm

Per istruzioni dettagliate su come distribuire e configurare il dashboard nel cluster Kubernetes, vedere [la documentazione di Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Per avviare il dashboard di Kubernetes, eseguire questo comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa sono i cluster SQL Server Big Data](big-data-cluster-overview.md).
