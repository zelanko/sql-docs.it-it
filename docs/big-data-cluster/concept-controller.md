---
title: Che cos'è il controller?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il controller di un cluster di big data di SQL Server 2019 (anteprima).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 4dba3e620ae3e6cd9aa6c09eb6196ac37acd77a7
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583404"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>Che cos'è il controller in un cluster di big data di SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Il controller ospita la logica di base per distribuire e gestire un cluster di big data. Si occupa di tutte le interazioni con Kubernetes, le istanze di SQL Server che fanno parte del cluster e altri componenti come HDFS e Spark. 

Il servizio controller fornisce le funzionalità di base seguenti:

- Gestione del ciclo di vita del cluster: bootstrap del cluster & eliminazione, aggiornare le configurazioni
- Gestire le istanze di SQL Server master
- Gestire i pool di calcolo, dati e archiviazione
- Esporre gli strumenti di monitoraggio per osservare lo stato del cluster
- Esporre gli strumenti di risoluzione dei problemi per rilevare e correggere problemi imprevisti
- Gestire la sicurezza del cluster: verificare che gli endpoint cluster protetto, gestire utenti e ruoli, configurare le credenziali per la comunicazione all'interno del cluster
- Gestire il flusso di lavoro degli aggiornamenti in modo che vengono implementate in modo sicuro (non disponibile nella versione CTP 2.4)
- Gestire la disponibilità elevata e ripristino di emergenza per i servizi con stato nel cluster (non disponibile nella versione CTP 2.4)

## <a name="deploying-the-controller-service"></a>Distribuzione del servizio controller

Il controller è distribuito e ospitato nello spazio dei nomi Kubernetes stesso in cui il cliente vuole compilare un cluster di big data. Questo servizio viene installato da un amministratore di Kubernetes durante il bootstrap del cluster, tramite l'utilità della riga di comando mssqlctl:

```bash
mssqlctl cluster create --name <name of your cluster>
```

Il flusso di lavoro di costruzione verrà layout su Kubernetes un cluster di big data completamente funzionale di SQL Server che include tutti i componenti descritti nel [Panoramica](big-data-cluster-overview.md) articolo. Il flusso di lavoro bootstrap crea innanzitutto il servizio controller, e ciò è sufficiente distribuire il servizio controller si coordina l'installazione e configurazione del resto della parte i servizi del pool di archiviazione, calcolo, dati e master.

## <a name="managing-the-cluster-through-the-controller-service"></a>La gestione del cluster tramite il servizio controller

È possibile gestire il cluster esclusivamente tramite il servizio di controller usando `mssqlctl` API o il portale di amministrazione cluster ospitato all'interno del cluster. Se si distribuiscono oggetti aggiuntivi di Kubernetes, ad esempio i POD nello spazio dei nomi stesso, non sono gestiti o monitorati dal servizio controller.

Il controller e gli oggetti Kubernetes (set di informazioni sullo stato, i POD, segreti e così via) creati per un cluster di big data si trovano in uno spazio dei nomi Kubernetes dedicato. Il servizio controller verrà concesse le autorizzazioni dall'amministratore del cluster Kubernetes per gestire tutte le risorse all'interno di tale spazio dei nomi.  I criteri RBAC per questo scenario viene configurato automaticamente come parte della distribuzione iniziale del cluster usando `mssqlctl`. 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` è un'utilità della riga di comando scritta in Python che consente agli amministratori di cluster da avviare e gestire i cluster di big data tramite le API REST esposta dal servizio controller.

### <a name="cluster-administration-portal"></a>Portale di amministrazione del cluster

Quando il servizio controller è attivo e in esecuzione, l'amministratore del cluster possa usare la [portale di amministrazione Cluster](cluster-admin-portal.md) per monitorare l'avanzamento della distribuzione, rilevare e risolvere i problemi con i servizi all'interno del cluster.

## <a name="controller-service-security"></a>Sicurezza del servizio controller

Tutte le comunicazioni per il servizio controller viene effettuata tramite l'API REST su HTTPS. Un certificato autofirmato verrà automaticamente generato automaticamente in fase di bootstrap. 

L'autenticazione all'endpoint del servizio controller è basato su nome utente e password. Vengono effettuato il provisioning di queste credenziali in fase di bootstrap del cluster usando l'input per le variabili di ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.

> [!NOTE]
> È necessario fornire una password in conformità con [requisiti di complessità delle password di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere le risorse seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
