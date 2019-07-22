---
title: Sicurezza agente (Creazione guidata nuova pubblicazione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02ae52aa310f760b06c51f003bd417f26486a5f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027837"
---
# <a name="agent-security-new-publication-wizard"></a>Sicurezza agente (Creazione guidata nuova pubblicazione)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pagina **Sicurezza agente** consente di specificare gli account nell'ambito dei quali gli agenti seguenti vengono eseguiti e si connettono ai computer in una topologia di replica.  
  
-   Agente snapshot per tutte le pubblicazioni.  
  
-   Agente di lettura log per tutte le pubblicazioni transazionali.  
  
-   Agente di lettura coda per le pubblicazioni transazionali con sottoscrizioni aggiornabili. Il processo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per questo agente viene creato se si seleziona l'opzione **Pubblicazione transazionale con sottoscrizioni aggiornabili** nella pagina **Tipo di pubblicazione** , indipendentemente dal tipo di sottoscrizioni aggiornabili utilizzate. Per altre informazioni sulle sottoscrizioni aggiornabili, vedere [Sottoscrizioni aggiornabili - Per la replica transazionale](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opzioni  
 **agente snapshot**  
 Visualizzato per tutte le pubblicazioni. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra **Sicurezza agente snapshot** .  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente snapshot** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente snapshot.  
  
 **Agente di lettura log**  
 Visualizzato per tutte le pubblicazioni transazionali. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra **Sicurezza agente di lettura log** .  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente di lettura log** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente di lettura log.  
  
> [!NOTE]  
>  esiste un agente di lettura log per ogni database pubblicato tramite la replica transazionale. Se esiste già una replica transazionale nel database, le impostazioni di sicurezza sono di sola lettura. È possibile modificare le impostazioni nella finestra di dialogo **Proprietà pubblicazione** , tuttavia le modifiche avranno effetto su tutte le pubblicazioni transazionali nel database.  
  
 **Agente di lettura coda**  
 Visualizzato per le pubblicazioni transazionali con sottoscrizioni aggiornabili. Fare clic su **Impostazioni di sicurezza** per specificare le impostazioni di sicurezza nella finestra di dialogo **Sicurezza agente di lettura coda** . Un processo di agente di lettura coda viene creato al termine della procedura guidata indipendentemente dalla creazione di sottoscrizioni ad aggiornamento in coda. Se non si prevede di creare sottoscrizioni ad aggiornamento in coda, è possibile disabilitare il processo. Fare clic con il pulsante destro del mouse sul processo, con nome nel formato *[\<ServerPubblicazione>].\<intero>* ., nella cartella **Processi** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi scegliere **Disabilita**.  
  
 Fare clic su **?** nella finestra di dialogo **Sicurezza agente di lettura coda** per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente di lettura coda.  
  
> [!NOTE]  
>  Esiste un unico agente di lettura coda per ogni database di distribuzione e tutti i server di pubblicazione che utilizzano il database. Se esiste già una pubblicazione transazionale che consente sottoscrizioni con aggiornamento in coda in uno qualsiasi dei server di pubblicazione che utilizzano un database di distribuzione specifico, le impostazioni di sicurezza sono di sola lettura. Nella finestra di dialogo **Proprietà server di distribuzione** è possibile modificare l'account nel cui ambito l'agente di lettura coda viene eseguito e si connette. Tuttavia le modifiche avranno effetto su tutti i server di pubblicazione che utilizzano il database di distribuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Controllo di identità e accesso (replica)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
