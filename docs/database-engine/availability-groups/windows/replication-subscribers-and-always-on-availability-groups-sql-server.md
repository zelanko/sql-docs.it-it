---
title: Sottoscrittori della replica e gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46348ec891fba60479633f824a96232290859cd3
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54298508"
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Sottoscrittori della replica e gruppi di disponibilità AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Quando viene eseguito il failover di un gruppo di disponibilità AlwaysOn contenente un database che opera come sottoscrittore di replica, la sottoscrizione di replica potrebbe non venire completata. Per i sottoscrittori transazionali, l'agente di distribuzione continuerà a replicare automaticamente se la sottoscrizione utilizza il nome del listener del gruppo di disponibilità del sottoscrittore. Per i sottoscrittori di merge, un amministratore di replica deve riconfigurare manualmente il sottoscrittore ricreando la sottoscrizione.  
  
## <a name="what-is-supported"></a>Operazioni supportate  
 La replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta il failover automatico del server di pubblicazione e il failover automatico dei sottoscrittori transazionali. Il failover di un server di distribuzione in un database di disponibilità non è supportato. I sottoscrittori della replica di tipo merge possono far parte di un gruppo di disponibilità, tuttavia sono necessarie azioni manuali per configurare il nuovo sottoscrittore dopo un failover. Non è possibile combinare i gruppi di disponibilità con gli scenari Websync e SQL Server Compact.  
  
## <a name="how-to-create-transactional-subscription-in-an-always-on-environment"></a>Come creare una sottoscrizione transazionale in un ambiente AlwaysOn  
 Per la replica transazionale, usare i passaggi seguenti per configurare un gruppo di disponibilità del sottoscrittore e impostarne il failover:  
  
1.  Prima di creare la sottoscrizione, aggiungere il database sottoscrittore al gruppo di disponibilità AlwaysOn appropriato.  
  
2.  Aggiungere il listener del gruppo di disponibilità del sottoscrittore come server collegato a tutti i nodi del gruppo di disponibilità. Questa operazione assicura che tutti i partner di failover potenziali siano in grado di riconoscere e connettersi al listener.  
  
3.  Usare lo script riportato nella sezione **Creazione di una sottoscrizione push di una replica transazionale** sottostante per creare la sottoscrizione con il nome del listener del gruppo di disponibilità del sottoscrittore. Dopo un failover, il nome del listener rimane sempre valido, mentre il nome del server effettivo del sottoscrittore dipenderà dal nodo effettivo diventato il nuovo nodo primario.  
  
    > [!NOTE]  
    >  La sottoscrizione deve essere creata usando uno script [!INCLUDE[tsql](../../../includes/tsql-md.md)] e non può essere creata con [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Se si crea una sottoscrizione pull:  
  
    1.  Nel nodo primario del sottoscrittore in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]aprire l'albero [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.  
  
    2.  Identificare il processo dell' **agente di distribuzione pull** e modificare il processo.  
  
    3.  Nel passaggio del processo **Esecuzione dell'agente** verificare i parametri `-Publisher` e `-Distributor` . Verificare che questi parametri contengano i nomi corretti del server diretto e dell'istanza del server di distribuzione e del database di pubblicazione.  
  
    4.  Modificare il parametro `-Subscriber` impostando il nome del listener del gruppo di disponibilità del sottoscrittore.  
  
 Quando si crea la sottoscrizione usando questa procedura, non si dovranno eseguire azioni dopo un failover.  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>Creazione di una sottoscrizione push di una replica transazionale  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>Per riprendere gli agenti di merge dopo il failover del gruppo di disponibilità del sottoscrittore  
 Per eseguire il merge della replica, un relativo amministratore deve riconfigurare manualmente il sottoscrittore attenendosi alla procedura seguente:  
  
1.  Eseguire **sp_subscription_cleanup** per rimuovere la sottoscrizione precedente per il sottoscrittore. Effettuare questa operazione nella nuova replica primaria, che precedentemente era la secondaria.  
  
2.  Ricreare la sottoscrizione creando una nuova sottoscrizione a partire da un nuovo snapshot.  
  
> [!NOTE]  
>  Il processo corrente non è pratico per i sottoscrittori della replica di tipo merge. Lo scenario principale per la replica di tipo merge, tuttavia, è composto da utenti disconnessi (desktop, portatili, dispositivi palmari) che non usano i gruppi di disponibilità AlwaysOn con il sottoscrittore.  
  
  
