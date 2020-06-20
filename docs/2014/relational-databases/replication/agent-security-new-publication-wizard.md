---
title: Sicurezza agente (Creazione guidata nuova pubblicazione) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 388554360003fe31bc1d7d93063832b6d265e359
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055709"
---
# <a name="agent-security-new-publication-wizard"></a>Sicurezza agente (Creazione guidata nuova pubblicazione)
  La pagina **Sicurezza agente** consente di specificare gli account nell'ambito dei quali gli agenti seguenti vengono eseguiti e si connettono ai computer in una topologia di replica.  
  
-   Agente snapshot per tutte le pubblicazioni.  
  
-   Agente di lettura log per tutte le pubblicazioni transazionali.  
  
-   Agente di lettura coda per le pubblicazioni transazionali con sottoscrizioni aggiornabili. Il processo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per questo agente viene creato se si è specificata l'opzione **Pubblicazione transazionale con sottoscrizioni aggiornabili** nella pagina **Tipo di pubblicazione**, indipendentemente dal tipo di sottoscrizioni aggiornabili usate. Per altre informazioni sulle sottoscrizioni aggiornabili, vedere [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Replication Agent Security Model](security/replication-agent-security-model.md) e [Replication Security Best Practices](security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opzioni  
 **Agente snapshot**  
 Visualizzato per tutte le pubblicazioni. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra **Sicurezza agente snapshot** .  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente snapshot** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente snapshot.  
  
 **Agente di lettura log**  
 Visualizzato per tutte le pubblicazioni transazionali. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra **Sicurezza agente di lettura log** .  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente di lettura log** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente di lettura log.  
  
> [!NOTE]  
>  esiste un agente di lettura log per ogni database pubblicato tramite la replica transazionale. Se esiste già una replica transazionale nel database, le impostazioni di sicurezza sono di sola lettura. È possibile modificare le impostazioni nella finestra di dialogo **Proprietà pubblicazione** , tuttavia le modifiche avranno effetto su tutte le pubblicazioni transazionali nel database.  
  
 **Agente di lettura coda**  
 Visualizzato per le pubblicazioni transazionali con sottoscrizioni aggiornabili. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra di dialogo **Sicurezza agente di lettura coda** . Un processo di agente di lettura coda viene creato al termine della procedura guidata indipendentemente dalla creazione di sottoscrizioni ad aggiornamento in coda. Se non si prevede di creare sottoscrizioni ad aggiornamento in coda, è possibile disabilitare il processo. Fare clic con il pulsante destro del mouse sul processo (denominato nel formato: *[ \<Publisher> ] \<integer> .*.) nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cartella **processi** di Agent, quindi scegliere **Disabilita**.  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente di lettura coda** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente di lettura coda.  
  
> [!NOTE]  
>  Esiste un unico agente di lettura coda per ogni database di distribuzione e tutti i server di pubblicazione che utilizzano il database. Se esiste già una pubblicazione transazionale che consente sottoscrizioni con aggiornamento in coda in uno qualsiasi dei server di pubblicazione che utilizzano un database di distribuzione specifico, le impostazioni di sicurezza sono di sola lettura. Nella finestra di dialogo **Proprietà server di distribuzione** è possibile modificare l'account nel cui ambito l'agente di lettura coda viene eseguito e si connette. Tuttavia le modifiche avranno effetto su tutti i server di pubblicazione che utilizzano il database di distribuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Gestire gli account di accesso e le password nella replica](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
