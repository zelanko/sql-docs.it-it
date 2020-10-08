---
title: Visualizzare lo stato del cluster
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come visualizzare lo stato di un cluster Big Data usando Azure Data Studio, i notebook e i comandi di azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f5b3b210cb4e20bdf9585a7efdfd0f10aa19f29
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725789"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Come visualizzare lo stato di un cluster Big Data 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come accedere agli endpoint di servizio e visualizzare lo stato dei componenti di un cluster Big Data di SQL Server. È possibile usare sia Azure Data Studio che **azdata** e questo articolo illustra entrambe le tecniche.

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> Usare Azure Data Studio

Dopo aver scaricato la versione più recente della **build Insider** di [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md), e possibile visualizzare gli endpoint di servizio e lo stato di un cluster Big Data con il dashboard dei cluster Big Data di SQL Server. Alcune delle funzionalità seguenti sono inizialmente disponibili solo per la build Insider di Azure Data Studio.

1. Creare prima di tutto una connessione al cluster Big Data in Azure Data Studio. Per altre informazioni, vedere [Connettersi a un cluster Big Data di SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

1. Fare clic con il pulsante destro del mouse sull'endpoint del cluster Big Data e scegliere **Gestisci**.

   ![Comando Gestisci del menu di scelta rapida](media/view-cluster-status/right-click-manage.png)

1. Selezionare la scheda **SQL Server Big Data Cluster** (Cluster Big Data di SQL Server) per accedere al dashboard dei cluster Big Data.

   ![Dashboard dei cluster Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Endpoint di servizio

È importante poter accedere facilmente ai vari servizi all'interno di un cluster Big Data. Il dashboard dei cluster Big Data fornisce una tabella degli endpoint di servizio che consente di visualizzare e copiare gli endpoint.

![endpoint di servizio](media/view-cluster-status/service-endpoints.png)

Questi servizi elencano gli endpoint che è possibile copiare e incollare quando è necessario per la connessione ai servizi. È ad esempio possibile fare clic sull'icona di copia a destra dell'endpoint e quindi incollare quanto copiato in una finestra di testo che richiede tale endpoint. L'endpoint del servizio di gestione cluster è necessario per eseguire il [notebook relativo allo stato del cluster](#notebook).

### <a name="dashboards"></a>Dashboard

La tabella degli endpoint di servizio espone anche diversi dashboard per il monitoraggio:

- Metriche (Grafana)
- Log (Kibana)
- Monitoraggio di processi Spark
- Gestione di risorse di Spark

È possibile fare clic direttamente su questi collegamenti. Verrà richiesto di eseguire l'autenticazione quando si accede a questi dashboard. Per i dashboard delle metriche e dei log, fornire le credenziali di amministratore del controller impostate in fase di distribuzione usando le variabili di ambiente **AZDATA_USERNAME** e **AZDATA_PASSWORD**. I dashboard Spark useranno le credenziali del gateway (Knox), ovvero l'identità di Active Directory in un cluster integrato con AD o **AZDATA_USERNAME** e **AZDATA_PASSWORD** se si usa l'autenticazione di base nel cluster.

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> Notebook relativo allo stato del cluster

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

È anche possibile usare i comandi di [azdata](../azdata/install/deploy-install-azdata.md) per visualizzare sia gli endpoint che lo stato del cluster.

### <a name="service-endpoints"></a>Endpoint di servizio

1. Accedere al cluster Big Data con [azdata login](../azdata/reference/reference-azdata.md). Impostare il parametro **--controller-endpoint** sull'indirizzo IP esterno dell'endpoint controller.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   Specificare il nome utente e la password configurati per il controller (AZDATA_USERNAME e AZDATA_PASSWORD) durante la distribuzione. 
   Per l'autenticazione di Active Directory, il comando è:

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. Eseguire [`azdata bdc endpoint list`](../azdata/reference/reference-azdata-bdc-endpoint.md) per ottenere un elenco con una descrizione di ogni endpoint e i relativi valori di porta e indirizzo IP. 

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

È possibile visualizzare lo stato del cluster con il comando [`azdata bdc status show`](../azdata/reference/reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Per eseguire il comando per lo stato, è prima di tutto necessario accedere con il comando **azdata login**, mostrato nella sezione precedente sugli endpoint.

Di seguito viene mostrato un output di esempio di questo comando:

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


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
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>Visualizzare lo stato di risorse specifiche

È possibile visualizzare lo stato di una risorsa specifica nel cluster con il comando [azdata bdc status show](../azdata/reference/reference-azdata-bdc-status.md). Quando si usa questo comando è possibile filtrare usando il parametro `--resource`. Ecco alcuni esempi di input per il parametro `--resource`:

- master
- controllo
- compute-0
- storage-0
- gateway

Il comando seguente visualizza ad esempio lo stato del pool di archiviazione:

```bash
azdata bdc status show --all --resource storage-0
```

Per visualizzare lo stato di tutti i componenti che eseguono un servizio specifico, è necessario usare il gruppo di comandi corrispondente `azdata bdc <serviceName> status show`. Ad esempio:

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

Ecco un esempio di output:

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> Eseguire il comando relativo allo stato con i parametri `--all` per informazioni aggiuntive sull'integrità, inclusi collegamenti ai dashboard di metriche e log corrispondenti all'istanza specifica. Di seguito è riportato un esempio di output quando vengono usati i parametri `--all`:

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

Il valore `logsUrl` fornisce un collegamento a un dashboard Kibana:

![Dashboard Kibana](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> Il browser Microsoft Edge precedente non è compatibile con Kibana. Per visualizzare il dashboard correttamente, è necessario usare un browser basato su Chromium. Quando si caricano i dashboard usando un browser non supportato, viene visualizzata una pagina vuota. Vedere qui per i browser supportati per Kibana.

I valori `nodeMetricsUrl` e `sqlMetricsUrl` forniscono un collegamento a un dashboard Grafana per il monitoraggio delle metriche dei nodi Kubernetes e delle metriche dei servizi dei cluster Big Data:

![Dashboard Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Visualizzare lo stato del controller

È possibile visualizzare lo stato del controller con il comando [`azdata bdc control status show`](../azdata/reference/reference-azdata-bdc-control-status.md). Questo comando fornisce collegamenti simili ai dashboard di monitoraggio correlati ai componenti del controller del cluster Big Data.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md)