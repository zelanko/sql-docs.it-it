---
title: Linee guida per la distribuzione
titleSuffix: SQL Server big data clusters
description: Informazioni su come distribuire SQL Server cluster 2019 Big Data (anteprima) in Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419416"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Come distribuire cluster di Big Data SQL Server in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server cluster Big Data viene distribuito come contenitore Docker in un cluster Kubernetes. Si tratta di una panoramica dei passaggi di installazione e configurazione:

- Configurare un cluster Kubernetes in una singola macchina virtuale, in un cluster di macchine virtuali o in Azure Kubernetes Service (AKS).
- Installare lo strumento di configurazione del cluster **azdata** nel computer client.
- Distribuire un cluster SQL Server Big Data in un cluster Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Installare SQL Server 2019 Big Data Tools

Prima di distribuire un cluster SQL Server 2019 Big Data, [installare innanzitutto gli strumenti di Big Data](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Estensione SQL Server 2019**

## <a id="prereqs"></a>Prerequisiti di Kubernetes

SQL Server cluster di Big Data richiedono una versione minima di Kubernetes di almeno v 1.10 per server e client (kubectl).

> [!NOTE]
> Si noti che le versioni client e server Kubernetes devono essere comprese tra + 1 o-1 versione secondaria. Per altre informazioni, vedere le [Note sulla versione di Kubernetes e il criterio SKU di sfasamento della versione)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a>Installazione del cluster Kubernetes

Se è già presente un cluster Kubernetes che soddisfa i prerequisiti indicati in precedenza, è possibile passare direttamente alla fase di [distribuzione](#deploy). Questa sezione presuppone una conoscenza di base dei concetti relativi a Kubernetes.  Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes](https://kubernetes.io/docs/home).

È possibile scegliere di distribuire Kubernetes in uno dei tre modi seguenti:

| Distribuisci Kubernetes in: | Descrizione | Collegamento |
|---|---|---|
| **Servizi Kubernetes di Azure (AKS)** | Un servizio contenitore Kubernetes gestito in Azure. | [Istruzioni](deploy-on-aks.md) |
| **Più computer (kubeadm)** | Un cluster Kubernetes distribuito in macchine fisiche o virtuali mediante **kubeadm** | [Istruzioni](deploy-with-kubeadm.md) |
| **Minikube** | Un cluster Kubernetes a nodo singolo in una macchina virtuale. | [Istruzioni](deploy-on-minikube.md) |

> [!TIP]
> Per uno script Python di esempio che distribuisce sia AKS sia un SQL Server Big Data cluster in un unico passaggio [, vedere Guida introduttiva: Distribuire SQL Server cluster Big Data in Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md).

### <a name="verify-kubernetes-configuration"></a>Verificare la configurazione di Kubernetes

Eseguire il comando **kubectl** per visualizzare la configurazione del cluster. Verificare che kubectl sia puntato al contesto del cluster corretto.

```bash
kubectl config view
```

Dopo aver configurato il cluster Kubernetes, è possibile procedere con la distribuzione di un nuovo cluster SQL Server Big Data. Se si esegue l'aggiornamento da una versione precedente, vedere [How to upgrade SQL Server Big Data Clusters](deployment-upgrade.md).

## <a id="deploy"></a>Panoramica della distribuzione

La maggior parte delle impostazioni del cluster Big Data è definita in un file di configurazione della distribuzione JSON. È possibile usare un profilo di distribuzione predefinito per AKS `kubeadm`, `minikube` o oppure è possibile personalizzare il file di configurazione della distribuzione da usare durante l'installazione. Per motivi di sicurezza, le impostazioni di autenticazione vengono passate tramite le variabili di ambiente.

Le sezioni seguenti forniscono altri dettagli su come configurare le distribuzioni di Big Data cluster, nonché esempi di personalizzazioni comuni. Inoltre, è sempre possibile modificare il file di configurazione della distribuzione personalizzata usando un editor come VS Code ad esempio.

## <a id="configfile"></a>Configurazioni predefinite

Le opzioni di distribuzione del cluster di Big data sono definite nei file di configurazione JSON. Sono disponibili tre profili di distribuzione standard con le impostazioni predefinite per gli ambienti di sviluppo/test:

| Profilo di distribuzione | Ambiente Kubernetes |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | Più computer (kubeadm) |
| **minikube-dev-test** | Minikube |

È possibile distribuire un cluster di Big Data eseguendo **azdata BDC create**. In questo modo verrà richiesto di scegliere una delle configurazioni predefinite e verrà illustrata la distribuzione.

La prima volta che si `azdata` esegue è necessario `--accept-eula` includere per accettare il contratto di licenza con l'utente finale (EULA).

```bash
azdata bdc create --accept-eula
```

In questo scenario vengono richieste le impostazioni che non fanno parte della configurazione predefinita, ad esempio le password. 

> [!NOTE]
> A partire da SQL Server 2019 CTP 3,2, non si è più membri di con il programma di adozione SQL Server 2019 [Early](https://aka.ms/eapsignup) per sperimentare le versioni di anteprima di Big Data cluster.

> [!IMPORTANT]
> Il nome predefinito del cluster Big Data è **MSSQL-cluster**. È importante saperlo per eseguire uno dei comandi **kubectl** che specificano lo spazio dei nomi Kubernetes con il `-n` parametro.

## <a id="customconfig"></a>Configurazioni personalizzate

È anche possibile personalizzare il proprio profilo di configurazione della distribuzione. Questa operazione può essere eseguita con i passaggi seguenti:

1. Iniziare con uno dei profili di distribuzione standard che corrispondono all'ambiente Kubernetes. È possibile usare il comando **azdata BDC Config list** per elencarli:

   ```bash
   azdata bdc config list
   ```

1. Per personalizzare la distribuzione, creare una copia del profilo di distribuzione con il comando **azdata BDC config init** . Ad esempio, il comando seguente crea una copia dei file di configurazione della distribuzione **AKS-dev-test** in una directory di `custom`destinazione denominata:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > Specifica una directory che contiene i file di configurazione, **cluster. JSON** e **Control. JSON**, in base al `--source` parametro. `--target`

1. Per personalizzare le impostazioni nel profilo di configurazione della distribuzione, è possibile modificare il file di configurazione della distribuzione in uno strumento adatto per la modifica dei file JSON, ad esempio VS Code. Per l'automazione tramite script, è anche possibile modificare il profilo di distribuzione personalizzato usando il comando **azdata BDC config** . Ad esempio, il comando seguente modifica un profilo di distribuzione personalizzato per modificare il nome del cluster distribuito da quello predefinito (**MSSQL-cluster**) a **test-cluster**:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > Uno strumento utile per trovare i percorsi JSON è l' [analizzatore online JSONPath](https://jsonpath.com/).

   Oltre a passare le coppie chiave-valore, è anche possibile fornire valori JSON inline o passare file di patch JSON. Per altre informazioni, vedere [configurare le impostazioni di distribuzione per i cluster Big Data](deployment-custom-configuration.md).

1. Passare quindi il file di configurazione personalizzato a **azdata BDC create**. Si noti che è necessario impostare le [variabili di ambiente](#env)necessarie. in caso contrario, verranno richiesti i valori seguenti:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Per ulteriori informazioni sulla struttura di un file di configurazione della distribuzione, vedere il [riferimento al file di configurazione della distribuzione](reference-deployment-config.md). Per altri esempi di configurazione, vedere [configurare le impostazioni di distribuzione per i cluster Big Data](deployment-custom-configuration.md).

## <a id="env"></a>Variabili di ambiente

Le variabili di ambiente seguenti vengono utilizzate per le impostazioni di sicurezza che non sono archiviate in un file di configurazione della distribuzione. Si noti che le impostazioni di Docker eccetto le credenziali possono essere impostate nel file di configurazione.

| Variabile di ambiente | Requisito |Descrizione |
|---|---|---|
| **CONTROLLER_USERNAME** | Obbligatoria |Nome utente per l'amministratore del cluster. |
| **CONTROLLER_PASSWORD** | Obbligatoria |Password per l'amministratore del cluster. |
| **MSSQL_SA_PASSWORD** | Obbligatoria |Password dell'utente SA per l'istanza di SQL master. |
| **KNOX_PASSWORD** | Obbligatoria |Password per l'utente Knox. |
| **ACCEPT_EULA**| Obbligatorio per il primo utilizzo di`azdata`| Non richiede alcun valore. Quando viene impostato come variabile di ambiente, applica EULA sia a SQL Server `azdata`sia a. Se non è impostato come variabile di ambiente, è `--accept-eula` possibile includere nel primo uso `azdata` del comando.|
| **DOCKER_USERNAME** | Facoltativo | Nome utente per accedere alle immagini del contenitore nel caso in cui vengano archiviate in un repository privato. Per informazioni dettagliate sull'uso di un repository Docker privato per la distribuzione di Big Data cluster, vedere l'argomento [distribuzioni offline](deploy-offline.md) .|
| **DOCKER_PASSWORD** | Facoltativo |Password per accedere al repository privato precedente. |

Queste variabili di ambiente devono essere impostate prima di chiamare **azdata BDC create**. Se una variabile non è impostata, viene richiesta.

L'esempio seguente illustra come impostare le variabili di ambiente per Linux (bash) e Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

Dopo aver impostato le variabili di ambiente, è `azdata bdc create` necessario eseguire per attivare la distribuzione. Questo esempio usa il profilo di configurazione del cluster creato in precedenza:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Tenere presente le linee guida seguenti:

- Se contiene caratteri speciali, assicurarsi di eseguire il wrapping della password tra virgolette doppie. È possibile impostare il **MSSQL_SA_PASSWORD** su quello che si preferisce, ma assicurarsi che la password sia abbastanza complessa e non usare `!`i `&` caratteri `'` o. Si noti che i delimitatori di virgolette doppie funzionano solo nei comandi bash.
- L'account di accesso **sa** è un amministratore di sistema nell'istanza di SQL Server master che viene creata durante l'installazione. Dopo aver creato il contenitore di SQL Server, la variabile di ambiente **MSSQL_SA_PASSWORD** specificata è individuabile eseguendo `echo $MSSQL_SA_PASSWORD` nel contenitore. Per motivi di sicurezza, modificare la password dell'amministratore di sistema in base alle procedure consigliate descritte [qui](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a>Installazione automatica

Per una distribuzione automatica, è necessario impostare tutte le variabili di ambiente necessarie, utilizzare un file di configurazione e chiamare `azdata bdc create` il comando con `--accept-eula yes` il parametro. Negli esempi della sezione precedente viene illustrata la sintassi per un'installazione automatica.

## <a id="monitor"></a>Monitorare la distribuzione

Durante il bootstrap del cluster, la finestra di comando client restituirà lo stato di distribuzione. Durante il processo di distribuzione, verrà visualizzata una serie di messaggi in cui è in attesa del Pod del controller:

```output
Waiting for cluster controller to start.
```

Da 15 a 30 minuti, è necessario ricevere una notifica relativa all'esecuzione del Pod del controller:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo a causa del tempo necessario per scaricare le immagini del contenitore per i componenti del cluster Big Data. Tuttavia, non deve richiedere diverse ore. Se si verificano problemi con la distribuzione, vedere [monitoraggio e risoluzione dei problemi SQL Server cluster di Big Data](cluster-troubleshooting-commands.md).

Al termine della distribuzione, l'output invia una notifica di esito positivo:

```output
Cluster deployed successfully.
```

> [!TIP]
> Il nome predefinito per il cluster Big Data distribuito è `mssql-cluster` a meno che non venga modificato da una configurazione personalizzata.

## <a id="endpoints"></a>Recupera endpoint

Al termine dell'esecuzione dello script di distribuzione, è possibile ottenere gli indirizzi IP degli endpoint esterni per il cluster Big Data usando la procedura seguente.

1. Dopo la distribuzione, trovare l'indirizzo IP dell'endpoint del controller dall'output standard di distribuzione oppure esaminando l'output IP esterno del comando **kubectl** seguente:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se durante la distribuzione non è stato modificato il nome predefinito, `-n mssql-cluster` usare il comando precedente. **MSSQL-cluster** è il nome predefinito per il cluster Big Data.

1. Accedere al cluster di Big Data con l' [account di accesso azdata](reference-azdata.md). Impostare il parametro **--controller-endpoint** sull'indirizzo IP esterno dell'endpoint del controller.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Specificare il nome utente e la password configurati per il controller (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante la distribuzione.

1. Eseguire l' [elenco di endpoint BDC azdata](reference-azdata-bdc-endpoint.md) per ottenere un elenco con una descrizione di ogni endpoint e i valori di porta e indirizzo IP corrispondenti. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   L'elenco seguente mostra l'output di esempio di questo comando:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

È anche possibile ottenere tutti gli endpoint di servizio distribuiti per il cluster eseguendo il comando **kubectl** seguente:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Se si usa minikube, è necessario eseguire il comando seguente per ottenere l'indirizzo IP a cui è necessario connettersi. Oltre all'indirizzo IP, specificare la porta per l'endpoint a cui è necessario connettersi.

```bash
minikube ip
```

## <a id="status"></a>Verificare lo stato del cluster

Dopo la distribuzione, è possibile controllare lo stato del cluster con il comando [azdata BDC status Show](reference-azdata-bdc-status.md) .

```bash
azdata bdc status show -o table
```

> [!TIP]
> Per eseguire i comandi di stato, è necessario prima accedere con il comando **azdata login** , illustrato nella sezione endpoint precedenti.

Di seguito è riportato un esempio di output di questo comando:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

In questo stato di riepilogo è inoltre possibile ottenere uno stato più dettagliato con i comandi seguenti:

- [stato del controllo BDC azdata](reference-azdata-bdc-control-status.md)
- [stato pool BDC azdata](reference-azdata-bdc-pool-status.md)

L'output di questi comandi contiene URL per i dashboard Kibana e Grafana per un'analisi più dettagliata.

Oltre a usare **azdata**, è anche possibile usare Azure Data Studio per trovare sia gli endpoint che le informazioni sullo stato. Per ulteriori informazioni sulla visualizzazione dello stato del cluster con **azdata** e Azure Data Studio, vedere [How to view the status of an Big Data cluster](view-cluster-status.md).

## <a id="connect"></a>Connettersi al cluster

Per altre informazioni su come connettersi al cluster Big Data, vedere [connettersi a un cluster di Big Data SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulla distribuzione di Big Data cluster, vedere le risorse seguenti:

- [Configurare le impostazioni di distribuzione per i cluster di Big Data](deployment-custom-configuration.md)
- [Eseguire una distribuzione offline di un cluster SQL Server Big Data](deploy-offline.md)
- [Workshop Architettura di cluster Big Data Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
