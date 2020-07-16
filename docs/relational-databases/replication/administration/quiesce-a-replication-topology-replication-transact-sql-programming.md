---
title: Disattivare una topologia di replica (SP di replica)
description: Informazioni su come usare le stored procedure di replica per disattivare una topologia di replica per SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1db75568779b7675a072467678e6be4004ec2698
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158879"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>Come mettere una topologia di replica in stato di inattività (programmazione Transact-SQL della replica)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  Mettere in*stato di inattività* un sistema significa arrestare le attività sulle tabelle pubblicate in tutti i nodi e verificare che ogni nodo abbia ricevuto tutte le modifiche dagli altri nodi. In questo argomento è illustrato come mettere in stato di inattività una topologia di replica, operazione necessaria per diverse attività amministrative, e assicurarsi che un nodo abbia ricevuto tutte le modifiche dagli altri nodi.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>Per mettere in stato di inattività una topologia di replica transazionale con sottoscrizioni di sola lettura  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_posttracertoken &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
4.  Assicurarsi che ciascun Sottoscrittore abbia ricevuto il token di traccia.  

### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>Per mettere in stato di inattività una topologia di replica transazionale con sottoscrizioni aggiornabili  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione e in tutti i Sottoscrittori.  
  
2.  Se i Sottoscrittori utilizzano sottoscrizioni ad aggiornamento in coda:  
  
    1.  Se l'agente di lettura coda non viene eseguito in modalità continua, eseguire l'agente. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Per verificare che la coda sia vuota, eseguire [sp_replqueuemonitor](../../../relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql.md) in ciascun Sottoscrittore.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_posttracertoken](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
4.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
5.  Assicurarsi che ciascun Sottoscrittore abbia ricevuto il token di traccia.  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>Per mettere in stato di inattività una topologia di replica transazionale peer-to-peer  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate in tutti i nodi.  
  
2.  Eseguire [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) in ciascun database di pubblicazione nella topologia.  
  
3.  Se l'agente di lettura log o l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. L'agente di lettura log deve essere avviato prima l'agente di distribuzione. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Eseguire [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) in ciascun database di pubblicazione nella topologia. Assicurarsi che il set di risultati contenga risposte da ciascuno degli altri nodi.  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>Per assicurarsi che un nodo peer-to-peer abbia ricevuto tutte le modifiche precedenti  
  
1.  Eseguire [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) nel nodo del database di pubblicazione in cui viene eseguita la verifica.  
  
2.  Se l'agente di lettura log o l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. L'agente di lettura log deve essere avviato prima l'agente di distribuzione. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Eseguire [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) nel nodo del database di pubblicazione in cui viene eseguita la verifica. Assicurarsi che il set di risultati contenga risposte da ciascuno degli altri nodi.  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>Per mettere in stato di inattività una topologia di replica di tipo merge  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione e in tutti i Sottoscrittori.  
  
2.  Eseguire due volte l'agente di merge per ciascuna sottoscrizione: sincronizzare una volta tutte le sottoscrizioni, quindi sincronizzare ciascuna di esse una seconda volta. In questo modo si garantisce che tutte le modifiche vengano replicate in tutti i nodi. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Se si verificano conflitti durante la sincronizzazione, è possibile che le modifiche richieste per la risoluzione dei conflitti non vengano propagate in tutti i nodi dopo aver eseguito due volte l'agente di merge.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;programmazione Transact-SQL della replica&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
