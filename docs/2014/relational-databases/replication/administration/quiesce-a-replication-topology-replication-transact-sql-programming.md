---
title: Come mettere una topologia di replica in stato di inattività (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f12f0fb8ee3a6118e03799d17836573fb5c733df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061551"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>Come mettere una topologia di replica in stato di inattività (programmazione Transact-SQL della replica)
   Mettere in *stato di inattività* un sistema significa arrestare le attività sulle tabelle pubblicate in tutti i nodi e verificare che ogni nodo abbia ricevuto tutte le modifiche dagli altri nodi. In questo argomento è illustrato come mettere in stato di inattività una topologia di replica, operazione necessaria per diverse attività amministrative, e assicurarsi che un nodo abbia ricevuto tutte le modifiche dagli altri nodi.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>Per mettere in stato di inattività una topologia di replica transazionale con sottoscrizioni di sola lettura  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_posttracertoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql).  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql).  
  
4.  Assicurarsi che ciascun Sottoscrittore abbia ricevuto il token di traccia.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>Per mettere in stato di inattività una topologia di replica transazionale con sottoscrizioni aggiornabili  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione e in tutti i Sottoscrittori.  
  
2.  Se i Sottoscrittori utilizzano sottoscrizioni ad aggiornamento in coda:  
  
    1.  Se l'agente di lettura coda non viene eseguito in modalità continua, eseguire l'agente. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Per verificare che la coda sia vuota, eseguire [sp_replqueuemonitor](/sql/relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql) in ciascun Sottoscrittore.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_posttracertoken](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql).  
  
4.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql).  
  
5.  Assicurarsi che ciascun Sottoscrittore abbia ricevuto il token di traccia.  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>Per mettere in stato di inattività una topologia di replica transazionale peer-to-peer  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate in tutti i nodi.  
  
2.  Eseguire [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) in ciascun database di pubblicazione nella topologia.  
  
3.  Se l'agente di lettura log o l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. L'agente di lettura log deve essere avviato prima l'agente di distribuzione. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Eseguire [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) in ciascun database di pubblicazione nella topologia. Assicurarsi che il set di risultati contenga risposte da ciascuno degli altri nodi.  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>Per assicurarsi che un nodo peer-to-peer abbia ricevuto tutte le modifiche precedenti  
  
1.  Eseguire [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) nel nodo del database di pubblicazione in cui viene eseguita la verifica.  
  
2.  Se l'agente di lettura log o l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. L'agente di lettura log deve essere avviato prima l'agente di distribuzione. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Eseguire [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) nel nodo del database di pubblicazione in cui viene eseguita la verifica. Assicurarsi che il set di risultati contenga risposte da ciascuno degli altri nodi.  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>Per mettere in stato di inattività una topologia di replica di tipo merge  
  
1.  Arrestare l'attività in tutte le tabelle pubblicate nel server di pubblicazione e in tutti i Sottoscrittori.  
  
2.  Eseguire due volte l'agente di merge per ciascuna sottoscrizione: sincronizzare una volta tutte le sottoscrizioni, quindi sincronizzare ciascuna di esse una seconda volta. In questo modo si garantisce che tutte le modifiche vengano replicate in tutti i nodi. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Se si verificano conflitti durante la sincronizzazione, è possibile che le modifiche richieste per la risoluzione dei conflitti non vengano propagate in tutti i nodi dopo aver eseguito due volte l'agente di merge.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;la programmazione Transact-SQL della replica&#41;](administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Misurare la latenza e convalidare le connessioni per la replica transazionale](../monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
