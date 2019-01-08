---
title: Panoramica degli agenti di replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41775a529d34aa5ca457f92c9d26e327b74705ea
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811863"
---
# <a name="replication-agents-overview"></a>Panoramica degli agenti di replica
  La replica utilizza alcuni programmi autonomi, denominati agenti, per eseguire le attività associate al rilevamento delle modifiche e alla distribuzione dei dati. Per impostazione predefinita, gli agenti di replica vengono eseguiti come processi pianificati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e, a tale scopo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent deve essere in funzione. Gli agenti di replica possono inoltre essere eseguiti dalla riga di comando e dalle applicazioni che utilizzano gli oggetti RMO (Replication Management Objects) e possono essere amministrati con Monitoraggio replica per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
## <a name="sql-server-agent"></a>SQL Server Agent  
 In[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent vengono inclusi e pianificati gli agenti utilizzati nella replica e viene offerto un modo semplice per eseguire gli agenti di replica. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent consente inoltre di controllare e monitorare le operazioni all'esterno della replica. Per altre informazioni, vedere [Configure SQL Server Agent](../../../ssms/agent/sql-server-agent.md).  
  
> [!IMPORTANT]  
>  Per impostazione predefinita, il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è disabilitato durante l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a meno che non si scelga in modo esplicito di avviarlo automaticamente durante l'installazione. Per altre informazioni sull'avvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, vedere [Start, Stop, or Pause the SQL Server Agent Service](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
## <a name="snapshot-agent"></a>agente snapshot  
 L'agente snapshot viene in genere utilizzato con tutti i tipi di replica. Questo agente prepara schemi e file dei dati iniziali di tabelle pubblicate e di altri oggetti, archivia i file di snapshot e registra le informazioni sulla sincronizzazione nel database di distribuzione. L'agente snapshot viene eseguito nel server di distribuzione. Per altre informazioni, vedere [Replication Snapshot Agent](replication-snapshot-agent.md).  
  
## <a name="log-reader-agent"></a>Agente di lettura log  
 L'agente di lettura dei log viene utilizzato nella replica transazionale. Questo agente sposta le transazioni contrassegnate per la replica dal log delle transazioni nel server di pubblicazione al database di distribuzione. A ogni database pubblicato tramite la replica transazionale è associato un agente di lettura log specifico eseguito nel server di distribuzione e connesso al server di pubblicazione. Il server di distribuzione e il server di pubblicazione possono coesistere nello stesso computer. Per altre informazioni, vedere [Replication Log Reader Agent](replication-log-reader-agent.md).  
  
## <a name="distribution-agent"></a>Agente di distribuzione  
 L'agente di distribuzione viene utilizzato nella replica snapshot e nella replica transazionale. Questo agente applica lo snapshot iniziale al Sottoscrittore e trasferisce nei Sottoscrittori le transazioni archiviate nel database di distribuzione. L'agente di distribuzione viene eseguito nel server di distribuzione per le sottoscrizioni push o nel Sottoscrittore per le sottoscrizioni pull. Per altre informazioni, vedere [Replication Distribution Agent](replication-distribution-agent.md).  
  
## <a name="merge-agent"></a>Agente di merge  
 L'agente di merge viene utilizzato nella replica di tipo merge. Questo agente applica lo snapshot iniziale al Sottoscrittore e trasferisce e riconcilia le modifiche incrementali apportate ai dati. Per ogni sottoscrizione di tipo merge è disponibile un agente di merge specifico che si connette sia al server di pubblicazione che al Sottoscrittore aggiornandoli entrambi. L'agente di merge viene eseguito nel server di distribuzione per le sottoscrizioni push o nel Sottoscrittore per le sottoscrizioni pull. Per impostazione predefinita, l'agente di merge carica le modifiche dal Sottoscrittore al server di pubblicazione e quindi scarica le modifiche dal server di pubblicazione al Sottoscrittore. Per altre informazioni, vedere [Replication Merge Agent](replication-merge-agent.md).  
  
## <a name="queue-reader-agent"></a>Agente di lettura coda  
 L'agente di lettura coda viene utilizzato nella replica transazionale con l'opzione di aggiornamento in coda. L'agente viene eseguito nel server di distribuzione e trasferisce le modifiche apportate nel Sottoscrittore nuovamente nel server di pubblicazione. A differenza dell'agente di distribuzione e dell'agente di merge, per tutti i server di pubblicazione e le pubblicazioni di un database di distribuzione specifico esiste una sola istanza dell'agente di lettura coda. Per altre informazioni sull'agente di lettura coda, vedere [Replication Queue Reader Agent](replication-queue-reader-agent.md). Per altre informazioni sulle sottoscrizioni aggiornabili, vedere [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="replication-maintenance-jobs"></a>Processi di manutenzione della replica  
 La replica include alcuni processi di manutenzione che consentono di eseguire operazioni di manutenzione pianificata e su richiesta. Per altre informazioni, vedere [Amministrazione dell'agente di replica](replication-agent-administration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Eseguire processi di manutenzione della replica &#40;SQL Server Management Studio&#41;](../administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md)   
 [Amministrazione dell'agente di replica](replication-agent-administration.md)  
  
  
