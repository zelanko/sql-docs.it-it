---
title: Linee guida per la distribuzione
titleSuffix: SQL Server Big Data Clusters
description: Informazioni su come distribuire cluster Big Data di SQL Server in Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 94e2fe49e52ed224a35183f9629bf8eeab112d17
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831600"
---
# <a name="how-to-deploy-big-data-clusters-2019-on-kubernetes"></a>Come distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un cluster Big Data di SQL Server viene distribuito come contenitore Docker in un cluster Kubernetes. Questa è una panoramica dei passaggi di installazione e configurazione:

- Configurare un cluster Kubernetes in una singola macchina virtuale, in un cluster di macchine virtuali o nel servizio Azure Kubernetes.
- Installare lo strumento di configurazione dei cluster `azdata` nel computer client.
- Distribuire un cluster Big Data di SQL Server in un cluster Kubernetes.

## <a name="install-sql-server-2019-big-data-tools"></a>Installare gli strumenti per Big Data di SQL Server 2019

Prima di distribuire un cluster Big Data di SQL Server 2019, [installare innanzitutto gli strumenti per Big Data](deploy-big-data-tools.md):

- `azdata`
- `kubectl`
- Azure Data Studio
- [Estensione di virtualizzazione dei dati](../azure-data-studio/data-virtualization-extension.md) per Azure Data Studio

## <a id="prereqs"></a> Prerequisiti per Kubernetes

I [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] richiedono la versione minima di Kubernetes 1.13 sia per il server sia per il client (kubectl).

> [!NOTE]
> Le versioni client e server di Kubernetes devono essere comprese tra le versioni secondarie +1 e -1. Per altre informazioni, vedere [Note sulla versione di Kubernetes e criteri per gli SKU relativi alla differenza tra versioni](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Installazione del cluster Kubernetes

Se è già presente un cluster Kubernetes che soddisfa i prerequisiti indicati sopra, è possibile passare direttamente alla [fase di distribuzione](#deploy). Questa sezione presuppone una conoscenza di base dei concetti relativi a Kubernetes.  Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes](https://kubernetes.io/docs/home).

È possibile scegliere di distribuire Kubernetes in uno dei tre modi seguenti:

| Distribuire in Kubernetes in: | Descrizione | Collegamento |
|---|---|---|
| **Servizio Azure Kubernetes** | Servizio contenitore Kubernetes gestito in Azure. | [Istruzioni](deploy-on-aks.md) |
| **Uno o più computer (`kubeadm`)** | Un cluster Kubernetes distribuito in computer fisici o macchine virtuali tramite `kubeadm` | [Istruzioni](deploy-with-kubeadm.md) |

> [!TIP]
> È anche possibile usare uno script per distribuire il servizio Azure Kubernetes e un cluster Big Data in un unico passaggio. Per altre informazioni, vedere come eseguire questa operazione in uno [script Python](quickstart-big-data-cluster-deploy.md) o in un [notebook](deploy-notebooks.md) di Azure Data Studio.

### <a name="verify-kubernetes-configuration"></a>Verificare la configurazione di Kubernetes

Eseguire il comando `kubectl` per visualizzare la configurazione del cluster. Assicurarsi che kubectl punti al contesto del cluster corretto.

```bash
kubectl config view
```

> [!Important] 
> Se si esegue la distribuzione in un cluster Kubernetes a più nodi che è stato avviato automaticamente con `kubeadm`, prima di avviare la distribuzione del cluster Big Data assicurarsi che gli orologi siano sincronizzati tra tutti i nodi Kubernetes cui è destinata la distribuzione. Il cluster Big Data include proprietà di stato predefinite per diversi servizi che sono sensibili al tempo e le differenze di orario possono causare errori relativi allo stato.

Dopo aver configurato il cluster Kubernetes, è possibile procedere con la distribuzione di un nuovo cluster Big Data di SQL Server. Se si esegue l'aggiornamento da una versione precedente, vedere [Come aggiornare [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

## <a name="ensure-you-have-storage-configured"></a>Verificare che sia stata configurata l'archiviazione

Per la maggior parte delle distribuzioni di cluster Big Data deve essere disponibile un archivio permanente. Al momento, è necessario assicurarsi di avere un piano per implementare un archivio permanente nel cluster Kubernetes prima di distribuire il cluster Big Data.

Se si esegue la distribuzione nel servizio Azure Kubernetes, non occorre configurare l'archiviazione. Il servizio Azure Kubernetes fornisce classi di archiviazione predefinite con provisioning dinamico. È possibile personalizzare la classe di archiviazione (`default` o `managed-premium`) nel file di configurazione della distribuzione. I profili predefiniti usano una classe di archiviazione `default`. Se si esegue la distribuzione in un cluster Kubernetes distribuito con `kubeadm`, è necessario assicurarsi di disporre di spazio di archiviazione sufficiente per un cluster con la scala desiderata e configurato per l'uso. Se si desidera personalizzare la modalità d'uso dell'archiviazione, è necessario farlo prima di procedere. Vedere [Salvataggio permanente dei dati con un cluster Big Data di SQL Server in Kubernetes](concept-data-persistence.md).

## <a id="deploy"></a> Panoramica della distribuzione

La maggior parte delle impostazioni del cluster Big Data è definita in un file di configurazione della distribuzione JSON. È possibile usare un profilo di distribuzione predefinito per il servizio Azure Kubernetes e cluster Kubernetes creati con `kubeadm` oppure è possibile personalizzare il file di configurazione della distribuzione da usare durante l'impostazione. Per motivi di sicurezza, le impostazioni di autenticazione vengono passate tramite variabili di ambiente.

Le sezioni seguenti forniscono altri dettagli su come configurare le distribuzioni di cluster Big Data, nonché alcuni esempi di personalizzazioni comuni. Inoltre, è sempre possibile modificare il file di configurazione della distribuzione personalizzato usando, ad esempio, un editor come VS Code.

## <a id="configfile"></a> Configurazioni predefinite

Le opzioni di distribuzione dei cluster Big Data sono definite in un file di configurazione della distribuzione JSON. È possibile avviare la personalizzazione della distribuzione del cluster dai profili di distribuzione predefiniti disponibili in `azdata`. 

> [!NOTE]
> Le immagini del contenitore necessarie per la distribuzione del cluster Big Data vengono ospitate nel registro contenitori di Microsoft (`mcr.microsoft.com`) nel repository `mssql/bdc`. Per impostazione predefinita, queste impostazioni sono già incluse nel file di configurazione `control.json` in ognuno dei profili di distribuzione inclusi con `azdata`. Inoltre, il tag dell'immagine del contenitore per ogni versione viene immesso automaticamente nello stesso file di configurazione. Se è necessario eseguire il pull delle immagini del contenitore nel registro contenitori privato e modificare le impostazioni del registro contenitori/repository, seguire le istruzioni contenute nell'[articolo sull'installazione offline](deploy-offline.md)

Eseguire questo comando per trovare i modelli disponibili:

```
azdata bdc config list -o table 
```

Ad esempio, per la versione SQL Server 2019 RTM Servicing Update (GDR1), il codice precedente restituisce:

```
Result
----------------
aks-dev-test
aks-dev-test-ha
kubeadm-dev-test
kubeadm-prod
```

| Profilo di distribuzione | Ambiente Kubernetes |
|---|---|
| `aks-dev-test` | Distribuzione di un cluster Big Data di SQL Server nel servizio Azure Kubernetes|
| `aks-dev-test-ha` | Distribuzione di un cluster Big Data di SQL Server nel servizio Azure Kubernetes. I servizi cruciali come l'istanza master di SQL Server e il nodo NameNode di HDFS vengono configurati per la disponibilità elevata.|
| `kubeadm-dev-test` | Distribuzione di un cluster Big Data di SQL Server in un cluster Kubernetes creato con kubeadm tramite uno o più computer fisici o macchine virtuali.|
| `kubeadm-prod`| Distribuzione di un cluster Big Data di SQL Server in un cluster Kubernetes creato con kubeadm tramite uno o più computer fisici o macchine virtuali. Usare questo modello per abilitare l'integrazione dei servizi del cluster Big Data con Active Directory. I servizi cruciali come l'istanza master di SQL Server e il nodo NameNode di HDFS vengono distribuiti in una configurazione a disponibilità elevata.  |

È possibile distribuire un cluster Big Data eseguendo `azdata bdc create`. Verrà chiesto di scegliere una delle configurazioni predefinite e quindi verranno presentati i passaggi di distribuzione.

La prima volta che si esegue `azdata`, è necessario includere `--accept-eula=yes` per accettare le condizioni del contratto di licenza con l'utente finale.

```bash
azdata bdc create --accept-eula=yes
```

In questo scenario vengono chieste le impostazioni che non fanno parte della configurazione predefinita, ad esempio le password. 

> [!IMPORTANT]
> Il nome predefinito del cluster Big Data è `mssql-cluster`. Questo dato è importante per eseguire tutti i comandi `kubectl` che specificano lo spazio dei nomi di Kubernetes con il parametro `-n`.

## <a id="customconfig"></a> Configurazioni personalizzate

È anche possibile personalizzare la distribuzione per gestire i carichi di lavoro che si prevede di eseguire. Si noti che non è possibile modificare la scalabilità (numero di repliche) o le impostazioni di archiviazione per i servizi del cluster Big Data dopo la distribuzione e di conseguenza è necessario pianificare attentamente la configurazione della distribuzione per evitare problemi di capacità. Per personalizzare la distribuzione, eseguire queste operazioni:

1. Iniziare con uno dei profili di distribuzione standard che corrispondono all'ambiente Kubernetes. È possibile usare il comando `azdata bdc config list` per elencarli:

   ```bash
   azdata bdc config list
   ```

1. Per personalizzare la distribuzione, creare una copia del profilo di distribuzione con il comando `azdata bdc config init`. Ad esempio, il comando seguente crea una copia dei file di configurazione della distribuzione `aks-dev-test` in una directory di destinazione denominata `custom`:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   >[!TIP]
   >`--target` specifica una directory che contiene i file di configurazione `bdc.json` e `control.json` in base al parametro `--source`.

1. Per personalizzare le impostazioni nel profilo di configurazione della distribuzione, è possibile modificare il file di configurazione della distribuzione in uno strumento adatto per la modifica dei file JSON, ad esempio VS Code. Per l'automazione tramite script, è anche possibile modificare il profilo di distribuzione personalizzato tramite il comando `azdata bdc config`. Ad esempio, il comando seguente modifica un profilo di distribuzione personalizzato in modo da cambiare il nome del cluster distribuito rispetto a quello predefinito (`mssql-cluster`) a `test-cluster`:  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > È anche possibile passare il nome del cluster in fase di distribuzione usando il parametro *--name* per il comando *azdata create bdc*. I parametri nel comando hanno la precedenza sui valori nei file di configurazione.
   >
   > Uno strumento utile per trovare i percorsi JSON è [JSONPath Online Evaluator](https://jsonpath.com/).
   >
   Oltre a passare coppie chiave-valore, è anche possibile fornire valori JSON inline o passare file di patch JSON. Per altre informazioni, vedere [Configurare le impostazioni di distribuzione per cluster Big Data](deployment-custom-configuration.md).

1. Passare quindi il file di configurazione personalizzato a `azdata bdc create`. Si noti che è necessario impostare le [variabili di ambiente](#env) necessarie o il terminale richiederà i valori:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Per altre informazioni sulla struttura di un file di configurazione della distribuzione, vedere [Informazioni di riferimento sul file di configurazione della distribuzione](reference-deployment-config.md). Per altri esempi di configurazione, vedere [Configurare le impostazioni di distribuzione per cluster Big Data](deployment-custom-configuration.md).

## <a id="env"></a> Variabili di ambiente

Le variabili di ambiente seguenti vengono usate per le impostazioni di sicurezza che non sono archiviate in un file di configurazione della distribuzione. Ad eccezione delle credenziali, le impostazioni di Docker possono essere impostate nel file di configurazione.

| Variabile di ambiente | Requisito |Descrizione |
|---|---|---|
| `AZDATA_USERNAME` | Obbligatoria |Nome utente dell'amministratore del cluster Big Data di SQL Server. Viene creato un account di accesso sysadmin con lo stesso nome nell'istanza master di SQL Server. Come procedura consigliata per la sicurezza, l'account `sa` è disabilitato. |
| `AZDATA_PASSWORD` | Obbligatoria |Password per gli account utente creati sopra. La stessa password viene usata per l'utente `root`, usato per la protezione del gateway Knox e HDFS. |
| `ACCEPT_EULA`| Obbligatoria per il primo utilizzo di `azdata`| Impostata su "yes". Quando è impostata come variabile di ambiente, applica il contratto di licenza con l'utente finale a SQL Server e a `azdata`. Se non è impostata come variabile di ambiente, è possibile includere `--accept-eula=yes` al primo utilizzo del comando `azdata`.|
| `DOCKER_USERNAME` | Facoltativo | Nome utente per accedere alle immagini del contenitore se sono archiviate in un repository privato. Per altre informazioni su come usare un repository Docker privato per la distribuzione di cluster Big Data, vedere l'argomento [Distribuzioni offline](deploy-offline.md).|
| `DOCKER_PASSWORD` | Facoltativo |Password per accedere al repository privato citato sopra. |

Queste variabili di ambiente devono essere impostate prima di chiamare `azdata bdc create`. Se una qualsiasi delle variabili non è impostata, viene chiesto di farlo.

L'esempio seguente mostra come impostare le variabili di ambiente per Linux (Bash) e Windows (PowerShell):

```bash
export AZDATA_USERNAME=admin
export AZDATA_PASSWORD=<password>
export ACCEPT_EULA=yes
```

```PowerShell
SET AZDATA_USERNAME=admin
SET AZDATA_PASSWORD=<password>
```

> [!NOTE]
> È necessario usare l'utente `root` per il gateway Knox con la password precedente. `root` è l'unico utente supportato per in questa configurazione di autenticazione di base (nome utente/password).
> Per connettersi a SQL Server con l'autenticazione di base, usare gli stessi valori delle [variabili di ambiente](#env) AZDATA_USERNAME e AZDATA_PASSWORD. 


Dopo aver impostato le variabili di ambiente, è necessario eseguire `azdata bdc create` per attivare la distribuzione. Questo esempio usa il profilo di configurazione del cluster creato sopra:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Tenere presenti le linee guida seguenti:

- Assicurarsi di racchiudere la password tra virgolette doppie se contiene caratteri speciali. È possibile impostare `AZDATA_PASSWORD` su qualsiasi valore desiderato, ma assicurarsi che la password sia sufficientemente complessa e non contenga i caratteri `!`, `&` e `'`. Le virgolette doppie funzionano come delimitatori solo nei comandi di Bash.
- L'account di accesso `AZDATA_USERNAME` è un amministratore di sistema nell'istanza master di SQL Server che viene creato durante la configurazione. Dopo aver creato il contenitore SQL Server, la variabile di ambiente `AZDATA_PASSWORD` specificata diventa individuabile eseguendo `echo $AZDATA_PASSWORD` nel contenitore. Per motivi di sicurezza, la procedura consigliata richiede la modifica della password.

## <a id="unattended"></a> Installazione automatica

Per una distribuzione automatica, è necessario impostare tutte le variabili di ambiente obbligatorie, usare un file di configurazione e chiamare il comando `azdata bdc create` con il parametro `--accept-eula yes`. Gli esempi forniti nella sezione precedente mostrano la sintassi per un'installazione automatica.

## <a id="monitor"></a> Monitorare la distribuzione

Durante l'avvio automatico del cluster la finestra di comando client restituisce lo stato della distribuzione. Durante il processo di distribuzione dovrebbe essere visualizzata una serie di messaggi che indicano che il processo è in attesa del pod del controller:

```output
Waiting for cluster controller to start.
```

Dopo 15 o 30 minuti si riceverà una notifica che indica che il pod del controller è in esecuzione:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo, necessario per scaricare le immagini dei contenitori per i componenti del cluster Big Data. Non dovrebbero tuttavia essere necessarie diverse ore. In caso di problemi durante la distribuzione, vedere [Monitoraggio e risoluzione dei problemi dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md).

Al termine della distribuzione, l'output segnala l'esito positivo:

```output
Cluster deployed successfully.
```

> [!TIP]
> Il nome predefinito per il cluster Big Data distribuito è `mssql-cluster`, a meno che non venga modificato da una configurazione personalizzata.

## <a id="endpoints"></a> Recuperare gli endpoint

Dopo aver eseguito lo script di distribuzione, è possibile ottenere gli indirizzi degli endpoint esterni per il cluster Big Data completando i passaggi seguenti.

1. Dopo la distribuzione, individuare l'indirizzo IP dell'endpoint controller dall'output standard della distribuzione o cercando nell'output EXTERNAL-IP del comando `kubectl` seguente:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se durante la distribuzione non è stato modificato il nome predefinito, usare `-n mssql-cluster` nel comando precedente. `mssql-cluster` è il nome predefinito per il cluster Big Data.

1. Accedere al cluster Big Data con [azdata login](reference-azdata.md). Impostare il parametro `--endpoint` sull'indirizzo IP esterno dell'endpoint controller.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   Specificare il nome utente e la password configurati per l'amministratore del cluster Big Data (AZDATA_USERNAME e AZDATA_PASSWORD) durante la distribuzione.

   > [!TIP]
   > Un amministratore del cluster Kubernetes che ha accesso al file di configurazione del cluster (file config kube) può configurare il contesto corrente in modo che punti al cluster Kubernetes di destinazione. In questo caso, è possibile accedere con `azdata login -n <namespaceName>`, dove `namespace` è il nome del cluster Big Data. Vengono richieste le credenziali se non sono specificate nel comando per l'accesso.
   
1. Eseguire [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) per ottenere un elenco con una descrizione di ogni endpoint, insieme ai valori di indirizzo IP e porta corrispondenti. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   L'elenco seguente mostra un output di esempio di questo comando:

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

È anche possibile ottenere tutti gli endpoint di servizio distribuiti per il cluster eseguendo il comando `kubectl` seguente:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a id="status"></a> Verificare lo stato del cluster

Dopo la distribuzione, è possibile controllare lo stato del cluster con il comando [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Per eseguire il comando per lo stato, è necessario prima di tutto accedere con il comando `azdata login`, mostrato nella sezione precedente sugli endpoint.

Di seguito viene mostrato un output di esempio di questo comando:

```output
Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 sql            ready    healthy         -
 hdfs           ready    healthy         -
 spark          ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

È anche possibile ottenere informazioni più dettagliate sullo stato con i comandi seguenti:

- [azdata bdc control status show](reference-azdata-bdc-control-status.md) restituisce lo stato di integrità di tutti i componenti associati al servizio di gestione dei controlli
```
azdata bdc control status show
```
Output di esempio:
```output
Control: ready                                                                                                                                                                                                      Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
```

- `azdata bdc sql status show` restituisce lo stato di integrità di tutte le risorse che hanno un servizio SQL Server
```
azdata bdc sql status show
```
Output di esempio:
```output
Sql: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
```

> [!IMPORTANT]
> Quando si usa il parametro `--all`, l'output di questi comandi contiene gli URL dei dashboard di Kibana e Grafana per un'analisi più dettagliata.

Oltre a `azdata`, è anche possibile usare Azure Data Studio per trovare sia gli endpoint sia le informazioni sullo stato. Per altre informazioni sulla visualizzazione dello stato del cluster con `azdata` e Azure Data Studio, vedere [Come visualizzare lo stato di un cluster Big Data](view-cluster-status.md).

## <a id="connect"></a> Connettersi al cluster

Per altre informazioni su come connettersi al cluster Big Data, vedere [Connettersi a un cluster Big Data di SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla distribuzione di cluster Big Data, vedere le risorse seguenti:

- [Configurare le impostazioni di distribuzione per cluster Big Data](deployment-custom-configuration.md)
- [Eseguire una distribuzione offline di un cluster Big Data di SQL Server](deploy-offline.md)
- [Workshop: Architettura Microsoft dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
