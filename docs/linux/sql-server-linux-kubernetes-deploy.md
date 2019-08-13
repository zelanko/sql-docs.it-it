---
title: Distribuire un gruppo di disponibilità Always On di SQL Server in un cluster Kubernetes
description: Questo articolo illustra i parametri per i requisiti globali per l'operatore del gruppo di disponibilità Always On di SQL Server in Kubernetes
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a4811c1f41c4c8b9a566dc13b3de713576b4980d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952622"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Distribuire un gruppo di disponibilità Always On di SQL Server in un cluster Kubernetes

L'esempio in questo articolo distribuisce un gruppo di disponibilità Always On di SQL Server in un cluster Kubernetes con tre repliche. Le repliche secondarie sono in modalità di commit sincrono.

In Kubernetes la distribuzione include un operatore di SQL Server, i contenitori di SQL Server e i servizi di bilanciamento del carico. L'operatore orchestra automaticamente il gruppo di disponibilità. Questo articolo spiega come:

- Distribuire l'operatore, i contenitori di SQL Server e i servizi di bilanciamento del carico.
- Connettersi al gruppo di disponibilità con i servizi.
- Aggiungere un database al gruppo di disponibilità.

## <a name="requirements"></a>Requisiti

- Un cluster Kubernetes nel servizio Azure Kubernetes con la versione più recente
- Almeno tre nodi
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Accedere al repository GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)

> [!NOTE]
> È possibile usare qualsiasi tipo di cluster Kubernetes. Per creare un cluster Kubernetes nel servizio Azure Kubernetes, vedere [Creare un cluster nel servizio Azure Kubernetes](https://docs.microsoft.com/azure/aks/create-cluster).
>
> Usare la versione più recente di Kubernetes. La versione specifica dipende dalla sottoscrizione e dall'area. Vedere [Versioni di Kubernetes supportate nel servizio Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions).  
>
> Lo script seguente crea un cluster Kubernetes a quattro nodi in Azure. Prima di eseguire lo script, sostituire `<latest version>` con la versione più recente disponibile. Ad esempio `1.12.5`.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>Distribuire l'operatore, i contenitori di SQL Server e i servizi di bilanciamento del carico

1. Creare uno [spazio dei nomi](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/).

      Questo esempio usa uno spazio dei nomi denominato `ag1`. Eseguire il comando seguente per creare lo spazio dei nomi.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      Tutti gli oggetti appartenenti a questa soluzione sono nello spazio dei nomi `ag1`.

1. Configurare e distribuire il manifesto dell'operatore di SQL Server.

      Copiare il file [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) di SQL Server da [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      Il file `operator.yaml` è il manifesto della distribuzione per l'operatore Kubernetes.
    
      Applicare il manifesto al cluster Kubernetes.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. Creare un segreto per Kubernetes con le password per l'account `sa` e la chiave master dell'istanza di SQL Server.

      Creare il segreto con `kubectl`.
      
      L'esempio seguente crea un segreto denominato `sql-secrets` nello spazio dei nomi `ag1`. Il segreto archivia due password:
      
      - `sapassword` archivia la password per l'account `sa` di SQL Server.
      - `masterkeypassword` archivia la password usata per creare la chiave master di SQL Server. 
    
   Copiare lo script nel terminale. Sostituire ogni `<>` con una password complessa ed eseguire lo script per creare il segreto.
    
   >[!NOTE]
   >La password non può usare i caratteri `&` o `` ` ``.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. Distribuire la risorsa di SQL Server personalizzata.

      Copiare il manifesto [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) di SQL Server da [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      >[!NOTE]
      >Il file `sqlserver.yaml` descrive i contenitori di SQL Server, le richieste di volumi persistenti, i volumi persistenti e i servizi di bilanciamento del carico necessari per ogni istanza di SQL Server.
    
      Applicare il manifesto al cluster Kubernetes.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
L'immagine seguente illustra la corretta applicazione di `kubectl apply` per questo esempio.

![Creare istanze di SQL Server](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

Dopo aver applicato il manifesto di SQL Server, l'operatore distribuisce i contenitori di SQL Server.

Kubernetes inserisce i contenitori nei pod. Usare `kubectl get pods --namespace ag1` per visualizzare lo stato dei pod. L'immagine seguente illustra la distribuzione di esempio dopo la distribuzione dei pod di SQL Server. 

![Pod compilati](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>Monitorare la distribuzione

È possibile usare il [dashboard di Kubernetes con il servizio Azure Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) per monitorare la distribuzione.

Usare `az aks browse` per avviare il dashboard. 

## <a name="connect-to-the-availability-group-with-the-services"></a>Connettersi al gruppo di disponibilità con i servizi

L'esempio [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) di [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) descrive i servizi di bilanciamento del carico che possono connettersi alle repliche del gruppo di disponibilità. 

- `ag1-primary` fornisce un endpoint per connettersi alla replica primaria.
- `ag1-secondary` fornisce un endpoint per connettersi a una replica secondaria.

Quando si applica il file manifesto, Kubernetes crea i servizi di bilanciamento del carico per ogni tipo di replica. Il servizio di bilanciamento del carico include un indirizzo IP. Usare questo indirizzo IP per connettersi al tipo di replica necessario.

Per distribuire i servizi, eseguire il comando seguente.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

Dopo aver distribuito i servizi, usare `kubectl get services --namespace ag1` per identificare l'indirizzo IP per i servizi.

Con l'indirizzo IP, è possibile connettersi all'istanza SQL Server che ospita ogni tipo di replica.

L'immagine seguente illustra:

- L'output di `kubectl get services` per lo spazio dei nomi `ag1`.

- I servizi di bilanciamento del carico creati per ogni contenitore di SQL Server. Usare questi indirizzi IP come endpoint per connettersi direttamente alle istanze di SQL Server nel cluster.

- La connessione `sqlcmd` alla replica primaria, con l'account `sa` tramite l'endpoint di bilanciamento del carico.

![Connessione](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>Aggiungere un database al gruppo di disponibilità

>[!NOTE]
>A questo punto, SQL Server Management Studio non può aggiungere un database a un gruppo di disponibilità. Usare Transact-SQL.

Dopo che Kubernetes ha creato i contenitori di SQL Server, completare i passaggi seguenti per aggiungere un database al gruppo di disponibilità.

1. [Connettersi](sql-server-linux-kubernetes-connect.md) a un'istanza di SQL Server nel cluster.

1. Creazione di un database.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. Eseguire un backup completo del database per avviare la catena di log.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. Aggiungere il database al gruppo di disponibilità.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
Il gruppo di disponibilità viene creato con il seeding automatico in modo che SQL Server crei automaticamente le repliche secondarie.

È possibile visualizzare lo stato del gruppo di disponibilità dal dashboard Gruppi di disponibilità di SQL Server Management Studio.

![dashboard](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>Passaggi successivi

- [Connettersi a un gruppo di disponibilità di SQL Server in un cluster Kubernetes](sql-server-linux-kubernetes-connect.md)

- [Gestire un gruppo di disponibilità di SQL Server in un cluster Kubernetes](sql-server-linux-kubernetes-manage.md)

- [SQL Server supporta i gruppi di disponibilità nei contenitori in un cluster Kubernetes](sql-server-ag-kubernetes.md)
