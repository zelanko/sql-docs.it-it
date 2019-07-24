---
title: Visualizzare lo stato del cluster
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come visualizzare lo stato di un cluster Big Data usando i comandi Azure Data Studio, Notebooks e azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419285"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Come visualizzare lo stato di un cluster di Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come accedere agli endpoint di servizio e visualizzare lo stato di un cluster SQL Server Big Data (anteprima). È possibile usare sia Azure Data Studio che **azdata**e questo articolo illustra entrambe le tecniche.

## <a id="datastudio"></a>USA Azure Data Studio

Dopo aver scaricato la **Build** più recente di [Azure Data Studio](https://aka.ms/azdata-insiders), è possibile visualizzare gli endpoint del servizio e lo stato di un cluster Big data con il dashboard di SQL Server Big Data cluster. Si noti che alcune delle funzionalità seguenti sono disponibili solo per la prima volta nella compilazione Insider di Azure Data Studio.

1. Per prima cosa, creare una connessione al cluster Big Data in Azure Data Studio. Per altre informazioni, vedere [connettersi a un cluster SQL Server Big data con Azure Data Studio](connect-to-big-data-cluster.md).

1. Fare clic con il pulsante destro del mouse sull'endpoint del cluster Big Data e scegliere Gestisci.

   ![pulsante destro del mouse su Gestisci](media/view-cluster-status/right-click-manage.png)

1. Selezionare la scheda **cluster SQL Server Big Data** per accedere al dashboard del cluster di Big Data.

   ![Dashboard del cluster di Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Endpoint di servizio

È importante poter accedere facilmente ai vari servizi all'interno di un cluster Big Data. Il dashboard del cluster Big Data fornisce una tabella degli endpoint di servizio che consente di visualizzare e copiare gli endpoint di servizio.

![endpoint di servizio](media/view-cluster-status/service-endpoints.png)

Le prime righe espongono i servizi seguenti:

- Proxy di applicazione
- Servizio Gestione cluster
- HDFS e Spark
- Proxy di gestione

Questi servizi elencano gli endpoint che possono essere copiati e incollati quando è necessario l'endpoint per la connessione a tali servizi. Ad esempio, è possibile fare clic sull'icona di copia a destra dell'endpoint e quindi incollarla in una finestra di testo che richiede tale endpoint. L'endpoint del servizio Gestione cluster è necessario per eseguire il [notebook di stato del cluster](#notebook).

### <a name="dashboards"></a>Dashboard

La tabella endpoint di servizio espone inoltre diversi dashboard per il monitoraggio:

- Metriche (Grafana)
- Log (Kibana)
- Monitoraggio processi Spark
- Gestione delle risorse Spark

È possibile fare clic direttamente su questi collegamenti. Viene chiesto due volte di specificare il nome utente e la password prima di connettersi al servizio.

### <a id="notebook"></a>Notebook stato del cluster

1. È anche possibile visualizzare lo stato del cluster del cluster di Big Data avviando il notebook dello stato del cluster. Per avviare il notebook, fare clic sull'attività **stato cluster** .

    ![Avviare](media/view-cluster-status/cluster-status-launch.png)

2. Prima di iniziare, saranno necessari gli elementi seguenti:

    - Nome del cluster di Big Data
    - Nome utente controller
    - Password controller
    - Endpoint controller

    Il nome predefinito del cluster Big Data è **MSSQL-cluster** , a meno che non sia stato personalizzato durante la distribuzione. È possibile trovare l'endpoint controller dal dashboard del cluster Big Data nella tabella degli endpoint di servizio. L'endpoint è elencato come **servizio di gestione cluster**. Se non si conoscono le credenziali, rivolgersi all'amministratore che ha distribuito il cluster.

3. Fare clic su **Esegui celle** sulla barra degli strumenti in alto.

4. Seguire la richiesta delle credenziali. Premere il tasto INVIO dopo aver digitato ogni credenziale per il nome del cluster Big Data, il nome utente del controller e la password del controller.

    > [!Note]
    > Se non si dispone di un file di configurazione configurato con il Big Data, verrà richiesto l'endpoint del controller. Digitare o incollare il testo, quindi premere INVIO per continuare.

5. Se la connessione è stata eseguita correttamente, nel resto del notebook viene visualizzato l'output di ogni componente del cluster Big Data. Quando si desidera eseguire nuovamente una determinata cella di codice, passare il mouse sulla cella di codice e fare clic sull'icona **Esegui** .

## <a name="use-azdata"></a>Usare azdata

È anche possibile usare i comandi [azdata](deploy-install-azdata.md) per visualizzare sia gli endpoint che lo stato del cluster.

### <a name="service-endpoints"></a>Endpoint di servizio

È possibile ottenere gli indirizzi IP degli endpoint esterni per il cluster Big Data usando la procedura seguente.

1. Trovare l'indirizzo IP dell'endpoint controller osservando l'output IP esterno del comando **kubectl** seguente:

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

### <a name="view-cluster-status"></a>Visualizzare lo stato del cluster

È possibile visualizzare lo stato del cluster con il comando [azdata BDC status Show](reference-azdata-bdc-status.md) .

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

### <a name="view-pool-status"></a>Visualizza lo stato del pool

È possibile visualizzare lo stato dei pool nel cluster con il comando [azdata BDC pool status Show](reference-azdata-bdc-pool-status.md) . Per usare questo comando, specificare il tipo di pool con il `--kind` parametro. I tipi di pool sono:

- Calcolare
- data
- master
- Scintilla
- Archiviazione

Ad esempio, il comando seguente visualizza lo stato del pool di archiviazione:

```bash
azdata bdc pool status show --kind storage
```

Verrà visualizzato un testo simile all'output seguente:

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

Il `logsUrl` valore si collega a un dashboard di Kibana con le informazioni di log:

![Dashboard di Kibana](./media/view-cluster-status/kibana-dashboard.png)

I `nodeMetricsUrl` valori `sqlMetricsUrl` e si collegano a un dashboard di grafana per il monitoraggio dell'integrità del nodo e della metrica SQL:

![Dashboard di Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Visualizza lo stato del controller

È possibile visualizzare lo stato del controller con il comando [azdata BDC Control Status Show](reference-azdata-bdc-control-status.md) . Fornisce collegamenti simili ai dashboard di monitoraggio correlati ai nodi controller del cluster Big Data.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa sono i cluster SQL Server Big Data](big-data-cluster-overview.md).
