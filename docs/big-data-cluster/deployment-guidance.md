---
title: Modalità di distribuzione
titleSuffix: SQL Server big data clusters
description: Informazioni su come distribuire i cluster di big data di SQL Server 2019 (anteprima) in Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7a863259a3eb04aef648d98f1d8c4ac22e4a3f38
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582414"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Come distribuire i cluster di big data di SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Cluster di big data di SQL Server possono essere distribuiti come contenitori docker in un cluster Kubernetes. Questa è una panoramica dei passaggi di installazione e configurazione:

- Configurare un cluster Kubernetes in una singola VM, cluster di macchine virtuali o in Azure Kubernetes Service (AKS).
- Installare lo strumento di configurazione cluster **mssqlctl** nel computer client.
- Distribuire cluster di big data di SQL Server in un cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Prerequisiti di cluster Kubernetes

I cluster di big data di SQL Server richiedono almeno la versione Kubernetes di almeno versione 1.10 per server e client (kubectl).

> [!NOTE]
> Si noti che le versioni di Kubernetes client e il server devono essere-1 o + 1 versione secondaria. Per altre informazioni, vedere [Kubernetes supportato rilasci e componente inclinazione](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Configurazione del cluster Kubernetes

Se si dispone già di un cluster Kubernetes che soddisfa di sopra dei prerequisiti, quindi è possibile andare direttamente al [passaggio di distribuzione](#deploy). In questa sezione si presuppone una conoscenza di base dei concetti relativi a Kubernetes.  Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes](https://kubernetes.io/docs/home).

È possibile scegliere di distribuire Kubernetes in uno dei tre modi:

| Distribuzione di Kubernetes in: | Descrizione | Collegamento |
|---|---|---|
| **Minikube** | Un cluster Kubernetes a nodo singolo in una macchina virtuale. | [Istruzioni](deploy-on-minikube.md) |
| **Azure Kubernetes Services (AKS)** | Un servizio di contenitore Kubernetes gestito in Azure. | [Istruzioni](deploy-on-aks.md) |
| **Più computer** | Un cluster Kubernetes distribuito nei computer fisici o macchine virtuali usando **kubeadm** | [Istruzioni](deploy-with-kubeadm.md) |
  
> [!TIP]
> Per un esempio di script python che consente di distribuire cluster di big data sia servizio contenitore di AZURE e SQL Server, vedere [distribuire un cluster di big data in Azure Kubernetes Service (AKS) di SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="deploy-sql-server-2019-big-data-tools"></a>Distribuire strumenti di SQL Server 2019 big data

Prima di distribuire il cluster di big data di SQL Server 2019, innanzitutto [installare gli strumenti dei big data](deploy-big-data-tools.md):
- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Estensione di SQL Server 2019**

## <a id="deploy"></a> Distribuire il cluster di big data di SQL Server

Dopo aver configurato il cluster Kubernetes, è possibile procedere con la distribuzione per il cluster di big data di SQL Server. 

> [!NOTE]
> Se esegue l'aggiornamento da una versione precedente, vedere la [esegue l'aggiornamento di questo articolo](#upgrade).

Per distribuire un cluster di big data in Azure con tutte le configurazioni predefinite per un ambiente di sviluppo/test, seguire le istruzioni riportate in questo articolo:

[Guida introduttiva: Distribuire cluster di big data di SQL Server in Kubernetes](quickstart-big-data-cluster-deploy.md)

Se si desidera personalizzare la distribuzione del cluster di big data in base al carico di lavoro deve, seguire le istruzioni nella parte restante di questo articolo.

## <a name="verify-kubernetes-configuration"></a>Verificare la configurazione di kubernetes

Eseguire la **kubectl** comando per visualizzare la configurazione del cluster. Verificare che tale kubectl fa riferimento il contesto del cluster corretto.

```bash
kubectl config view
```

## <a id="env"></a> Definire le variabili di ambiente

La configurazione del cluster può essere personalizzata usando un set di variabili di ambiente che vengono passati al `mssqlctl create cluster` comando. La maggior parte delle variabili di ambiente sono facoltativa con i valori predefiniti come indicato di seguito. Si noti che le variabili di ambiente, ad esempio le credenziali che richiedono l'input dell'utente.

| Variabile di ambiente | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|
| **ACCEPT_EULA** | Yes | N/D | Accettare il contratto di licenza di SQL Server (ad esempio, 'Yes').  |
| **CLUSTER_NAME** | Yes | N/D | Il nome dello spazio dei nomi Kubernetes per distribuire cluster di big data in SQL Server. |
| **CLUSTER_PLATFORM** | Yes | N/D | La piattaforma che è distribuito il cluster Kubernetes. Può essere `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | No | 1 | Il numero di repliche di pool di calcolo da compilare. Nella versione CTP 2.4 solo con valori consentito è 1. |
| **CLUSTER_DATA_POOL_REPLICAS** | no | 2 | Il numero di dati del pool di repliche da compilare. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | No | 2 | Il numero di repliche di pool di archiviazione da compilare. |
| **DOCKER_REGISTRY** | Yes | TBD | Il Registro di sistema privato in cui sono archiviate le immagini usate per distribuire il cluster. |
| **DOCKER_REPOSITORY** | Yes | TBD | Il repository privato all'interno del Registro di sistema precedente in cui sono archiviate le immagini.  È necessario per la durata dell'anteprima pubblica gestita. |
| **DOCKER_USERNAME** | Yes | N/D | Il nome utente per accedere alle immagini di contenitore nel caso in cui sono archiviati in un repository privato. È necessario per la durata dell'anteprima pubblica gestita. |
| **DOCKER_PASSWORD** | Yes | N/D | La password per accedere al repository privato precedente. È necessario per la durata dell'anteprima pubblica gestita.|
| **DOCKER_EMAIL** | Yes | N/D | L'indirizzo di posta elettronica. |
| **DOCKER_IMAGE_TAG** | No | più recente | L'etichetta utilizzata per contrassegnare le immagini. |
| **DOCKER_IMAGE_POLICY** | No | Always | Imporre sempre un'operazione pull delle immagini.  |
| **DOCKER_PRIVATE_REGISTRY** | Yes | N/D | Per l'intervallo di tempo dell'anteprima pubblica gestita, è necessario impostare questo valore su "1". |
| **CONTROLLER_USERNAME** | Yes | N/D | Il nome utente dell'amministratore cluster. |
| **CONTROLLER_PASSWORD** | Yes | N/D | La password dell'amministratore cluster. |
| **KNOX_PASSWORD** | Yes | N/D | La password per utente Knox. |
| **MSSQL_SA_PASSWORD** | Yes | N/D | La password dell'utente dell'amministratore di sistema per l'istanza master di SQL. |
| **USE_PERSISTENT_VOLUME** | No | true | `true` Per utilizzare attestazioni Volume permanente Kubernetes per l'archiviazione di pod.  `false` usare l'archiviazione temporanea host per l'archiviazione di pod. Vedere le [persistenza dei dati](concept-data-persistence.md) per altri dettagli vedere l'articolo. Se si distribuisce SQL Server del cluster di big data in minikube e USE_PERSISTENT_VOLUME = true, è necessario impostare il valore per `STORAGE_CLASS_NAME=standard`. |
| **STORAGE_CLASS_NAME** | No | predefiniti | Se `USE_PERSISTENT_VOLUME` è `true` viene indicato il nome della classe di archiviazione Kubernetes da usare. Vedere le [persistenza dei dati](concept-data-persistence.md) per altri dettagli vedere l'articolo. Se si distribuisce SQL Server del cluster di big data in minikube, il nome predefinito della classe di archiviazione è diverso ed è necessario eseguirne l'override impostando `STORAGE_CLASS_NAME=standard`. |
| **CONTROLLER_PORT** | No | 30080 | La porta TCP/IP che il servizio controller è in ascolto sulla rete pubblica. |
| **MASTER_SQL_PORT** | No | 31433 | La porta TCP/IP che è in ascolto l'istanza SQL master nella rete pubblica. |
| **KNOX_PORT** | No | 30443 | Porta TCP/IP Knox Apache è in ascolto sulla rete pubblica. |
| **PROXY_PORT** | No | 30777 | Porta TCP/IP del servizio proxy è in ascolto sulla rete pubblica. Questa è la porta usata per il calcolo del portale URL. |
| **GRAFANA_PORT** | No | 30888 | Porta TCP/IP di Grafana con monitoraggio dell'applicazione è in ascolto sulla rete pubblica. |
| **KIBANA_PORT** | No | 30999 | La porta TCP/IP che è in ascolto l'applicazione di ricerca log di Kibana nella rete pubblica. |


> [!IMPORTANT]
>1. Per la durata della fase di anteprima privata limitata, le credenziali del registro Docker privato verranno fornite all'utente durante la valutazione di [registrazione EAP](https://aka.ms/eapsignup).
>1. Per un cluster locale compilati con **kubeadm**, il valore per la variabile di ambiente `CLUSTER_PLATFORM` è `kubernetes`. Inoltre, quando `USE_PERSISTENT_VOLUME=true`, è necessario pre-provisioning di una classe di archiviazione Kubernetes e passarlo tramite il `STORAGE_CLASS_NAME`.
>1. Verificare che a capo le password tra virgolette quando contiene caratteri speciali. È possibile impostare il MSSQL_SA_PASSWORD con qualsiasi nome desiderato, ma assicurarsi che questi sono sufficientemente complessi e non usare la `!`, `&` o `'` caratteri. Si noti che i delimitatori tra virgolette doppie funzionano solo in comandi bash.
>1. Il nome del cluster deve essere solo alfanumerici caratteri minuscoli, senza spazi. Tutti Kubernetes gli elementi (contenitori, i POD, set prive di stato e servizi) per il cluster verranno creati in uno spazio dei nomi con lo stesso nome del cluster il nome specificato.
>1. Il **SA** account sia un amministratore di sistema nell'istanza Master di SQL Server che viene creato durante l'installazione. Dopo la creazione il contenitore di SQL Server, la variabile di ambiente MSSQL_SA_PASSWORD specificata diventa individuabile eseguendo echo MSSQL_SA_PASSWORD $ nel contenitore. Per motivi di sicurezza, modificare la password dell'amministratore di sistema in base alle procedure consigliate documentate [qui](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Impostare le variabili di ambiente necessarie per la distribuzione di un cluster di big data è diverso a seconda se si usano client Windows o Linux.  Scegliere i passaggi seguenti a seconda del sistema operativo in uso.

Inizializzare le variabili di ambiente seguente, sono necessari per distribuire il cluster:

### <a name="windows"></a>Windows

Usa una finestra CMD (non PowerShell), configurare le seguenti variabili di ambiente. Non utilizzare le virgolette per racchiudere i valori.

```cmd
SET ACCEPT_EULA=yes
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your email address>
SET DOCKER_PRIVATE_REGISTRY=1
```

### <a name="linux"></a>Linux

Inizializzare le variabili di ambiente seguenti. In bash, è possibile usare le virgolette per racchiudere ogni valore.

```bash
export ACCEPT_EULA="yes"
export CLUSTER_PLATFORM="<minikube or aks or kubernetes>"

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your email address>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Impostazioni di Minikube

Se si distribuisce in minikube e `USE_PERSISTENT_VOLUME=true` (impostazione predefinita), è inoltre necessario sostituire il valore predefinito per `STORAGE_CLASS_NAME` variabile di ambiente.

Usare il comando seguente in Windows per le distribuzioni di minikube:

```cmd
SET STORAGE_CLASS_NAME=standard
```

Usare il comando seguente in Linux per le distribuzioni di minikube:

```bash
export STORAGE_CLASS_NAME=standard
```

In alternativa, è possibile eliminare con volumi permanenti in minikube impostando `USE_PERSISTENT_VOLUME=false`.

### <a name="kubadm-settings"></a>Impostazioni Kubadm

Se si distribuisce con kubeadm sul proprio computer fisici o macchine virtuali, è necessario pre-provisioning di una classe di archiviazione Kubernetes e passarlo tramite il `STORAGE_CLASS_NAME`. In alternativa, è possibile eliminare con volumi permanenti impostando `USE_PERSISTENT_VOLUME=false`. Per altre informazioni sull'archiviazione permanente, vedere [persistenza dei dati con SQL Server del cluster di big data in Kubernetes](concept-data-persistence.md).

## <a name="deploy-sql-server-big-data-cluster"></a>Distribuire il cluster Big Data di SQL Server

L'API di creazione del cluster viene usato per inizializzare lo spazio dei nomi Kubernetes e distribuire tutti i POD delle applicazioni nello spazio dei nomi. Per distribuire cluster di big data di SQL Server nel cluster Kubernetes, eseguire il comando seguente:

```bash
mssqlctl cluster create --name <your-cluster-name>
```

Durante il bootstrap del cluster, la finestra di comando client restituirà lo stato della distribuzione. Durante il processo di distribuzione, verrà visualizzato una serie di messaggi in cui è in attesa il pod controller:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Dopo 10 a 20 minuti, si dovrebbe ricevere una notifica che il pod controller sia in esecuzione:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo a causa del tempo necessario per scaricare le immagini del contenitore per i componenti del cluster di big data. Tuttavia, non richiederà alcune ore. Se si verificano problemi con la distribuzione, vedere la [risoluzione dei problemi](#troubleshoot) sezione di questo articolo per imparare a monitorare e controllare la distribuzione.

Al termine della distribuzione, l'output invia una notifica di esito positivo:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> Ottenere gli endpoint del cluster di big data

Una volta completato lo script di distribuzione, è possibile ottenere l'indirizzo IP dell'istanza master di SQL Server mediante i passaggi descritti di seguito. Si userà questo indirizzo IP e porta numero 31433 per connettersi all'istanza master di SQL Server (ad esempio:  **\<ip-address-of-endpoint-master-pool\>, 31433**). Allo stesso modo, è possibile connettersi a SQL Server associati IP del cluster (Gateway HDFS/Spark) dei big data con il **protezione di endpoint** servizio.

I seguenti comandi di kubectl recuperano gli endpoint comuni per il cluster di big data:

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc endpoint-security -n <your-cluster-name>
kubectl get svc endpoint-service-proxy -n <your-cluster-name>
```

Cercare il **External-IP** valore assegnato a ogni servizio.

Tutti gli endpoint del cluster vengono illustrati anche nella **gli endpoint di servizio** scheda nel portale di amministrazione Cluster. È possibile accedere al portale con l'esterno indirizzo IP e porta numero per il `endpoint-service-proxy` (ad esempio: **https://\<ip-address-of-endpoint-service-proxy\>: 30777/portale**). Le credenziali per accedere al portale di amministrazione sono i valori delle `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variabili di ambiente fornite sopra. È possibile utilizzare il portale di amministrazione Cluster anche per monitorare la distribuzione.

Per altre informazioni sulla connessione, vedere [Connetti a SQL Server del cluster di big data con Azure Data Studio](connect-to-big-data-cluster.md).

### <a name="minikube"></a>Minikube

Se si usa Minikube, è necessario eseguire il comando seguente per ottenere l'indirizzo IP che è necessario connettersi a. Oltre all'indirizzo IP, specificare la porta per l'endpoint a che è necessario connettersi. Per ottenere tutti gli endpoint di servizio per 

```bash
minikube ip
```

Indipendentemente dalla piattaforma si sta usando il cluster Kubernetes, per ottenere tutti gli endpoint del servizio distribuiti per il cluster, eseguire il comando seguente:
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> Eseguire l'aggiornamento a una nuova versione

Attualmente, l'unico modo per aggiornare un cluster di big data a una nuova versione è manualmente, rimuovere e ricreare il cluster. Ogni versione ha una versione univoca del **mssqlctl** che non è compatibile con la versione precedente. Inoltre, se un cluster precedente è stato necessario scaricare un'immagine in un nuovo nodo, l'immagine più recente potrebbe non essere compatibile con le immagini precedenti nel cluster. Per eseguire l'aggiornamento alla versione più recente, procedere come segue:

1. Prima di eliminare il vecchio cluster, eseguire il backup dei dati nell'istanza di master di SQL Server e in HDFS. Per l'istanza master di SQL Server, è possibile usare [SQL Server backup e ripristino](data-ingestion-restore-database.md). Per un HDFS, si [possibile copiare i dati con **curl**](data-ingestion-curl.md).

1. Eliminare il vecchio cluster con il `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di **mssqlctl** che corrisponde al cluster. Non eliminare un cluster con la versione più recente di meno recente **mssqlctl**.

1. Disinstallare eventuali versioni precedenti del **mssqlctl**.

   ```bash
   pip3 uninstall mssqlctl
   ```

   > [!IMPORTANT]
   > Non è necessario installare la nuova versione del **mssqlctl** senza disinstallare innanzitutto tutte le versioni precedenti.

1. Installare la versione più recente di **mssqlctl**. 

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > Per ogni versione e il percorso **mssqlctl** le modifiche. Anche se è installato in precedenza **mssqlctl**, è necessario reinstallare dal percorso più recente prima di creare il nuovo cluster.

1. Installare la versione più recente seguendo le istruzioni riportate nel [distribuire sezione](#deploy) di questo articolo. 

## <a id="troubleshoot"></a> Monitoraggio e risoluzione dei problemi

Per monitorare o risolvere i problemi di una distribuzione, usare **kubectl** per verificare lo stato del cluster e di rilevare potenziali problemi. In qualsiasi momento durante una distribuzione, è possibile aprire una finestra di comando diverso per eseguire i test seguenti.

1. Controllare lo stato dei POD nel cluster.

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   Durante la distribuzione di POD con un **lo stato** dei **ContainerCreating** ancora riaperto. Se la distribuzione si blocca per qualche motivo, questo può avere un'idea in cui il problema potrebbe essere. Si analizzino i **pronti** colonna. Queste informazioni indicano quanti contenitori è sono avviata nel pod. Si noti che le distribuzioni possono richiedere più di trenta minuti a seconda della configurazione e la rete. Gran parte di questo tempo viene impiegata per scaricare le immagini del contenitore per i diversi componenti. La tabella seguente illustra l'output di esempio modificato dei due contenitori durante una distribuzione:

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. Viene descritto un singolo pod per altri dettagli. Controlla se il comando seguente di `mssql-storage-pool-default-0` pod.

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   Ciò restituisce informazioni dettagliate sui pod, inclusi gli eventi recenti. Se si è verificato un errore, è possibile trovare alcuni casi il messaggio di errore.

1. Recuperare i registri per contenitori in esecuzione in un pod. Il comando seguente recupera i log per tutti i contenitori in esecuzione nel pod denominato `mssql-storage-pool-default-0` vengono inseriti in un file denominato `pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. Esaminare i servizi del cluster durante e dopo una distribuzione con il comando seguente:

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   Questi servizi supportano le connessioni interne ed esterne per i cluster di big data. Per le connessioni esterne, vengono usati i servizi seguenti:

   | Servizio | Descrizione |
   |---|---|
   | **endpoint-master-pool** | Fornisce l'accesso all'istanza master.<br/>(**EXTERNAL-IP, 31433** e il **SA** utente) |
   | **endpoint-controller** | Supporta gli strumenti e i client che gestiscono il cluster. |
   | **endpoint-service-proxy** | Fornisce l'accesso per il [portale di amministrazione Cluster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**:30777/portal)|
   | **endpoint-security** | Fornisce l'accesso al gateway HDFS/Spark.<br/>(**EXTERNAL-IP** e il **radice** utente) |

1. Usare la [portale di amministrazione del Cluster](cluster-admin-portal.md) per monitorare la distribuzione nel **distribuzione** scheda. È necessario attendere per il **endpoint-servizio-proxy** avvio prima di accedere a questo portale, pertanto non sarà disponibile all'inizio di una distribuzione del servizio.

> [!TIP]
> Per altre informazioni sulla risoluzione dei problemi del cluster, vedere [comandi Kubectl per il monitoraggio e risoluzione dei problemi dei cluster di SQL Server i big data](cluster-troubleshooting-commands.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere le risorse seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)