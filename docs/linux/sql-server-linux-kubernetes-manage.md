---
title: Gestire un SQL Server Always On gruppo di disponibilità Kubernetes
description: Questo articolo illustra come gestire un SQL Server gruppo di disponibilità AlwaysOn in Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad4f310ce6c0e200d5e658b3d5814131000d0004
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231111"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Gestire SQL Server Always On Kubernetes gruppo di disponibilità

Per gestire un gruppo di disponibilità AlwaysOn in Kubernetes, creare un manifesto e applicarlo al cluster. Il manifesto è un `.yaml` file.  

Gli esempi in questo articolo si applicano a tutti i cluster Kubernetes. Gli scenari in questi esempi vengono eseguiti in un cluster in Azure Kubernetes Service.

Vedere un esempio di distribuzione completa nel [distribuire un SQL Server gruppo di disponibilità AlwaysOn nel Kubernetes Cluster](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Eseguire il failover: gruppo di disponibilità SQL Server in Kubernetes

Per eseguire il failover o spostare una replica primaria in un altro nodo in un gruppo di disponibilità, completare i passaggi seguenti:

1. Definire un processo in un file manifesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -in di [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) repository github descrive un processo di failover.

  Copiare il file manifesto per l'amministrazione terminal.

  Aggiornare il file per l'ambiente.

  - Sostituire `<containerName>` con il nome del pod (ad esempio mssql2-0) della destinazione del gruppo di disponibilità previsto.
  - Se il gruppo di disponibilità non è nel `ag1` dello spazio dei nomi, sostituire `ag1` con lo spazio dei nomi.

  Questo file definisce un processo di failover denominato `manual-failover`.

1. Per distribuire il processo, usare `kubectl apply`. Lo script seguente consente di distribuire il processo.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Dopo il processo viene distribuito, kubernetes, con l'operatore di Server SQL, esegue le attività seguenti:
  
  - Abbassa di livello della replica primaria al database secondario
  
  - Alza di livello la replica primaria specificata
  
  Dopo l'applicazione, file manifesto Kubernetes esegue il processo. Il processo consente di selezionare un nuovo leader il supervisore e consente di spostare la replica primaria per l'istanza di SQL Server del leader.

1. Verificare che il completamento del processo.
  
  Dopo che Kubernetes esegue il processo, è possibile esaminare il log.
  
  L'esempio seguente restituisce lo stato del processo denominato `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. Eliminare il processo di failover manuale. 

  >[!IMPORTANT]
  >Prima di emettere un altro failover manuale, è necessario eliminare manualmente il processo.
  > 
  >È possibile visualizzare lo stato dell'oggetto processo in Kubernetes rimane dopo il completamento. È necessario eliminare manualmente i processi precedenti dopo avere stabilito il relativo stato. L'eliminazione del processo elimina anche i log di Kubernetes. Se non si elimina il processo, i processi futuri failover avrà esito negativo a meno che non si modifica il nome del processo e il selettore di pod. Per altre informazioni, vedere [- i processi eseguiti fino al completamento](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

  Il comando seguente elimina il processo.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>Ruotare le credenziali

Ruotare le credenziali per reimpostare la password per SQL Server `sa` account e il Server SQL [chiave master del servizio](../relational-databases/security/encryption/service-master-key.md). 

Per completare questa attività, si verrà creazione di nuovi segreti nel cluster Kubernetes e quindi creare un processo per ruotare le credenziali.

Prima di ruotare le credenziali, assicurarsi un nuovo master secret per la password e la chiave master.

Lo script seguente crea un segreto denominato `new-sql-secrets`. Prima di eseguire lo script, sostituire `<>` con password complesse per il `sapassword` e il `masterkeypassword`. Usare password diverse per ogni valore corrispondente.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Completare i passaggi seguenti per ogni istanza di SQL Server che è la chiave master o `sa` password.

1. Copia [ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) per l'amministrazione terminal.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) nel [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) repository di github è un esempio di un manifesto per il processo.

  Prima di applicare questo manifesto, aggiornare il manifesto per l'ambiente. Esaminare e modificare le impostazioni seguenti in base alle esigenze.

  - Verificare lo spazio dei nomi. Aggiornare se necessario. Nell'esempio seguente in un manifesto si applica a uno spazio dei nomi denominato `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Verificare il nome dell'istanza di SQL Server. Aggiornare se necessario. Nell'esempio seguente in una specifica del manifesto si applica a un'istanza di SQL Server denominata `mssql1`.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  Salvare il file manifesto aggiornato nella workstation.

1. Usare `kubectl` per distribuire il processo.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes Aggiorna la chiave master e `sa` password per un'istanza di SQL Server in un gruppo di disponibilità.

1. Verificare che il processo viene completato. Eseguire il comando seguente: Per verificare che il processo viene completato, eseguire 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Dopo che il processo ha esito positivo, la chiave master e `sa` password per un'istanza di SQL Server vengono aggiornati.


1. Prima di eseguire nuovamente il processo, eliminare il processo. Ogni nome del processo deve essere univoco.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Per impostare lo stesso `sa` password per tutte le istanze di SQL Server, ripetere i passaggi precedenti per ogni istanza di SQL Server.

## <a name="next-steps"></a>Passaggi successivi

[Accedere al dashboard di Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Gruppo di disponibilità SQL Server in cluster Kubernetes](sql-server-ag-kubernetes.md)
