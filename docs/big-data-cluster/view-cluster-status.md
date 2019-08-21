---
title: Visualizzare lo stato del cluster
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come visualizzare lo stato di un cluster Big Data usando Azure Data Studio, i notebook e i comandi di azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 028864712658e35913fa04fb1a85e4ca960ad573
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653279"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Come visualizzare lo stato di un cluster Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come accedere agli endpoint di servizio e visualizzare lo stato di un cluster Big Data di SQL Server (anteprima). È possibile usare sia Azure Data Studio che **azdata** e questo articolo illustra entrambe le tecniche.

## <a id="datastudio"></a> Usare Azure Data Studio

Dopo aver scaricato la versione più recente della **build Insider** di [Azure Data Studio](https://aka.ms/azdata-insiders), e possibile visualizzare gli endpoint di servizio e lo stato di un cluster Big Data con il dashboard dei cluster Big Data di SQL Server. Si noti che alcune delle funzionalità seguenti sono inizialmente disponibili solo per la build Insider di Azure Data Studio.

1. Creare prima di tutto una connessione al cluster Big Data in Azure Data Studio. Per altre informazioni, vedere [Connettersi a un cluster Big Data di SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

1. Fare clic con il pulsante destro del mouse sull'endpoint del cluster Big Data e scegliere **Gestisci**.

   ![Comando Gestisci del menu di scelta rapida](media/view-cluster-status/right-click-manage.png)

1. Selezionare la scheda **SQL Server Big Data Cluster** (Cluster Big Data di SQL Server) per accedere al dashboard dei cluster Big Data.

   ![Dashboard dei cluster Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Endpoint di servizio

È importante poter accedere facilmente ai vari servizi all'interno di un cluster Big Data. Il dashboard dei cluster Big Data fornisce una tabella degli endpoint di servizio che consente di visualizzare e copiare gli endpoint.

![endpoint di servizio](media/view-cluster-status/service-endpoints.png)

Le prime righe espongono i servizi seguenti:

- Proxy dell'applicazione
- Servizio di gestione cluster
- HDFS e Spark
- Proxy di gestione

Questi servizi elencano gli endpoint che è possibile copiare e incollare quando è necessario per la connessione ai servizi. È ad esempio possibile fare clic sull'icona di copia a destra dell'endpoint e quindi incollare quanto copiato in una finestra di testo che richiede tale endpoint. L'endpoint del servizio di gestione cluster è necessario per eseguire il [notebook relativo allo stato del cluster](#notebook).

### <a name="dashboards"></a>Dashboard

La tabella degli endpoint di servizio espone anche diversi dashboard per il monitoraggio:

- Metriche (Grafana)
- Log (Kibana)
- Monitoraggio di processi Spark
- Gestione di risorse di Spark

È possibile fare clic direttamente su questi collegamenti. Viene chiesto due volte di specificare il nome utente e la password prima di connettersi al servizio.

### <a id="notebook"></a> Notebook relativo allo stato del cluster

1. È anche possibile visualizzare lo stato del cluster Big Data avviando il notebook relativo allo stato del cluster. Per avviare il notebook, fare clic sull'attività **Stato cluster**.

    ![avvio](media/view-cluster-status/cluster-status-launch.png)

2. Prima di iniziare, è necessario disporre di quanto segue:

    - Nome del cluster Big Data
    - Nome utente del controller
    - Password del controller
    - Endpoint controller

    Il nome predefinito del cluster Big Data è **mssql-cluster**, a meno che non sia stato personalizzato durante la distribuzione. È possibile trovare l'endpoint controller nel dashboard dei cluster Big Data nella tabella relativa agli endpoint di servizio. L'endpoint è elencato come **Cluster Management Service** (Servizio di gestione cluster). Se non si conoscono le credenziali, rivolgersi all'amministratore che ha distribuito il cluster.

3. Fare clic su **Run Cells** (Esegui celle) sulla barra degli strumenti superiore.

4. Seguire le indicazioni di richiesta delle credenziali. Premere INVIO dopo aver digitato ogni credenziale per il nome del cluster Big Data, il nome utente del controller e la password del controller.

    > [!Note]
    > Se non è disponibile un file di configurazione con i Big Data, verrà richiesto l'endpoint controller. Digitare o incollare l'endpoint e quindi premere INVIO per continuare.

5. Se la connessione viene stabilita correttamente, nel resto del notebook verrà visualizzato l'output di ogni componente del cluster Big Data. Quando si vuole eseguire di nuovo una determinata cella di codice, passare il puntatore sulla cella di codice e fare clic sull'icona **Esegui**.

## <a name="use-azdata"></a>Usare azdata

È anche possibile usare i comandi di [azdata](deploy-install-azdata.md) per visualizzare sia gli endpoint che lo stato del cluster.

### <a name="service-endpoints"></a>Endpoint di servizio

Dopo avere ottenuto gli indirizzi IP degli endpoint esterni per il cluster Big Data, seguire questa procedura.

1. Individuare l'indirizzo IP dell'endpoint controller esaminando l'output EXTERNAL-IP del comando **kubectl** seguente:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se durante la distribuzione non è stato modificato il nome predefinito, usare `-n mssql-cluster` nel comando precedente. **mssql-cluster** è il nome predefinito per il cluster Big Data.

1. Accedere al cluster Big Data con [azdata login](reference-azdata.md). Impostare il parametro **--controller-endpoint** sull'indirizzo IP esterno dell'endpoint controller.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Specificare il nome utente e la password configurati per il controller (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante la distribuzione.

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

### <a name="view-cluster-status"></a>Visualizzare lo stato del cluster

È possibile visualizzare lo stato del cluster con il comando [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show -o table
```

> [!TIP]
> Per eseguire il comando per lo stato, è prima di tutto necessario accedere con il comando **azdata login**, mostrato nella sezione precedente sugli endpoint.

Di seguito viene mostrato un output di esempio di questo comando:

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

### <a name="view-pool-status"></a>Visualizzare lo stato dei pool

Dopo la distribuzione, è possibile visualizzare lo stato dei pool nel cluster con il comando [azdata bdc pool status show](reference-azdata-bdc-pool-status.md). Per usare questo comando, specificare il tipo di pool con il parametro `--kind`. I possibili tipi di pool sono i seguenti:

- compute
- data
- master
- spark
- storage

Ad esempio, il comando seguente visualizza lo stato del pool di archiviazione:

```bash
azdata bdc pool status show --kind storage
```

L'output dovrebbe essere simile al testo seguente:

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

Il valore `logsUrl` fornisce un collegamento a un dashboard Kibana con informazioni di log:

![Dashboard Kibana](./media/view-cluster-status/kibana-dashboard.png)

I valori `nodeMetricsUrl` e `sqlMetricsUrl` forniscono un collegamento a un dashboard Grafana per il monitoraggio dell'integrità dei nodi e delle metriche SQL:

![Dashboard Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Visualizzare lo stato del controller

È possibile visualizzare lo stato del controller con il comando [azdata bdc control status show](reference-azdata-bdc-control-status.md). Questo comando fornisce collegamenti simili ai dashboard di monitoraggio correlati ai nodi del controller del cluster Big Data.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster Big Data, vedere [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)la pagina relativa a.
