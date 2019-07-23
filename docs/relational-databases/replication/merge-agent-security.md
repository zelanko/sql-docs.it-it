---
title: Sicurezza agente di merge | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 45cc5e8c2ca3e311704ffd4eb6577d2e934d484a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140716"
---
# <a name="merge-agent-security"></a>Sicurezza agente di merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Sicurezza agente di merge** consente di specificare l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] con cui viene eseguito l'agente di merge. L'agente di merge viene eseguito nel server di distribuzione per le sottoscrizioni push e nel Sottoscrittore per le sottoscrizioni pull. L'account di Windows è detto anche *account di processo*, poiché si tratta dell'account con cui viene eseguito il processo dell'agente. Le opzioni aggiuntive disponibili in questa finestra di dialogo dipendono dalla modalità con cui si accede a tale finestra di dialogo:  
  
-   Se si accede alla finestra di dialogo dalla Creazione guidata nuova sottoscrizione, è inoltre possibile specificare il contesto in cui l'agente di merge stabilisce le connessioni al Sottoscrittore (per le sottoscrizioni push) o ai server di pubblicazione e di distribuzione (per le sottoscrizioni pull). È possibile stabilire la connessione utilizzando l'account di Windows oppure nel contesto di un account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato dall'utente.  
  
-   Se si accede alla finestra di dialogo dalla finestra di dialogo **Proprietà sottoscrizione** , specificare il contesto in cui l'agente di merge stabilisce le connessioni facendo clic sul pulsante delle proprietà ( **...** ) nella riga **Connessione al Sottoscrittore** o **Connessione al server di pubblicazione** della finestra di dialogo. Per altre informazioni sull'accesso alla finestra di dialogo **Proprietà delle sottoscrizioni**, vedere [Visualizzare e modificare le proprietà delle sottoscrizioni push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Tutti gli account devono essere validi e per ogni account deve essere stata specificata la password corretta. Gli account e le password vengono convalidati solo dopo l'avvio dell'esecuzione di un agente.  
  
## <a name="options"></a>Opzioni  
 **Process Account**  
 Consente di immettere l'account di Windows con cui viene eseguito l'agente di merge.  
  
-   Per le sottoscrizioni push, l'account deve:  
  
    -   Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.  
  
    -   Essere un membro del ruolo PAL.  
  
    -   Essere un account di accesso associato a un utente nel database di pubblicazione.  
  
    -   Disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
-   Per le sottoscrizioni pull, l'account deve essere almeno un membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.  
  
 Sono necessarie autorizzazioni aggiuntive nel caso in cui l'account di processo sia rappresentato durante l'attivazione delle connessioni. Vedere le sezioni **Connetti al server di pubblicazione e al server di distribuzione** e **Connetti al Sottoscrittore** riportate di seguito.  
  
 Non è possibile specificare **l'account di processo** per le sottoscrizioni pull di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], in quanto l'agente di merge non viene eseguito nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Password** e **Conferma password**  
 Immettere la password per l'account di Windows.  
  
 **Connetti al server di pubblicazione e al server di distribuzione**  
 Per le sottoscrizioni push, le connessioni al server di pubblicazione e al server di distribuzione vengono sempre stabilite tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
 Per le sottoscrizioni pull, scegliere se l'agente di merge deve stabilire le connessioni al server di pubblicazione e al server di distribuzione tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** oppure utilizzando un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona l'opzione per l'utilizzo di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere un account di accesso e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di scegliere di rappresentare l'account di Windows anziché di utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'account di Windows o l'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per la connessione deve:  
  
-   Essere un membro del ruolo PAL.  
  
-   Essere un account di accesso associato a un utente nel database di pubblicazione.  
  
-   Essere un account di accesso associato a un utente nel database di distribuzione (l'utente può essere l'utente Guest).  
  
-   Disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
 **Connetti al Sottoscrittore**  
 Per le sottoscrizioni pull, le connessioni al Sottoscrittore vengono sempre stabilite tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
 Per le sottoscrizioni push, scegliere se l'agente di merge deve stabilire le connessioni al server di pubblicazione e al server di distribuzione tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** oppure utilizzando un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona l'opzione per l'utilizzo di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere un account di accesso e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  È consigliabile scegliere di rappresentare l'account di Windows anziché di utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'account di Windows o l'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per la connessione deve essere almeno un membro del ruolo del database predefinito **db_owner** nel database di sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire gli account di accesso e le password nella replica](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sottoscrizione delle pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
