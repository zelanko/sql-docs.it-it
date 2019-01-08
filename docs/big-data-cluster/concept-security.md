---
title: Concetti relativi alla sicurezza
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive i concetti di sicurezza per il cluster di big data 2019 Server SQL (anteprima). Sono inclusi che descrive l'endpoint del cluster e l'autenticazione del cluster.
author: nelgson
ms.author: negust
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: d4da38df828b2859de07a7676fc5070bcecf6329
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030575"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>Concetti relativi alla sicurezza per i cluster di SQL Server i big Data

Un cluster sicuro dei big Data implica il supporto e coerente per gli scenari di autenticazione e autorizzazione, in SQL Server e HDFS/Spark. L'autenticazione è il processo di verifica dell'identità di un utente o un servizio e per garantire che siano chi si sono che afferma di essere. Autorizzazione fa riferimento alla concessione o negazione dell'accesso a risorse specifiche in base all'identità dell'utente richiedente. Questo passaggio viene eseguito dopo che un utente viene identificato tramite l'autenticazione.

Autorizzazione nel contesto di Big Data è in genere eseguite tramite elenchi di controllo di accesso (ACL), che associa le identità degli utenti con autorizzazioni specifiche. HDFS supporta l'autorizzazione, limitando l'accesso per le API del servizio, i file HDFS e l'esecuzione del processo.

Questo articolo illustra i concetti chiave correlati alla sicurezza del cluster di big data.

## <a name="cluster-endpoints"></a>Endpoint cluster

Esistono tre punti di ingresso per il cluster di big data

* Gateway di HDFS/Spark (Knox): si tratta di un endpoint basato su HTTPS. Altri endpoint vengono elaborati tramite questo. Gateway HDFS/Spark viene usato per accedere ai servizi, ad esempio webHDFS e Livy. Quando sono presenti riferimenti a Knox, si tratta dell'endpoint.

* Endpoint del controller - servizio di Gestione cluster di big data che espone le API REST per la gestione del cluster. Alcuni strumenti, ad esempio il portale di amministrazione, sono anche accessibili tramite questo endpoint.

* Istanza master - endpoint TDS per strumenti di database e applicazioni per connettersi all'istanza di SQL Server Master nel cluster.

![Endpoint cluster](media/concept-security/cluster_endpoints.png)

Attualmente, non è possibile aprire porte aggiuntive per l'accesso al cluster dall'esterno.

### <a name="how-endpoints-are-secured"></a>Modo in cui gli endpoint sono protetti

Protezione degli endpoint del cluster di big data viene eseguita tramite password che possono essere set/aggiornato uno usando le variabili di ambiente o i comandi dell'interfaccia della riga. Tutte le password interno del cluster vengono archiviate come segreti Kubernetes.  

## <a name="authentication"></a>Autenticazione

Durante il provisioning del cluster, viene creato un numero di account di accesso.

Alcuni di questi account di accesso sono per i servizi comunicare tra loro e altri sono per gli utenti finali accedere al cluster.

### <a name="end-user-authentication"></a>Autenticazione dell'utente finale
Durante il provisioning del cluster, un numero di password dell'utente finale deve essere impostato utilizzando le variabili di ambiente. Queste sono le password che agli amministratori SQL e gli amministratori di cluster usano per accedere ai servizi:

Nome utente di controller:
 + CONTROLLER_USERNAME = < controller_username >

Password del controller:  
 + CONTROLLER_PASSWORD = < controller_password >

Password dell'account SA di SQL Master: 
 + MSSQL_SA_PASSWORD = < controller_sa_password >

Password per l'accesso all'endpoint HDFS/Spark:
 + KNOX_PASSWORD = < knox_password >

### <a name="intra-cluster-authentication"></a>Autenticazione all'interno del cluster

Durante la distribuzione del cluster viene creato un numero di account di accesso SQL:

* Un account di accesso SQL speciale viene creato nell'istanza di SQL Controller che è gestito, con ruolo sysadmin dal sistema. La password per questo account di accesso viene acquisita come segreto K8s.

* Viene creato un account di accesso sysadmin in tutte le istanze SQL nel cluster, che possiede e gestisce di Controller. È necessario per eseguire attività amministrative, ad esempio per il programma di installazione a disponibilità elevata, su queste istanze del Controller. Questi account di accesso usati anche per la comunicazione all'interno del cluster tra istanze SQL, ad esempio istanza master di SQL che comunicano con un pool di dati.

> [!NOTE]
> Nella versione corrente, è supportata solo l'autenticazione di base. Controllo degli accessi con granularità fine a oggetti HDFS e SQL dei big data cluster calcolo e i dati nei pool, non è ancora disponibile.

## <a name="intra-cluster-communication"></a>Comunicazioni all'interno del cluster

Comunicazioni con i servizi non-SQL all'interno del cluster di big data, ad esempio Livy Spark o Spark per il pool di archiviazione, sono protette tramite certificati. Tutti i Server SQL per la comunicazione tra SQL Server viene protetto usando l'account di accesso SQL.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere gli articoli seguenti:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
- [Guida introduttiva: Distribuire cluster di big data di SQL Server in Kubernetes](quickstart-big-data-cluster-deploy.md)
