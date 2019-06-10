---
title: Che cos'è la distribuzione di applicazioni?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive la distribuzione di applicazioni in un cluster di big data di SQL Server 2019 (anteprima).
author: jterh
ms.author: jroth
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a6ba9caed2b01abc50e16e34d1a13413af2d0ba
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801863"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>Che cos'è la distribuzione di applicazioni in un cluster di SQL Server 2019 dei big Data?

Distribuzione dell'applicazione consente la distribuzione di applicazioni nel cluster di big data, fornendo le interfacce per creare, gestire ed eseguire le applicazioni. Le applicazioni distribuite nel cluster di big data usufruire la potenza di calcolo del cluster e possono accedere ai dati che sono disponibili nel cluster. In questo modo si aumenta la scalabilità e prestazioni delle applicazioni, gestendo le applicazioni in cui si trovano i dati.
Le sezioni seguenti descrivono l'architettura e la funzionalità di distribuzione dell'applicazione.

## <a name="application-deployment-architecture"></a>Architettura di distribuzione applicazione

Distribuzione di applicazioni è costituito da un controller e i gestori di runtime delle app. Quando si crea un'applicazione, un file di specifica (`spec.yaml`) viene fornito. Ciò `spec.yaml` file contiene tutto ciò che il controller deve sapere per distribuire correttamente l'applicazione. Di seguito è riportato un esempio del contenuto per `spec.yaml`:

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

Controlla se il controller la `runtime` specificato nella `spec.yaml` file e chiama il gestore di runtime corrispondenti. Il gestore di runtime crea l'applicazione. Prima di tutto un Kubernetes ReplicaSet viene creata contenente uno o più POD, ognuno dei quali contiene l'applicazione da distribuire. Il numero di POD è definito per il `replicas` parametro impostato `spec.yaml` file per l'applicazione. Ogni pod può avere uno dei più pool. Il numero di pool è definito per il `poolsize` parametro set nel `spec.yaml` file.

Queste impostazioni hanno un impatto sulla quantità di richieste che può gestire la distribuzione in parallelo. Il numero massimo di richieste in un determinato momento è uguale a `replicas` volte `poolsize`. Se sono presenti 5 repliche e 2 pool per ogni replica la distribuzione può gestire 10 richieste in parallelo. Vedere l'immagine seguente per una rappresentazione grafica dei `replicas` e `poolsize`:

![DimensionePool e repliche](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Dopo aver ReplicaSet è stata creata e il numero di POD sono stati avviati, viene creato un processo cron se un `schedule` è stato impostato nel `spec.yaml` file. Infine, viene creato un Kubernetes Service che consente di gestire ed eseguire l'applicazione (vedere sotto).

Quando viene eseguita un'applicazione, il servizio di Kubernetes per i proxy di applicazione, le richieste a una replica e restituisce i risultati.

## <a name="how-to-work-with-application-deployment"></a>Come lavorare con la distribuzione di applicazioni

Le due interfacce principali per la distribuzione dell'applicazione sono: 
- [Interfaccia della riga di comando `mssqlctl`](big-data-cluster-create-apps.md)
- [Estensione di Visual Studio Code e Data Studio di Azure](app-deployment-extension.md)

È anche possibile che un'applicazione può essere eseguito tramite un servizio web RESTful. Per altre informazioni, vedere [utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come creare ed eseguire applicazioni nel cluster di big data di SQL Server, vedere gli argomenti seguenti:

- [Distribuire applicazioni con mssqlctl](big-data-cluster-create-apps.md)
- [Distribuire le applicazioni usando l'estensione per la distribuzione di App](app-deployment-extension.md)
- [Utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md)

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
