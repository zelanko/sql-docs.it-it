---
title: Gestire un gruppo di disponibilità Always On di SQL Server in Kubernetes
description: Questo articolo illustra come gestire un gruppo di disponibilità Always On di SQL Server in Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952546"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Gestire un gruppo di disponibilità Always On di SQL Server in Kubernetes

Per gestire un gruppo di disponibilità Always On in Kubernetes, creare un manifesto e applicarlo al cluster. Il manifesto è un file `.yaml`.  

Gli esempi in questo articolo si applicano a tutti i cluster Kubernetes. Gli scenari in questi esempi vengono applicati a un cluster nel servizio Azure Kubernetes.

Per un esempio della distribuzione completa, vedere [Distribuire un gruppo di disponibilità Always On di SQL Server in un cluster Kubernetes](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Failover - Gruppo di disponibilità SQL Server in Kubernetes

Per effettuare il failover di una replica primaria o per spostarla in un nodo diverso in un gruppo di disponibilità, completare i passaggi seguenti:

1. Definire un processo in un file manifesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml): nel repository GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) descrive un processo di failover.

  Copiare il file manifesto nel terminale di amministrazione.

  Aggiornare il file per il proprio ambiente.

  - Sostituire `<containerName>` con il nome del pod (ad esempio, mssql2-0) della destinazione del gruppo di disponibilità prevista.
  - Se il gruppo di disponibilità non è nello spazio dei nomi `ag1`, sostituire `ag1` con lo spazio dei nomi.

  Questo file definisce un processo di failover denominato `manual-failover`.

1. Per distribuire il processo, usare `kubectl apply`. Lo script seguente distribuisce il processo.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Dopo la distribuzione del processo, Kubernetes, con l'operatore di SQL Server, esegue le attività seguenti:
  
  - Abbassa di livello la replica primaria impostandola come secondaria
  
  - Alza di livello la replica specificata impostandola come primaria
  
  Dopo aver applicato il file manifesto, Kubernetes esegue il processo. Il processo fa in modo che il supervisore selezioni un nuovo leader e sposta la replica primaria all'istanza SQL Server del leader.

1. Verificare che il processo sia stato completato.
  
  Dopo che Kubernetes ha eseguito il processo, è possibile esaminare il log.
  
  In questo esempio viene restituito lo stato del processo `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. Eliminare il processo di failover manuale. 

  >[!IMPORTANT]
  >È necessario eliminare il processo manualmente prima di eseguire un altro failover manuale.
  > 
  >L'oggetto processo in Kubernetes rimane presente anche dopo il completamento, in modo che sia possibile visualizzarne lo stato. È necessario eliminare manualmente i processi precedenti dopo aver preso nota dello stato. Eliminando il processo vengono eliminati anche i log di Kubernetes. Se non si elimina il processo, i processi di failover futuri avranno esito negativo a meno che non si modifichino il nome del processo e il selettore di pod. Per altre informazioni, vedere [Jobs - Run to Completion](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) (Processi: esecuzione fino al completamento).

  Il comando seguente elimina il processo.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>Ruotare le credenziali

Ruotare le credenziali per reimpostare la password per l'account `sa` di SQL Server e la [chiave master del servizio](../relational-databases/security/encryption/service-master-key.md) SQL Server. 

Per completare questa attività, si creeranno nuovi segreti nel cluster Kubernetes e quindi si creerà un processo per ruotare le credenziali.

Prima di ruotare le credenziali, creare un nuovo segreto per la password e la chiave master.

Lo script seguente crea un segreto denominato `new-sql-secrets`. Prima di eseguire lo script, sostituire `<>` con password complesse per `sapassword` e `masterkeypassword`. Usare password diverse per ogni rispettivo valore.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Completare i passaggi seguenti per ogni istanza di SQL Server per cui è necessaria la chiave master o la password `sa`.

1. Copiare [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) nel terminale di amministrazione.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) nel repository GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) è un esempio di un manifesto per questo processo.

  Prima di applicare questo manifesto, aggiornare il manifesto per l'ambiente. Esaminare e modificare le impostazioni seguenti, in base alla necessità.

  - Verificare lo spazio dei nomi. Aggiornarlo se necessario. L'esempio seguente in un manifesto si applica a uno spazio dei nomi denominato `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Verificare il nome dell'istanza di SQL Server. Aggiornarlo se necessario. L'esempio seguente nella specifica di un manifesto si applica a un'istanza di SQL Server denominata `mssql1`.

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

  Kubernetes aggiorna la chiave master e la password `sa` per un'istanza di SQL Server in un gruppo di disponibilità.

1. Verificare che il processo sia stato completato. Eseguire il comando seguente: Per verificare che il processo sia stato completato, eseguire 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Dopo il completamento del processo, la chiave master e la password `sa` per un'istanza di SQL Server vengono aggiornate.


1. Prima di eseguire di nuovo il processo, eliminarlo. Ogni processo deve essere univoco.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Per impostare la stessa password `sa` per tutte le istanze di SQL Server, ripetere i passaggi precedenti per ogni istanza di SQL Server.

## <a name="next-steps"></a>Passaggi successivi

[Accedere al dashboard di Kubernetes con il servizio Azure Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Gruppo di disponibilità di SQL Server nel cluster Kubernetes](sql-server-ag-kubernetes.md)
