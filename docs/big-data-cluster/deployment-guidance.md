---
title: Linee guida per la distribuzione
titleSuffix: SQL Server big data clusters
description: Informazioni su come distribuire i cluster di big data di SQL Server 2019 (anteprima) in Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a2ace569180006f54461631848ecbf5342b2c1e3
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472038"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Come distribuire i cluster di big data di SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Cluster di big data di SQL Server viene distribuita come contenitori docker in un cluster Kubernetes. Questa è una panoramica dei passaggi di installazione e configurazione:

- Configurare un cluster Kubernetes in una singola VM, cluster di macchine virtuali o in Azure Kubernetes Service (AKS).
- Installare lo strumento di configurazione cluster **mssqlctl** nel computer client.
- Distribuire un cluster di big data di SQL Server in un cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Installare strumenti di SQL Server 2019 big data

Prima di distribuire un cluster di big data, SQL Server 2019 innanzitutto [installare gli strumenti dei big data](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Estensione di SQL Server 2019**

## <a id="prereqs"></a> Prerequisiti di Kubernetes

I cluster di big data di SQL Server richiedono almeno la versione Kubernetes di almeno versione 1.10 per server e client (kubectl).

> [!NOTE]
> Si noti che le versioni di Kubernetes client e server devono essere all'interno di versione secondaria + 1 o -1. Per altre informazioni, vedere [Kubernetes supportato rilasci e componente inclinazione](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Configurazione del cluster Kubernetes

Se si dispone già di un cluster Kubernetes che soddisfi i prerequisiti precedenti, quindi è possibile andare direttamente al [passaggio di distribuzione](#deploy). In questa sezione si presuppone una conoscenza di base dei concetti relativi a Kubernetes.  Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes](https://kubernetes.io/docs/home).

È possibile scegliere di distribuire Kubernetes in uno dei tre modi:

| Distribuzione di Kubernetes in: | Descrizione | Collegamento |
|---|---|---|
| **Azure Kubernetes Services (AKS)** | Un servizio di contenitore Kubernetes gestito in Azure. | [Istruzioni](deploy-on-aks.md) |
| **Più computer (kubeadm)** | Un cluster Kubernetes distribuito nei computer fisici o macchine virtuali usando **kubeadm** | [Istruzioni](deploy-with-kubeadm.md) |
| **Minikube** | Un cluster Kubernetes a nodo singolo in una macchina virtuale. | [Istruzioni](deploy-on-minikube.md) |

> [!TIP]
> Per un esempio di script python che consente di distribuire AKS sia un Server SQL cluster di big data in un unico passaggio, vedere [Guida introduttiva: Distribuire SQL Server in Azure Kubernetes Service (AKS) del cluster dei big data](quickstart-big-data-cluster-deploy.md).

### <a name="verify-kubernetes-configuration"></a>Verificare la configurazione di Kubernetes

Eseguire la **kubectl** comando per visualizzare la configurazione del cluster. Verificare che tale kubectl fa riferimento il contesto del cluster corretto.

```bash
kubectl config view
```

Dopo aver configurato il cluster Kubernetes, è possibile procedere con la distribuzione di un nuovo cluster di big data di SQL Server. Se esegue l'aggiornamento da una versione precedente, vedi [come aggiornare i cluster di SQL Server i big data](deployment-upgrade.md).

## <a id="deploy"></a> Panoramica della distribuzione

A partire da CTP 2.5, la maggior parte delle impostazioni di cluster di big data sono definite in un file di configurazione di distribuzione JSON. È possibile usare un profilo di distribuzione predefinito per AKS, kubeadm, oppure minikube oppure è possibile personalizzare il proprio file di configurazione di distribuzione da usare durante l'installazione. Per motivi di sicurezza, le impostazioni di autenticazione vengono passate tramite le variabili di ambiente.

Le sezioni seguenti forniscono altri dettagli su come configurare i big data cluster le distribuzioni, nonché esempi di personalizzazione comuni. Inoltre, è sempre possibile modificare il file di configurazione di distribuzione personalizzato usando un editor, ad esempio Visual Studio code, ad esempio.

## <a id="configfile"></a> Configurazioni predefinite

I big data opzioni sono definite nei file di configurazione JSON di distribuzione del cluster. Esistono tre profili di distribuzione standard con le impostazioni predefinite per gli ambienti di sviluppo/test:

| Profilo di distribuzione | Ambiente di Kubernetes |
|---|---|
| **aks-dev-test.json** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test.json** | Più computer (kubeadm) |
| **minikube-dev-test.json** | minikube |

È possibile distribuire un cluster di big data eseguendo **di creazione del cluster mssqlctl**. Questo verrà richiesto di scegliere una delle configurazioni predefinite e quindi in modo semplificato la distribuzione.

```bash
mssqlctl cluster create
```

> [!TIP]
> In questo esempio, richiesto per tutte le impostazioni che non fanno parte della configurazione predefinita, ad esempio le password. Si noti che le informazioni di Docker viene fornite all'utente da Microsoft come parte del 2019 Server SQL [programma Early Adoption](https://aka.ms/eapsignup).

## <a id="customconfig"></a> Configurazioni personalizzate

È anche possibile personalizzare il proprio file di configurazione di distribuzione. È possibile farlo con i passaggi seguenti:

1. Iniziare con uno dei profili di distribuzione standard che corrispondono all'ambiente di Kubernetes. È possibile usare la **elenco di configurazione di cluster mssqlctl** comando per elencare li:

   ```bash
   mssqlctl cluster config list
   ```

1. Per personalizzare la distribuzione, creare una copia del profilo di distribuzione con il **mssqlctl cluster config init** comando. Ad esempio, il comando seguente crea una copia del **aks-dev-test.json** file di configurazione di distribuzione nella directory corrente:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. Per personalizzare le impostazioni nel file di configurazione di distribuzione, è possibile modificarlo in uno strumento valido per la modifica di documenti json, ad esempio Visual Studio Code. Per l'automazione con script, è possibile modificare il file di configurazione personalizzata mediante **gruppo di sezione di configurazione di cluster mssqlctl** comando. Ad esempio, il comando seguente modifica un file di configurazione personalizzato per modificare il nome del cluster distribuito da quello predefinito (**mssql-cluster**) per **test-cluster**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > Uno strumento utile per trovare i percorsi JSON è il [analizzatore Online JSONPath](https://jsonpath.com/).

   Oltre a passare coppie chiave-valore, è anche possibile fornire i valori JSON inline o passare i file di patch JSON. Per altre informazioni, vedere [configurare le impostazioni di distribuzione per i cluster di big data](deployment-custom-configuration.md).

1. Quindi passare il file di configurazione personalizzati **di creazione del cluster mssqlctl**. Si noti che è necessario impostare la necessaria [variabili di ambiente](#env), in caso contrario, verrà richiesto per i valori:

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> Per altre informazioni sulla struttura di un file di configurazione di distribuzione, vedere la [riferimento a file di configurazione di distribuzione](reference-deployment-config.md). Per altri esempi di configurazione, vedere [configurare le impostazioni di distribuzione per i cluster di big data](deployment-custom-configuration.md).

## <a id="env"></a> Variabili di ambiente

Le variabili di ambiente seguenti vengono usate per le impostazioni di sicurezza che non sono archiviate in un file di configurazione di distribuzione.

| Variabile di ambiente | Descrizione |
|---|---|---|---|
| **DOCKER_REGISTRY** | Il Registro di sistema privato in cui sono archiviate le immagini usate per distribuire il cluster. |
| **DOCKER_REPOSITORY** | Il repository privato all'interno del Registro di sistema precedente in cui sono archiviate le immagini. |
| **DOCKER_USERNAME** | Il nome utente per accedere alle immagini di contenitore nel caso in cui sono archiviati in un repository privato. |
| **DOCKER_PASSWORD** | La password per accedere al repository privato precedente. |
| **DOCKER_IMAGE_TAG** | L'etichetta utilizzata per contrassegnare le immagini. Per impostazione predefinita **più recente**, ma è consigliabile usare il tag che corrisponde alla versione per evitare problemi di incompatibilità di versione. |
| **CONTROLLER_USERNAME** | Il nome utente dell'amministratore cluster. |
| **CONTROLLER_PASSWORD** | La password dell'amministratore cluster. |
| **KNOX_PASSWORD** | La password per utente Knox. |
| **MSSQL_SA_PASSWORD** | La password dell'utente dell'amministratore di sistema per l'istanza master di SQL. |

Queste variabili di ambiente devono essere impostate prima di chiamare **di creazione del cluster mssqlctl**. Se tutte le variabili non sono impostata, richiesto.

Nell'esempio seguente viene illustrato come impostare le variabili di ambiente per Linux (bash) e Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=<controller_user>
export CONTROLLER_PASSWORD=<password>
export DOCKER_REGISTRY=<docker-registry>
export DOCKER_REPOSITORY=<docker-repository>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
export DOCKER_IMAGE_TAG=ctp2.5
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET DOCKER_REGISTRY=<docker-registry>
SET DOCKER_REPOSITORY=<docker-repository>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
SET DOCKER_IMAGE_TAG=ctp2.5
```

Durante la configurazione variabili di ambiente, è necessario eseguire `mssqlctl cluster create` per attivare la distribuzione. Questo esempio Usa il file di configurazione del cluster creato in precedenza:

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

Tenere presente le linee guida seguenti:

- A questo punto, verranno fornite le credenziali del registro Docker privato per l'utente al momento di valutazione di [registrazione programma Early Adoption](https://aka.ms/eapsignup). Registrazione di adozione programma anticipata è necessaria per testare i cluster di big data di SQL Server.
- Verificare che a capo le password tra virgolette quando contiene caratteri speciali. È possibile impostare il **MSSQL_SA_PASSWORD** qualsiasi elemento, ad esempio, ma assicurarsi che la password è sufficientemente complessa che non usano il `!`, `&` o `'` caratteri. Si noti che i delimitatori tra virgolette doppie funzionano solo in comandi bash.
- Il **SA** account di accesso è un amministratore di sistema nell'istanza master di SQL Server che viene creato durante l'installazione. Dopo aver creato il contenitore di SQL Server, il **MSSQL_SA_PASSWORD** variabile di ambiente specificata diventa individuabile eseguendo echo MSSQL_SA_PASSWORD $ nel contenitore. Per motivi di sicurezza, modificare la password dell'amministratore di sistema in base alle procedure consigliate documentate [qui](../linux/quickstart-install-connect-docker.md#sapassword).
- Il **DOCKER_IMAGE_TAG** in questo esempio i controlli quale versione si siano installando. In questo esempio è la versione CTP 2.5.

## <a id="unattended"></a> Installazione automatica

Per una distribuzione automatica, è necessario impostare tutte le variabili di ambiente necessarie, usare un file di configurazione e chiamare `mssqlctl cluster create` comando con il `--accept-eula yes` parametro. Gli esempi nella sezione precedente illustrano la sintassi per l'installazione automatica.

## <a id="monitor"></a> Monitorare la distribuzione

Durante il bootstrap del cluster, la finestra di comando client restituirà lo stato della distribuzione. Durante il processo di distribuzione, verrà visualizzato una serie di messaggi in cui è in attesa il pod controller:

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

In meno di 15 a 30 minuti, si dovrebbe ricevere una notifica che il pod controller sia in esecuzione:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo a causa del tempo necessario per scaricare le immagini del contenitore per i componenti del cluster di big data. Tuttavia, non richiederà alcune ore. Se si verificano problemi con la distribuzione, vedere [monitoraggio e risoluzione dei problemi dei cluster di SQL Server i big data](cluster-troubleshooting-commands.md).

Al termine della distribuzione, l'output invia una notifica di esito positivo:

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

Prendere nota dell'URL del **Endpoint portale** nell'output precedente per l'uso nella sezione successiva.

> [!TIP]
> È il nome predefinito per il cluster di big data distribuita `mssql-cluster` a meno che non modificato da una configurazione personalizzata.

## <a id="endpoints"></a> Recuperare gli endpoint

Una volta completato lo script di distribuzione, è possibile ottenere gli indirizzi IP degli endpoint esterni per il cluster di big data usando la procedura seguente.

1. Copiare l'output della distribuzione, il **Endpoint portale** e rimuovere il `/portal/` alla fine. Si tratta dell'URL del Proxy di gestione (ad esempio, `https://<ip-address>:30777`).

   > [!TIP]
   > Se non è l'output della distribuzione, è possibile ottenere l'indirizzo IP per il Proxy di gestione, esaminando l'output di EXTERNAL-IP di quanto segue **kubectl** comando:
   >
   > ```bash
   > kubectl get svc mgmtproxy-svc-external -n <your-cluster-name>
   > ```

1. Accedere al cluster di big data con **mssqlctl login**. Impostare il **-endpoint** parametro per il Proxy di gestione.

   ```bash
   mssqlctl login --endpoint https://<ip-address>:30777
   ```

   Specificare il nome utente e la password configurata per il controller (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante la distribuzione.

1. Eseguire **elenco di endpoint cluster mssqlctl** per ottenere un elenco con una descrizione di ogni endpoint e i relativi valori di porta e indirizzo IP. Ad esempio, l'esempio seguente visualizza l'output per l'endpoint del portale di gestione:

   ```output
   {
     "description": "Management Portal",
     "endpoint": "https://<ip-address>:30777/portal",
     "ip": "<ip-address>",
     "name": "portal",
     "port": 30777,
     "protocol": "https"
   },
   ```

1. Tutti gli endpoint del cluster vengono illustrati anche nella **gli endpoint di servizio** scheda nel portale di amministrazione Cluster. È possibile accedere al portale tramite l'endpoint del portale di gestione nel passaggio precedente (ad esempio, `https://<ip-address>:30777/portal`). Le credenziali per accedere al portale di amministrazione sono i valori per il controller il nome utente e la password specificata durante la distribuzione. È possibile utilizzare il portale di amministrazione Cluster anche per monitorare la distribuzione.

### <a name="minikube"></a>Minikube

Se si usa minikube, è necessario eseguire il comando seguente per ottenere l'indirizzo IP che è necessario connettersi a. Oltre all'indirizzo IP, specificare la porta per l'endpoint a che è necessario connettersi.

```bash
minikube ip
```

Indipendentemente dalla piattaforma si sta usando il cluster Kubernetes, per ottenere tutti gli endpoint del servizio distribuiti per il cluster, eseguire il comando seguente:

```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="connect"></a> Connettersi al cluster

Per altre informazioni su come connettersi al cluster di big data, vedere [Connetti a SQL Server del cluster di big data con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla distribuzione di cluster di big data, vedere le risorse seguenti:

- [Configurare le impostazioni di distribuzione per i cluster di big data](deployment-custom-configuration.md)
- [Eseguire una distribuzione non in linea di un cluster di big data di SQL Server](deploy-offline.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
