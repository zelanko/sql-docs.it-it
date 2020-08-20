---
description: Sicurezza agente &lt;NomeAgente&gt;
title: Sicurezza agente &lt;NomeAgente&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 283f19912bcb5f3c57f84c845d9bf051a7c211d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470366"
---
# <a name="ltagentnamegt-agent-security"></a>Sicurezza agente &lt;NomeAgente&gt;
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La pagina **\<AgentName>Sicurezza agente**  consente di specificare gli account usati per l'esecuzione dall'agente di distribuzione (per la replica transazionale e snapshot) o dall'agente di merge (per la replica di tipo merge) e per la creazione di connessioni ai computer in una topologia di replica. Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md) e [Procedure consigliate per la sicurezza della replica](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opzioni  
 Fare clic sul pulsante delle proprietà ( **...** ) nella riga di ciascun Sottoscrittore per accedere alla finestra di dialogo **Sicurezza agente di distribuzione** o **Sicurezza agente di merge** . Per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dagli agenti, fare clic su **?** nella finestra di dialogo visualizzata.  
  
 Dopo l'immissione delle impostazioni in una delle finestre di dialogo, le informazioni di connessione per il Sottoscrittore vengono visualizzate nella griglia.  
  
 **Agente per Sottoscrittore**  
 Nome di ciascun Sottoscrittore.  
  
 **Connessione al server di distribuzione**  
 Visualizzato per la replica transazionale e snapshot. Contesto in cui viene creata la connessione al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni push, la connessione locale è quella stabilita con il server di distribuzione, pertanto in questo campo viene sempre visualizzato: **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>** ' per le sottoscrizioni push.  
  
-   Per le sottoscrizioni pull, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo campo viene visualizzato uno dei valori seguenti: **Usa l'account di accesso '\<Login>'** , **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>'** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
 **Connessione al server di pubblicazione e al server di distribuzione**  
 Visualizzato per la replica di tipo merge. Contesto in cui vengono create le connessioni al server di pubblicazione e al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni push, la connessione locale è quella stabilita con il server di pubblicazione e il server di distribuzione, pertanto in questo campo viene sempre visualizzato: **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>** ' per le sottoscrizioni push.  
  
-   Per le sottoscrizioni pull, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo campo viene visualizzato uno dei valori seguenti: **Usa l'account di accesso '\<Login>'** , **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>'** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
 **Connessione al Sottoscrittore**  
 Contesto in cui viene creata la connessione al Sottoscrittore. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente:  
  
-   Per le sottoscrizioni pull, la connessione locale è quella stabilita con il Sottoscrittore, pertanto in questo campo viene sempre visualizzato: **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>** ' per le sottoscrizioni push.  
  
-   Per le sottoscrizioni push, la connessione può inoltre essere creata nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo campo viene visualizzato uno dei valori seguenti: **Usa l'account di accesso '\<Login>'** , **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>'** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Controllo di identità e accesso (replica)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
