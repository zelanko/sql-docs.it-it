---
title: Che cos'è la distribuzione di applicazioni?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive la distribuzione di applicazioni in un cluster SQL Server 2019 Big Data (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419411"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>Che cos'è la distribuzione di applicazioni in un cluster SQL Server 2019 Big Data?

La distribuzione dell'applicazione consente la distribuzione di applicazioni nel cluster Big Data fornendo interfacce per la creazione, la gestione e l'esecuzione di applicazioni. Le applicazioni distribuite nel cluster Big Data traggono vantaggio dalla potenza di calcolo del cluster e possono accedere ai dati disponibili nel cluster. Ciò aumenta la scalabilità e le prestazioni delle applicazioni, gestendo al tempo stesso le applicazioni in cui si trovano i dati.
Le sezioni seguenti descrivono l'architettura e le funzionalità della distribuzione di applicazioni.

## <a name="application-deployment-architecture"></a>Architettura di distribuzione delle applicazioni

La distribuzione dell'applicazione è costituita da un controller e da gestori di runtime dell'app. Quando si crea un'applicazione, viene fornito un`spec.yaml`file di specifica (). Questo `spec.yaml` file contiene tutte le informazioni necessarie per la distribuzione corretta dell'applicazione da parte del controller. Di seguito è riportato un esempio del contenuto per `spec.yaml`:

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

Il controller esamina l' `runtime` oggetto specificato `spec.yaml` nel file e chiama il gestore di runtime corrispondente. Il gestore di runtime crea l'applicazione. Viene innanzitutto creato un ReplicaSet Kubernetes contenente uno o più POD, ognuno dei quali contiene l'applicazione da distribuire. Il numero di Pod è definito dal `replicas` set di parametri `spec.yaml` nel file per l'applicazione. Ogni pod può avere uno o più pool. Il numero di pool è definito dal `poolsize` set di parametri `spec.yaml` nel file.

Queste impostazioni hanno un effetto sulla quantità di richieste che la distribuzione è in grado di gestire in parallelo. Il numero massimo di richieste in un determinato momento è uguale a `replicas` times. `poolsize` Se si dispone di 5 repliche e 2 pool per replica, la distribuzione può gestire 10 richieste in parallelo. Vedere l'immagine seguente per una rappresentazione grafica di `replicas` e `poolsize`:

![PoolSize e repliche](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Dopo la creazione di REPLICASET e l'avvio dei Pod, viene creato un processo cron se è stato `schedule` impostato un valore `spec.yaml` nel file. Infine, viene creato un servizio Kubernetes che può essere usato per gestire ed eseguire l'applicazione (vedere di seguito).

Quando viene eseguita un'applicazione, il servizio Kubernetes per l'applicazione inoltra le richieste a una replica e restituisce i risultati.

## <a name="how-to-work-with-application-deployment"></a>Come usare la distribuzione di applicazioni

Le due interfacce principali per la distribuzione di applicazioni sono: 
- [Interfaccia della riga di comando`azdata`](big-data-cluster-create-apps.md)
- [Estensione Visual Studio Code e Azure Data Studio](app-deployment-extension.md)

È anche possibile che un'applicazione venga eseguita usando un servizio Web RESTful. Per ulteriori informazioni, vedere [utilizzo di applicazioni in cluster Big Data](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su come creare ed eseguire applicazioni in cluster SQL Server Big Data, vedere gli argomenti seguenti:

- [Distribuire applicazioni con azdata](big-data-cluster-create-apps.md)
- [Distribuire applicazioni usando l'estensione per la distribuzione di app](app-deployment-extension.md)
- [Utilizzare le applicazioni in cluster Big Data](big-data-cluster-consume-apps.md)

Per ulteriori informazioni sui cluster SQL Server Big Data, vedere la panoramica seguente:

- [Che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md)
