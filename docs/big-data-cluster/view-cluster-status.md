---
title: Visualizzare lo stato del cluster
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come visualizzare lo stato di un cluster di big data usando comandi mssqlctl, notebook e Studio di Azure Data.
author: yualan
ms.author: alayu
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2edd49c37655d420cf8022677c0d0287028a0b93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413968"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Come visualizzare lo stato di un cluster di big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come accedere agli endpoint di servizio e visualizzare lo stato di un cluster di big data di SQL Server (anteprima). È possibile usare entrambi Data Studio di Azure e **mssqlctl**, e questo articolo descrive entrambe le tecniche.

## <a id="datastudio"></a> Usare Studio dei dati di Azure

Dopo aver scaricato la versione più recente **build insiders** dei [Studio di Azure Data](https://aka.ms/azdata-insiders), è possibile visualizzare gli endpoint di servizio e lo stato di un big data del cluster con il dashboard del cluster SQL Server i big Data. Si noti che alcune delle funzionalità riportate di seguito sono innanzitutto disponibili solo nella build Insider di Studio di Azure Data.

1. In primo luogo, creare una connessione al cluster di big data in Azure Data Studio. Per altre informazioni, vedere [Connetti a SQL Server del cluster di big data con Azure Data Studio](connect-to-big-data-cluster.md).

1. Fare doppio clic sull'endpoint cluster dei big data e fare clic su **Gestisci**.

   ![a destra fare clic su Gestisci](media/view-cluster-status/right-click-manage.png)

1. Selezionare il **Cluster di Big Data di SQL Server** pressione di tab per accedere al dashboard del cluster di big data.

   ![Dashboard del cluster dei big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Endpoint di servizio

È importante essere in grado di accedere più facilmente i diversi servizi all'interno di un cluster di big data. Dashboard del cluster di big data fornisce una tabella di endpoint di servizio che consente di visualizzare e copiare l'endpoint del servizio.

![Endpoint di servizio](media/view-cluster-status/service-endpoints.png)

Le prime righe diversi espongono i servizi seguenti:

- Proxy dell'applicazione
- Servizio di Gestione cluster
- HDFS e Spark
- Proxy di gestione

Questi servizi elencare gli endpoint che possono essere copiati e incollati quando è necessario l'endpoint per la connessione a tali servizi. Ad esempio, è possibile fare clic sull'icona di copia a destra dell'endpoint e quindi incollarla in una finestra di testo che richiede che l'endpoint. L'endpoint del servizio di gestione di Cluster è necessario eseguire la [notebook di stato cluster](#notebook).

### <a name="dashboards"></a>Dashboard

La tabella di endpoint di servizio espone anche diversi dashboard per il monitoraggio:

- Metriche (Grafana)
- Log (Kibana)
- Monitoraggio dei processi di Spark
- Gestione delle risorse di Spark

È possibile fare direttamente clic su tali collegamenti. Viene chiesto di immettere due volte per fornire il nome utente e la password prima di connettersi al servizio.

### <a id="notebook"></a> Notebook lo stato del cluster

1. È anche possibile visualizzare lo stato del cluster del cluster di big data, avviare il notebook lo stato del Cluster. Per avviare il notebook, fare clic il **lo stato del Cluster** attività.

    ![avvio veloce](media/view-cluster-status/cluster-status-launch.png)

2. Prima di iniziare, sono necessari gli elementi seguenti:

    - Nome del cluster di big data
    - Nome utente controller
    - Password del controlle
    - Endpoint controller

    Il nome del cluster di big data predefinito è **mssql-cluster** a meno che non è stato personalizzato durante la distribuzione. Nella tabella gli endpoint di servizio, è possibile trovare l'endpoint controller dal dashboard del cluster di big data. L'endpoint viene elencato come **servizio di gestione Cluster**. Se non si conosce le credenziali, chiedere all'amministratore che ha distribuito il cluster.

3. Fare clic su **eseguire le celle** sulla barra degli strumenti superiore.

4. Attenersi alla richiesta delle credenziali. Premere INVIO dopo aver ogni credenziale per il nome del cluster di big data, controller il nome utente e la password del controlle di tipo.

    > [!Note]
    > Se non è un programma di installazione di file di configurazione con i big data, verrà richiesto per l'endpoint del controller. Digitare o incollare il codice e quindi premere INVIO per continuare.

5. Se connesso correttamente, il resto del notebook verrà visualizzato l'output di ogni componente del cluster di big data. Quando si desidera eseguire nuovamente una determinati cella di codice, passare il mouse su una cella di codice e scegliere il **eseguire** icona.

## <a name="use-mssqlctl"></a>Usare mssqlctl

È anche possibile usare [mssqlctl](deploy-install-mssqlctl.md) comandi per visualizzare gli endpoint e lo stato del cluster.

### <a name="service-endpoints"></a>Endpoint di servizio

È possibile ottenere gli indirizzi IP degli endpoint esterni per il cluster di big data usando la procedura seguente.

1. Trovare l'indirizzo IP dell'endpoint del controller, esaminando l'output di EXTERNAL-IP di quanto segue **kubectl** comando:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se non è modificato il nome predefinito durante la distribuzione, usare `-n mssql-cluster` nel comando precedente. **MSSQL-cluster** è il nome predefinito per il cluster di big data.

1. Accedere al cluster di big data con [mssqlctl login](reference-mssqlctl.md). Impostare il **-controller-endpoint** parametro per l'indirizzo IP esterno dell'endpoint del controller.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Specificare il nome utente e la password configurata per il controller (CONTROLLER_USERNAME e CONTROLLER_PASSWORD) durante la distribuzione.

1. Eseguire [elenco di endpoint di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-endpoint.md) per ottenere un elenco con una descrizione di ogni endpoint e i relativi valori di porta e indirizzo IP. 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   L'elenco seguente mostra l'output di esempio da questo comando:

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

È possibile visualizzare lo stato del cluster con il [Mostra lo stato di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-status.md) comando.

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> Per eseguire i comandi di stato, è prima necessario accedere con il **mssqlctl login** comando, che è stato illustrato nella sezione endpoint precedente.

Il seguente esempio di output da questo comando:

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

### <a name="view-pool-status"></a>Visualizzare lo stato del pool

È possibile visualizzare lo stato dei pool all'interno del cluster con il [Mostra lo stato del pool di mssqlctl bdc](reference-mssqlctl-bdc-pool-status.md) comando. Per usare questo comando, specificare il tipo di pool con la `--kind` parametro. I tipi di pool sono:

- Calcolo
- data
- master
- Spark
- Archiviazione

Ad esempio, il comando seguente consente di visualizzare lo stato del pool del pool di archiviazione:

```bash
mssqlctl bdc pool status show --kind storage
```

Testo dovrebbe essere simile all'output seguente:

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

Il `logsUrl` valore collegamenti a un dashboard kibana con le informazioni sul log:

![dashboard kibana](./media/view-cluster-status/kibana-dashboard.png)

Il `nodeMetricsUrl` e `sqlMetricsUrl` collegano valori a un dashboard di grafana per il monitoraggio di integrità del nodo e le metriche SQL:

![Grafana dashboard](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Stato del controller di visualizzazione

È possibile visualizzare lo stato del controller con la [mssqlctl integrazione applicativa dei dati controllo stato Mostra](reference-mssqlctl-bdc-control-status.md) comando. Vengono forniti collegamenti simili per il dashboard di monitoraggio correlate ai nodi del controller del cluster di big data.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server i big data](big-data-cluster-overview.md).
