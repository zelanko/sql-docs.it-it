---
title: Distribuire un contenitore di SQL Server in Kubernetes con servizi Kubernetes di Azure (AKS)
description: Questa esercitazione illustra come distribuire una soluzione a disponibilità elevata SQL Server con Kubernetes in Azure Kubernetes Service.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: mvc
ms.technology: linux
ms.openlocfilehash: 2ae299553c700de7f22976917fa8556f93dbe61b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032048"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Distribuire un contenitore di SQL Server in Kubernetes con servizi Kubernetes di Azure (AKS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Informazioni su come configurare un'istanza di SQL Server su Kubernetes in Azure Kubernetes Service (AKS), con un archivio permanente per disponibilità elevata (HA). La soluzione offre la resilienza. Se l'istanza di SQL Server non riesce, Kubernetes nuovamente viene creata automaticamente in un nuovo pod. Kubernetes offre anche la resilienza rispetto a un errore del nodo.

Questa esercitazione illustra come configurare un'istanza di SQL Server a disponibilità elevata in un contenitore nel servizio contenitore di AZURE. È anche possibile creare [i gruppi di disponibilità per i contenitori di SQL Server](sql-server-ag-kubernetes.md). Per confrontare le due diverse soluzioni di Kubernetes, vedere [disponibilità elevata per i contenitori di SQL Server](sql-server-linux-container-ha-overview.md).

> [!div class="checklist"]
> * Creare una password SA
> * Creare spazio di archiviazione
> * Creare la distribuzione
> * Connettersi con SQL Server Management Studio (SSMS)
> * Verificare l'errore e il ripristino

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Soluzione a disponibilità elevata su Kubernetes in esecuzione in Azure Kubernetes Service

Include il supporto per Kubernetes 1.6 e versioni successive [classi di archiviazione](https://kubernetes.io/docs/concepts/storage/storage-classes/), [attestazioni di volume permanente](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)e il [tipo di volume di disco di Azure](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). È possibile creare e gestire le istanze di SQL Server in modo nativo in Kubernetes. L'esempio in questo articolo illustra come creare un [distribuzione](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) per ottenere una configurazione a disponibilità elevata simile a un'istanza cluster di failover nel disco condiviso. In questa configurazione, Kubernetes svolgerà il ruolo dell'agente di orchestrazione del cluster. Quando un'istanza di SQL Server in un contenitore ha esito negativo, l'agente di orchestrazione avvia un'altra istanza del contenitore che collega alla stessa risorsa di archiviazione permanente.

![Diagramma del cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

Nel diagramma precedente `mssql-server` è un contenitore in un [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Kubernetes Orchestra le risorse del cluster. Oggetto [set di repliche](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) assicura che il pod viene recuperato automaticamente dopo un errore di nodo. Applicazioni di connettono al servizio. In questo caso, il servizio rappresenta un servizio di bilanciamento del carico che ospita un indirizzo IP che rimane invariata dopo l'errore del `mssql-server`.

Nel diagramma seguente, il `mssql-server` contenitore non è riuscita. Come l'agente di orchestrazione Kubernetes garantisce il conteggio corretto delle istanze integre nella replica di impostarla e avvia un nuovo contenitore in base alla configurazione. L'agente di orchestrazione avvia un nuovo pod nello stesso nodo, e `mssql-server` si riconnette alla stessa risorsa di archiviazione permanente. Il servizio si connette a creati nuovamente `mssql-server`.

![Diagramma del cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

Nel diagramma seguente, il nodo che ospita il `mssql-server` contenitore non è riuscita. L'agente di orchestrazione avvia nuovi pod in un nodo diverso, e `mssql-server` si riconnette alla stessa risorsa di archiviazione permanente. Il servizio si connette a creati nuovamente `mssql-server`.

![Diagramma del cluster Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Prerequisiti

* **Cluster Kubernetes**
   - L'esercitazione è necessario un cluster Kubernetes. Usa la procedura [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) per gestire il cluster. 

   - Visualizzare [distribuire un cluster del servizio contenitore di Azure (AKS)](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster) per creare e connettersi a un cluster Kubernetes a nodo singolo nel servizio contenitore di AZURE con `kubectl`. 

   >[!NOTE]
   >Per proteggersi da errori di nodo, un cluster Kubernetes richiede più di un nodo.

* **Azure CLI 2.0.23**
   - Le istruzioni riportate in questa esercitazione sono state convalidate rispetto 2.0.23 CLI di Azure.

## <a name="create-an-sa-password"></a>Creare una password SA

Creare una password SA nel cluster Kubernetes. Kubernetes è possibile gestire le informazioni di configurazione sensibili, come le password come [segreti](https://kubernetes.io/docs/concepts/configuration/secret/).

Il comando seguente crea una password per l'account SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Sostituire `MyC0m9l&xP@ssw0rd` con una password complessa.

   Per creare un segreto Kubernetes denominato `mssql` che contiene il valore `MyC0m9l&xP@ssw0rd` per il `SA_PASSWORD`, eseguire il comando.


## <a name="create-storage"></a>Creare spazio di archiviazione

Configurare un [volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) e [attestazione di volume permanente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) nel cluster Kubernetes. Completare questi passaggi: 

1. Creare un manifesto per definire la classe di archiviazione e del volume permanente attestazione.  Il manifesto specifica di strumento di provisioning di archiviazione, parametri, e [occupata da criteri](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). Il cluster Kubernetes Usa questo manifesto per creare l'archivio permanente. 

   Nell'esempio seguente yaml definisce una classe di archiviazione e attestazione di volume permanente. È di strumento di provisioning di classe di archiviazione `azure-disk`, perché si trova il cluster Kubernetes in Azure. Il tipo di account di archiviazione è `Standard_LRS`. L'attestazione di volume permanente è denominato `mssql-data`. I metadati di attestazione di volume permanente includeranno un'annotazione la connessione eseguire il backup per la classe di archiviazione. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   Salvare il file (ad esempio, **pvc.yaml**).

1. Creare l'attestazione di volume permanente Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` è la posizione in cui è stato salvato il file.

   Il volume permanente viene automaticamente creato come account di archiviazione di Azure e associato per l'attestazione di volume permanente. 

    ![Schermata del comando di attestazione di volume permanente](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Verificare l'attestazione di volume permanente.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` è il nome dell'attestazione di volume permanente.

   Nel passaggio precedente, l'attestazione di volume permanente è denominato `mssql-data`. Per visualizzare i metadati relativi l'attestazione di volume permanente, eseguire il comando seguente:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   I metadati restituiti includeranno un valore denominato `Volume`. Questo valore viene eseguito il mapping al nome del blob.

   ![Screenshot dei metadati restituiti, tra cui Volume](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   Il valore per il volume corrisponde alla parte del nome del blob nell'immagine seguente dal portale di Azure: 

   ![Nome del blob del portale screenshot di Azure](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Verificare il volume permanente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` Restituisce i metadati relativi a volume permanente che è stato automaticamente creato e associato per l'attestazione di volume permanente. 

## <a name="create-the-deployment"></a>Creare la distribuzione

In questo esempio, il contenitore che ospita l'istanza di SQL Server viene descritto come un oggetto di distribuzione di Kubernetes. La distribuzione crea un set di repliche. Il set di repliche consente di creare il pod. 

In questo passaggio, creare un manifesto per descrivere il contenitore basato su SQL Server [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) immagine Docker. I riferimenti al manifesto le `mssql-server` attestazione di volume permanente e il `mssql` segreto che sono già state applicate al cluster Kubernetes. Il manifesto descrive anche un [servizio](https://kubernetes.io/docs/concepts/services-networking/service/). Questo servizio è un servizio di bilanciamento del carico. Il servizio di bilanciamento del carico garantisce che l'indirizzo IP viene mantenuta dopo che viene recuperato l'istanza di SQL Server. 

1. Creare un manifesto (con estensione YAML) per descrivere la distribuzione. L'esempio seguente illustra una distribuzione, tra cui un contenitore in base l'immagine del contenitore SQL Server.

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   Copiare il codice precedente in un nuovo file denominato `sqldeployment.yaml`. Aggiornare i valori seguenti: 

   * MSSQL_PID `value: "Developer"`: Imposta il contenitore per l'esecuzione di SQL Server Developer edition. Edizione per sviluppatori non ha la licenza per i dati di produzione. Se la distribuzione di produzione, impostare l'edizione appropriata (`Enterprise`, `Standard`, o `Express`). 

      >[!NOTE]
      >Per altre informazioni, vedere [licenza di SQL Server come](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: È necessario che una voce per `claimName:` che esegue il mapping al nome usato per l'attestazione di volume permanente. Questa esercitazione Usa `mssql-data`. 

   * `name: SA_PASSWORD`: Configura l'immagine del contenitore per impostare la password dell'amministratore di sistema, come definito in questa sezione.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Quando Kubernetes consente di distribuire il contenitore, fa riferimento al segreto denominato `mssql` per ottenere il valore della password. 

   >[!NOTE]
   >Tramite il `LoadBalancer` tipo di servizio, l'istanza di SQL Server sia accessibile in remoto (tramite internet) sulla porta 1433.

   Salvare il file (ad esempio, **sqldeployment.yaml**).

1. Creare la distribuzione.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` è la posizione in cui è stato salvato il file.

   ![Schermata del comando di distribuzione](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   La distribuzione e il servizio vengono creati. L'istanza di SQL Server è in un contenitore, connesso a un archivio permanente.

   Per visualizzare lo stato del pod, digitare `kubectl get pod`.

   ![Schermata del comando pod get](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   Nell'immagine precedente, il pod con stato `Running`. Questo stato indica che il contenitore è pronto. L'operazione potrebbe richiedere alcuni minuti.

   >[!NOTE]
   >Dopo aver creata la distribuzione, può richiedere alcuni minuti prima che il pod è visibile. Il ritardo nel cluster effettua il pull, infatti, il [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) immagine dall'hub Docker. Dopo che l'immagine verrà inserita la prima volta, le distribuzioni successive potrebbero essere più veloce se la distribuzione è destinata a un nodo che dispone già dell'immagine memorizzati nella cache su di esso. 

1. Verificare che i servizi sono in esecuzione. Eseguire il comando seguente:

   ```azurecli
   kubectl get services 
   ```

   Questo comando restituisce i servizi in esecuzione, nonché gli indirizzi IP interni ed esterni per i servizi. Prendere nota dell'indirizzo IP esterno per il `mssql-deployment` servizio. Usare questo indirizzo IP per connettersi a SQL Server. 

   ![Schermata del comando del servizio get](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Per altre informazioni sullo stato degli oggetti nel cluster Kubernetes, eseguire:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Connettersi all'istanza di SQL Server

Se il contenitore è stato configurato come descritto, è possibile connettersi a un'applicazione dall'esterno della rete virtuale di Azure. Usare il `sa` account e l'indirizzo IP esterno di indirizzi per il servizio. Usare la password che è stato configurato come il segreto Kubernetes. 

È possibile utilizzare le seguenti applicazioni per connettersi all'istanza di SQL Server. 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   Per connettersi con `sqlcmd`, eseguire il comando seguente:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Sostituire i valori seguenti:
      
    - `<External IP Address>` con l'indirizzo IP per il `mssql-deployment` servizio 
    - `MyC0m9l&xP@ssw0rd` con la password

## <a name="verify-failure-and-recovery"></a>Verificare l'errore e il ripristino

Per verificare un errore e il ripristino, è possibile eliminare il pod. Eseguire i passaggi seguenti:

1. Elencare i pod in esecuzione SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Prendere nota del nome del pod che eseguono SQL Server.

1. Eliminare il pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` il valore viene restituito nel passaggio precedente per nome del pod. 

Kubernetes ricrea automaticamente i pod per ripristinare un'istanza di SQL Server e connettersi all'archiviazione persistente. Usare `kubectl get pods` per verificare che venga distribuito un pod nuovo. Usare `kubectl get services` per verificare che l'indirizzo IP per il nuovo contenitore è lo stesso. 

## <a name="summary"></a>Riepilogo

In questa esercitazione è stato descritto come distribuire i contenitori di SQL Server in un cluster Kubernetes per la disponibilità elevata. 

> [!div class="checklist"]
> * Creare una password SA
> * Creare spazio di archiviazione
> * Creare la distribuzione
> * Connettersi con SQL Server Management Studio (SSMS)
> * Verificare l'errore e il ripristino

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
>[Introduzione a Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)


