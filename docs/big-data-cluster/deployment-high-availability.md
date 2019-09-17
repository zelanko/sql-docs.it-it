---
title: Distribuire SQL Server cluster di Big data con disponibilità elevata
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: Informazioni su come distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (anteprima) a con disponibilità elevata.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 307697f43fc1c2615f212ae5f433485814dd62d0
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874700"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>Distribuire SQL Server cluster di Big data con disponibilità elevata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Al momento della distribuzione di un cluster di Big Data (BDC), è possibile configurare SQL Server master per la distribuzione in una configurazione del gruppo di disponibilità. Questa configurazione aumenta l'affidabilità di SQL Server Master, oltre a ciò che l'infrastruttura Kubernetes Abilita con il monitoraggio dell'integrità incorporato, il rilevamento degli errori e i meccanismi di failover. I gruppi di disponibilità (AG) aggiungono ridondanza all'istanza di SQL Server. In questa configurazione, il monitoraggio, il rilevamento degli errori e le attività di failover vengono gestiti da Big Data servizio di gestione cluster, ovvero il servizio di controllo.

Inoltre, le altre attività amministrative come la configurazione degli endpoint del mirroring del database, la creazione del gruppo di disponibilità e l'aggiunta di database al gruppo di disponibilità sono fornite dalla piattaforma del cluster Big Data.

Di seguito sono riportate alcune delle funzionalità abilitate dai gruppi di disponibilità:

1. Se nel file di configurazione della distribuzione vengono specificate le impostazioni di disponibilità elevata, viene creato un `containedag` singolo gruppo di disponibilità denominato. Per impostazione predefinita `containedag` , in sono presenti tre repliche, inclusa quella primaria. Tutte le operazioni CRUD per il gruppo di disponibilità sono gestite internamente.
1. Tutti i database vengono aggiunti automaticamente al gruppo di disponibilità, `master` tra `msdb`cui e. I database di configurazione di base non sono inclusi nel gruppo di disponibilità perché includono metadati a livello di istanza specifici di ogni replica.
1. Viene eseguito automaticamente il provisioning di un endpoint esterno per la connessione ai database del gruppo di disponibilità. Questo endpoint `master-svc-external` svolge il ruolo di listener del gruppo di disponibilità.
1. Viene eseguito il provisioning di un secondo endpoint esterno per le connessioni di sola lettura alle repliche secondarie. 


# <a name="deploy"></a>Distribuzione

Per distribuire SQL Server Master in un gruppo di disponibilità:

1. Abilitare la `hadr` funzionalità
1. Specificare il numero di repliche per il gruppo di disponibilità (il valore minimo è 3)
1. Configurare i dettagli del secondo endpoint esterno creato per le connessioni alle repliche secondarie di sola lettura

Nei passaggi seguenti viene illustrato come creare un file di patch che include queste impostazioni e come applicarlo ai profili `aks-dev-test` di `kubeadm-dev-test` configurazione o. Questi passaggi illustrano un esempio di come applicare la patch `aks-dev-test` al profilo per aggiungere gli attributi a disponibilità elevata. Per una distribuzione in un cluster kubeadm, è possibile applicare una patch simile, ma assicurarsi *di usare* Deport per il **serviceType** nella sezione **endpoint** .

1. Creazione di `patch.json` un file

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. Clonare il profilo di destinazione

    ```bash
    azdata bdc config init --source aks-dev-test --target custom-aks
    ```

1. Applicare il file di patch al profilo personalizzato

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```

## <a name="connect-to-sql-server-databases"></a>Connettersi a database di SQL Server

A seconda del tipo di carico di lavoro che si vuole eseguire con SQL Server Master, è possibile connettersi al database primario per i carichi di lavoro di lettura/scrittura o ai database nelle repliche secondarie per il tipo di carico di lavoro di sola lettura. Di seguito è riportato un contorno per ogni tipo di connessione:

### <a name="connect-to-databases-on-the-primary-replica"></a>Connettersi ai database nella replica primaria

Per le connessioni alla replica primaria, usare `sql-server-master` endpoint. Questo endpoint è anche il listener del gruppo di disponibilità. Tutte le connessioni si trovano nel contesto del gruppo di disponibilità. Ad esempio, una connessione predefinita che utilizza questo endpoint comporterà la connessione `master` al database all'interno del gruppo di disponibilità, `master` non il database dell'istanza di SQL Server.

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

> [!NOTE]
> Gli eventi di failover possono verificarsi durante un'esecuzione di query distribuita che accede ai dati da origini dati remote come HDFS o il pool di dati. Come procedura consigliata, le applicazioni devono essere progettate in modo da ottenere la logica di ripetizione dei tentativi di connessione in caso di disconnessione causata dal failover.  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>Connettersi ai database nelle repliche secondarie

Per le connessioni di sola lettura ai database nelle repliche secondarie, `sql-server-master-readonly` usare l'endpoint. Questo endpoint funge da servizio di bilanciamento del carico tra tutte le repliche secondarie. Specificare il contesto del database utente nella stringa di connessione.

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>Connettersi a un'istanza di SQL Server

Per alcune operazioni come l'impostazione delle configurazioni a livello di server o l'aggiunta manuale di un database al gruppo di disponibilità (nel caso in cui il database sia stato creato con un flusso di lavoro di ripristino), è necessaria una connessione all'istanza di. Per fornire questa connessione, esporre un endpoint esterno. Di seguito è riportato un esempio in cui viene illustrato come esporre l'endpoint e quindi aggiungere il database creato con un flusso di lavoro di ripristino al gruppo di disponibilità.

- Determinare il pod che ospita la replica primaria connettendosi all' `sql-server-master` endpoint ed eseguire:

    ```sql
    SELECT @@SERVERNAME
   ```

- Esporre l'endpoint esterno creando un nuovo servizio Kubernetes

    Per un cluster kubeadm eseguire il comando seguente. Sostituire `podName` con il nome del server restituito nel passaggio precedente, `serviceName` con il nome preferito per il servizio Kubernetes creato e `namespaceName`* con il nome del cluster di integrazione applicativa dei dati.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    Per un'esecuzione del cluster AKS, eseguire lo stesso comando, ad eccezione del fatto che il tipo di servizio `LoadBalancer`creato sarà. Esempio: 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    Di seguito è riportato un esempio di questo comando eseguito su AKS, in cui il pod che `master-0`ospita il database primario è:

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    Ottenere l'indirizzo IP del servizio Kubernetes creato:

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> Come procedura consigliata, è consigliabile eseguire la pulizia eliminando il servizio Kubernetes creato in precedenza eseguendo questo comando:
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- Aggiungere il database al gruppo di disponibilità.

    Per aggiungere il database al gruppo di disponibilità, è necessario eseguirlo in modalità di recupero con registrazione completa e deve essere eseguito un backup del log. Usare l'indirizzo IP del servizio Kubernetes creato in precedenza e connettersi all'istanza di SQL Server quindi eseguire le istruzioni TSQL come illustrato di seguito.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    Nell'esempio seguente viene aggiunto un database `sales` denominato ripristinato nell'istanza:

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>Limitazioni note

Questi sono i problemi noti e le limitazioni con i gruppi di disponibilità per SQL Server master nel cluster Big Data:

- I database creati come risultato di flussi di lavoro `CREATE DATABASE` diversi `RESTORE`da `CREATE DATABASE FROM SNAPSHOT` like, non vengono aggiunti automaticamente al gruppo di disponibilità. [Connettersi all'istanza](#instance-connect) di e aggiungere manualmente il database al gruppo di disponibilità.
- Alcune operazioni come l'esecuzione di impostazioni di `sp_configure` configurazione del server con richiedono una connessione all'istanza master. Non è possibile usare l'endpoint primario corrispondente. Seguire [le istruzioni](#instance-connect) per connettersi all'istanza di SQL Server ed eseguire `sp_configure`.
- La configurazione della disponibilità elevata deve essere creata quando si distribuisce l'integrazione applicativa dei dati. Non è possibile abilitare la configurazione della disponibilità elevata con i gruppi di disponibilità dopo la distribuzione.

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni sull'utilizzo dei file di configurazione nelle distribuzioni Big Data cluster, vedere [How [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] to deploy on Kubernetes](deployment-guidance.md#configfile).
- Per ulteriori informazioni sulla funzionalità gruppi di disponibilità per SQL Server, vedere [Panoramica di gruppi di disponibilità always on (SQL Server)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017).
