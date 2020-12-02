---
title: Visualizzare e modificare i parametri del prompt dei comandi degli agenti
description: Informazioni su come visualizzare e modificare i parametri del prompt dei comandi usati dai diversi agenti di replica in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 10ef5b2c2e873d3f17085137134aabd8db57b059
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131030"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Gli agenti di replica sono file eseguibili che accettano parametri della riga di comando. Per impostazione predefinita, gli agenti vengono eseguiti in passaggi di processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Agent, quindi questi parametri possono essere visualizzati e modificati usando la finestra di dialogo **Proprietà processo - \<Job>** . accessibile dalla cartella **Processi** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e dalla scheda **Agenti** di Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Le modifiche apportate al parametro dell'agente verranno applicate al successivo avvio dell'agente. Se l'agente viene eseguito in modo continuo, è necessario arrestarlo e riavviarlo.  
  
 Sebbene i parametri possano essere modificati direttamente, in genere li si modifica tramite un profilo agente. Per altre informazioni, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Se si accede ai processi agente dalla cartella **Processi** , utilizzare la tabella seguente per determinare il nome del processo agente e i parametri disponibili per ogni agente.  
  
|Agente|Nome processo|Per l'elenco dei parametri, vedere...|  
|-----------|--------------|------------------------------------|  
|agente snapshot|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente snapshot per una partizione di una pubblicazione di tipo merge|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente di lettura log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[Agente lettura log repliche](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Agente di merge per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente di merge per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente di distribuzione per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente di distribuzione per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente di distribuzione per le sottoscrizioni push di Sottoscrittori non SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente di lettura coda|**[\<Distributor>].\<integer>**|[Agente di lettura coda repliche](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Per le sottoscrizioni push di pubblicazioni Oracle, è **\<Publisher>-\<Publisher**> invece di **\<Publisher>-\<PublicationDatabase>**  
  
 \*\*Per le sottoscrizioni pull di pubblicazioni Oracle, è **\<Publisher>-\<DistributionDatabase**> invece di **\<Publisher>-\<PublicationDatabase>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente di replica in Management Studio  
  
1.  Connettersi al computer appropriato in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server:  
  
    -   Per l'agente di distribuzione e l'agente di merge per le sottoscrizioni pull, connettersi al Sottoscrittore.  
  
    -   Per tutti gli altri agenti, connettersi al server di distribuzione.  
  
2.  Espandere la cartella **SQL Server Agent** e quindi la cartella **Processi** .  
  
3.  Fare clic con il pulsante destro del mouse su un processo e scegliere **Proprietà**.  
  
4.  Nella pagina **Passaggi** della finestra di dialogo **Proprietà processo - \<Job>** selezionare il passaggio **Esecuzione agente** e quindi fare clic su **Modifica**.  
  
5.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
6.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente di distribuzione e dell'agente di merge in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
4.  Nella finestra **Sottoscrizione < NomeSottoscrizione>** fare clic su **Azione** e quindi su **Proprietà processo - \<AgentName>** .  
  
5.  Nella pagina **Passaggi** della finestra di dialogo **Proprietà processo - \<Job>** selezionare il passaggio **Esecuzione agente** e quindi fare clic su **Modifica**.  
  
6.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
7.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente snapshot, dell'agente di lettura log e dell'agente di lettura coda in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Agenti** .  
  
3.  Fare clic con il pulsante destro del mouse su un punto all'interno del riquadro della griglia e quindi scegliere **Proprietà**.  
  
4.  Nella pagina **Passaggi** della finestra di dialogo **Proprietà processo - \<Job>** selezionare il passaggio **Esecuzione agente** e quindi fare clic su **Modifica**.  
  
5.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
6.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione dell'agente di replica](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Concetti di base relativi ai file eseguibili dell'agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Panoramica degli agenti di replica](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
