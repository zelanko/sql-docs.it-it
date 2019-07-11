---
title: Che cos'è il controller?
titleSuffix: SQL Server big data clusters
description: Questo articolo descrive il controller di un cluster di big data di SQL Server 2019 (anteprima).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 076cc40c09d4b086ae7a416ac1cc5ccbcc16a20a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729180"
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
- Gestire la sicurezza del cluster:
  - Verificare che gli endpoint cluster sicuro
  - Gestire utenti e ruoli
  - Configurare le credenziali per la comunicazione all'interno del cluster

## <a name="deploying-the-controller-service"></a>Distribuzione del servizio controller

Il controller è distribuito e ospitato nello spazio dei nomi Kubernetes stesso in cui il cliente vuole compilare un cluster di big data. Questo servizio viene installato da un amministratore di Kubernetes durante cluster bootstrap, utilizzando il **mssqlctl** utilità della riga di comando. Per altre informazioni, vedere [Introduzione ai cluster di SQL Server i big data](deploy-get-started.md).

Il flusso di lavoro di costruzione verrà layout su Kubernetes un cluster di big data completamente funzionale di SQL Server che include tutti i componenti descritti nel [Panoramica](big-data-cluster-overview.md) articolo. Il flusso di lavoro bootstrap crea innanzitutto il servizio controller, e ciò è sufficiente distribuire il servizio controller si coordina l'installazione e configurazione del resto della parte i servizi del pool di archiviazione, calcolo, dati e master.

## <a name="managing-the-cluster-through-the-controller-service"></a>La gestione del cluster tramite il servizio controller

È possibile gestire il cluster tramite il servizio di controller usando **mssqlctl** comandi. Se si distribuiscono oggetti aggiuntivi di Kubernetes, ad esempio i POD nello spazio dei nomi stesso, non sono gestiti o monitorati dal servizio controller. È anche possibile usare **kubectl** comandi per gestire il cluster a livello di Kubernetes. Per altre informazioni, vedere [monitoraggio e risoluzione dei problemi dei cluster di SQL Server i big data](cluster-troubleshooting-commands.md).

Il controller e gli oggetti Kubernetes (set di informazioni sullo stato, i POD, segreti e così via) creati per un cluster di big data si trovano in uno spazio dei nomi Kubernetes dedicato. Il servizio controller verrà concesse le autorizzazioni dall'amministratore del cluster Kubernetes per gestire tutte le risorse all'interno di tale spazio dei nomi.  I criteri RBAC per questo scenario viene configurato automaticamente come parte della distribuzione iniziale del cluster usando **mssqlctl**.

### <a name="mssqlctl"></a>mssqlctl

**mssqlctl** è un'utilità della riga di comando scritta in Python che consente di avviare e gestire i cluster di big data tramite le API REST esposta dal servizio controller gli amministratori del cluster.

## <a name="controller-service-security"></a>Sicurezza del servizio controller

Tutte le comunicazioni per il servizio controller viene effettuata tramite l'API REST su HTTPS. Un certificato autofirmato verrà automaticamente generato automaticamente in fase di bootstrap. 

L'autenticazione all'endpoint del servizio controller è basato su nome utente e password. Vengono effettuato il provisioning di queste credenziali in fase di bootstrap del cluster usando l'input per le variabili di ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.

> [!NOTE]
> È necessario fornire una password in conformità con [requisiti di complessità delle password di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere le risorse seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Workshop: Cluster di big data Microsoft SQL Server architettura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
