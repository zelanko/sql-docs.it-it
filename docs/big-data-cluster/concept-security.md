---
title: Concetti relativi alla sicurezza
titleSuffix: SQL Server big data clusters
description: Questo articolo presenta i concetti relativi alla sicurezza per i cluster Big Data di SQL Server 2019 (anteprima). È inclusa la descrizione degli endpoint del cluster e dell'autenticazione del cluster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54ae86785590eb26fb8ac402f3ae8ab6c7f29a98
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958662"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>Concetti relativi alla sicurezza per i cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un cluster Big Data sicuro implica un supporto costante e coerente per gli scenari di autenticazione e autorizzazione, sia in SQL Server sia in HDFS/Spark. L'autenticazione è il processo di verifica dell'identità di un utente o di un servizio per garantire che corrisponda a quella dichiarata dall'utente o dal servizio stesso. Per autorizzazione si intende la concessione o la negazione dell'accesso a risorse specifiche in base all'identità dell'utente richiedente. Questo passaggio viene eseguito dopo l'identificazione di un utente tramite l'autenticazione.

Nel contesto dei Big Data l'autorizzazione viene in genere eseguita tramite gli elenchi di controllo di accesso (ACL), che associano le identità utente ad autorizzazioni specifiche. HDFS supporta l'autorizzazione limitando l'accesso alle API del servizio, ai file HDFS e all'esecuzione del processo.

Questo articolo presenta i principali concetti relativi alla sicurezza nel cluster Big Data.

## <a name="cluster-endpoints"></a>Endpoint del cluster

Esistono tre punti di ingresso al cluster Big Data

* Gateway HDFS/Spark (Knox): endpoint basato su HTTPS. Gli altri endpoint vengono trasmessi tramite proxy attraverso questo. Il gateway HDFS/Spark viene usato per accedere a servizi come webHDFS e Livy. Ogni volta che vi sono riferimenti a Knox, si tratta dell'endpoint.

* Endpoint controller: servizio di gestione del cluster Big Data che espone API REST per la gestione del cluster. Tramite questo endpoint è anche possibile accedere ad alcuni strumenti.

* Istanza master: endpoint TDS per gli strumenti e le applicazioni di database per la connessione all'istanza master di SQL Server nel cluster.

![Endpoint del cluster](media/concept-security/cluster_endpoints.png)

Attualmente non è possibile aprire porte aggiuntive per accedere al cluster dall'esterno.

### <a name="how-endpoints-are-secured"></a>Protezione degli endpoint

La protezione degli endpoint nel cluster Big Data avviene tramite password che possono essere impostate/aggiornate usando variabili di ambiente o comandi dell'interfaccia della riga di comando. Tutte le password interne del cluster vengono archiviate come segreti Kubernetes.  

## <a name="authentication"></a>Autenticazione

Durante il provisioning del cluster, vengono creati diversi account di accesso.

Alcuni di questi account di accesso servono alla comunicazione dei servizi gli uni con gli altri, mentre altri sono destinati agli utenti finali per accedere al cluster.

### <a name="end-user-authentication"></a>Autenticazione dell'utente finale
Durante il provisioning del cluster, è necessario impostare diverse password per l'utente finale tramite variabili di ambiente. Queste password verranno usate dagli amministratori di SQL e del cluster per accedere ai servizi:

Nome utente del controller:
 + CONTROLLER_USERNAME=<nome_utente_controller>

Password del controller:  
 + CONTROLLER_USERNAME=<password_controller>

Password dell'amministratore di sistema dell'istanza master di SQL: 
 + MSSQL_SA_PASSWORD=<password_amministratore_sistema_controller>

Password per l'accesso all'endpoint HDFS/Spark:
 + KNOX_PASSWORD=<password_knox>

### <a name="intra-cluster-authentication"></a>Autenticazione all'interno del cluster

Durante il provisioning del cluster, vengono creati diversi account di accesso SQL:

* Nell'istanza SQL del controller viene creato un account di accesso SQL speciale gestito dal sistema, con il ruolo sysadmin. La password per questo account di accesso viene acquisita come segreto K8s.

* In tutte le istanze SQL nel cluster viene creato un account di accesso sysadmin, di proprietà del controller e gestito dal controller. Questo account è necessario al controller per eseguire attività amministrative, ad esempio l'installazione o l'aggiornamento di risorse a disponibilità elevata su queste istanze. Questi account di accesso vengono usati anche per la comunicazione all'interno del cluster tra istanze SQL, ad esempio l'istanza master di SQL Server che comunica con un pool di dati.

> [!NOTE]
> Nella versione corrente è supportata solo l'autenticazione di base. Il controllo di accesso con granularità fine per gli oggetti HDFS e per i pool di dati e di calcolo del cluster SQL Big Data non è ancora disponibile.

## <a name="intra-cluster-communication"></a>Comunicazione all'interno del cluster

La comunicazione con servizi non SQL all'interno del cluster Big Data, ad esempio da Livy a Spark o da Spark al pool di archiviazione, viene protetta tramite certificati. Tutta la comunicazione da SQL Server a SQL Server viene protetta tramite account di accesso SQL.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere le risorse seguenti:

- [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Architettura dei cluster Big Data di Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
