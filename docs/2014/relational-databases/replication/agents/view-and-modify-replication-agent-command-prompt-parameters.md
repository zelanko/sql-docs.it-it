---
title: Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e64551075920f2f08bf84fe22086c06387b4439a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068746"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters-sql-server-management-studio"></a>Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica (SQL Server Management Studio)
  Gli agenti di replica sono file eseguibili che accettano parametri della riga di comando. Per impostazione predefinita, gli agenti vengono eseguiti in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] passaggi di processo di Agent, quindi questi parametri possono essere visualizzati e modificati tramite la finestra di dialogo **Proprietà processo- \<Job> ** . accessibile dalla cartella **Processi** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e dalla scheda **Agenti** di Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](../monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Le modifiche apportate al parametro dell'agente verranno applicate al successivo avvio dell'agente. Se l'agente viene eseguito in modo continuo, è necessario arrestarlo e riavviarlo.  
  
 Sebbene i parametri possano essere modificati direttamente, in genere li si modifica tramite un profilo agente. Per altre informazioni, vedere [Replication Agent Profiles](replication-agent-profiles.md).  
  
 Se si accede ai processi agente dalla cartella **Processi** , utilizzare la tabella seguente per determinare il nome del processo agente e i parametri disponibili per ogni agente.  
  
|Agente|Nome processo|Per un elenco dei parametri, vedere...|  
|-----------|--------------|------------------------------------|  
|agente snapshot|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Agente snapshot per una partizione di una pubblicazione di tipo merge|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Agente di lettura log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[Agente lettura log repliche](replication-log-reader-agent.md)|  
|Agente di merge per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Agente di merge per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Agente di distribuzione per le sottoscrizioni push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**<sup>1</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente di distribuzione per le sottoscrizioni pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**<sup>2</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente di distribuzione per le sottoscrizioni push di Sottoscrittori non SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente di lettura coda|**[\<Distributor>].\<integer>**|[Agente di lettura coda repliche](replication-queue-reader-agent.md)|  
  
 <sup>1</sup> per le sottoscrizioni push di pubblicazioni Oracle, è * * \<Publisher> - \<Publisher**> anziché**\<Publisher>-\<PublicationDatabase>**  
  
 <sup>2</sup> per le sottoscrizioni pull di pubblicazioni Oracle, è * * \<Publisher> - \<DistributionDatabase**> anziché**\<Publisher>-\<PublicationDatabase>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente di replica in Management Studio  
  
1.  Connettersi al computer appropriato in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server:  
  
    -   Per l'agente di distribuzione e l'agente di merge per le sottoscrizioni pull, connettersi al Sottoscrittore.  
  
    -   Per tutti gli altri agenti, connettersi al server di distribuzione.  
  
2.  Espandere la cartella **SQL Server Agent** e quindi la cartella **Processi** .  
  
3.  Fare clic con il pulsante destro del mouse su un processo e scegliere **Proprietà**.  
  
4.  Nella pagina **passaggi** della finestra di dialogo **Proprietà processo \<Job> -** selezionare il passaggio **esecuzione agente**e quindi fare clic su **modifica**.  
  
5.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
6.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente di distribuzione e dell'agente di merge in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
4.  Nella finestra **sottoscrizione \< SubscriptionName> ** fare clic su **azione**e quindi su ** \<AgentName> Proprietà processo**.  
  
5.  Nella pagina **passaggi** della finestra di dialogo **Proprietà processo \<Job> -** selezionare il passaggio **esecuzione agente**e quindi fare clic su **modifica**.  
  
6.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
7.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Per visualizzare e modificare i parametri della riga di comando dell'agente snapshot, dell'agente di lettura log e dell'agente di lettura coda in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Agenti** .  
  
3.  Fare clic con il pulsante destro del mouse su un punto all'interno del riquadro della griglia e quindi scegliere **Proprietà**.  
  
4.  Nella pagina **passaggi** della finestra di dialogo **Proprietà processo \<Job> -** selezionare il passaggio **esecuzione agente**e quindi fare clic su **modifica**.  
  
5.  Nella finestra di dialogo **Proprietà passaggio processo - Esecuzione agente** modificare il campo **Comando** .  
  
6.  Fare clic su **OK** in entrambe le finestre di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione dell'agente di replica](replication-agent-administration.md)   
 [Concetti relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md)   
 [Panoramica degli agenti di replica](replication-agents-overview.md)  
  
  
