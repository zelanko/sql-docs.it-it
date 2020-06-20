---
title: Sicurezza agente &lt;NomeAgente&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 75d4cccdb867716cf16490b4662edec4d5856fe6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016783"
---
# <a name="ltagentnamegt-agent-security"></a>Sicurezza agente &lt;NomeAgente&gt;
  La pagina ** \<AgentName> sicurezza agente** consente di specificare gli account utilizzati per l'esecuzione del agente di distribuzione (per la replica transazionale e snapshot) o agente di merge (per la replica di tipo merge) e per stabilire connessioni ai computer in una topologia di replica. Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md) e [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opzioni  
 Fare clic sul pulsante delle proprietà ( **...** ) nella riga di ciascun Sottoscrittore per accedere alla finestra di dialogo **Sicurezza agente di distribuzione** o **Sicurezza agente di merge** . Per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dagli agenti, fare clic su **?** nella finestra di dialogo visualizzata.  
  
 Dopo l'immissione delle impostazioni in una delle finestre di dialogo, le informazioni di connessione per il Sottoscrittore vengono visualizzate nella griglia.  
  
 **Agente per Sottoscrittore**  
 Nome di ciascun Sottoscrittore.  
  
 **Connessione al server di distribuzione**  
 Visualizzato per la replica transazionale e snapshot. Contesto in cui viene creata la connessione al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni push, la connessione locale è la connessione al server di distribuzione, pertanto in questo campo viene sempre visualizzato: **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '** per le sottoscrizioni push.  
  
-   Per le sottoscrizioni pull, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nel campo viene visualizzato uno dei seguenti elementi: **Usa account di accesso ' \<Login> '**, **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
 **Connessione al server di pubblicazione e al server di distribuzione**  
 Visualizzato per la replica di tipo merge. Contesto in cui vengono create le connessioni al server di pubblicazione e al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni push, la connessione locale è la connessione al server di pubblicazione e al server di distribuzione, pertanto in questo campo viene sempre visualizzato: **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '** per le sottoscrizioni push.  
  
-   Per le sottoscrizioni pull, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nel campo viene visualizzato uno dei seguenti elementi: **Usa account di accesso ' \<Login> '**, **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
 **Connessione al Sottoscrittore**  
 Contesto in cui viene creata la connessione al Sottoscrittore. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni pull, la connessione locale è la connessione al Sottoscrittore, pertanto in questo campo viene sempre visualizzato: **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '** per le sottoscrizioni push.  
  
-   Per le sottoscrizioni push, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nel campo viene visualizzato uno dei seguenti elementi: **Usa account di accesso ' \<Login> '**, **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](view-and-modify-pull-subscription-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](view-and-modify-push-subscription-properties.md)   
 [Gestire gli account di accesso e le password nella replica](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md)   
 [Sicurezza replica di SQL Server](security/view-and-modify-replication-security-settings.md)  
  
  
