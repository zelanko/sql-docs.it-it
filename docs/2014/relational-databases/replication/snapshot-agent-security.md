---
title: Sicurezza agente snapshot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6bfd64cea8d661b2d1d5b1b4c7e581d2f4e413a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055657"
---
# <a name="snapshot-agent-security"></a>Sicurezza agente snapshot
  La finestra di dialogo **Sicurezza agente snapshot** consente di specificare:  
  
-   L'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con cui viene eseguito l'agente snapshot nel server di distribuzione. L'account di Windows è detto anche *account di processo*, poiché si tratta dell'account con cui viene eseguito il processo dell'agente.  
  
-   Il contesto nel quale l'agente snapshot stabilisce le connessioni al server di pubblicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La connessione può essere stabilita tramite rappresentazione dell'account di Windows oppure nel contesto di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato dall'utente.  
  
    > [!NOTE]  
    >  L'agente snapshot stabilisce le connessioni al server di pubblicazione anche quando il server di pubblicazione e il server di distribuzione si trovano nello stesso computer. L'agente snapshot stabilisce inoltre le connessioni al server di distribuzione. Tali connessioni vengono sempre stabilite tramite rappresentazione dell'account di  Windows con cui viene eseguito l'agente.  
  
     Per i server di pubblicazione Oracle, specificare il contesto in cui l'agente snapshot si connette al server di pubblicazione nella finestra di dialogo **Proprietà server di pubblicazione** , alla quale è possibile accedere dalla finestra di dialogo **Proprietà server di distribuzione** . Per altre informazioni, vedere [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md).  
  
 Tutti gli account devono essere validi e per ogni account deve essere stata specificata la password corretta. Gli account e le password vengono convalidati solo dopo l'avvio dell'esecuzione di un agente.  
  
## <a name="options"></a>Opzioni  
 **Account processo**  
 Consente di immettere un account di Windows con cui eseguire l'agente snapshot nel server di distribuzione. L'account di Windows specificato deve:  
  
-   Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.  
  
-   Disporre delle autorizzazioni di scrittura per la condivisione snapshot.  
  
 **Password** e **Conferma password**  
 Immettere la password per l'account di Windows.  
  
 **Connessione al server di pubblicazione**  
 Consente di scegliere se l'agente snapshot deve stabilire le connessioni al server di distribuzione tramite rappresentazione dell'account specificato nella casella di testo **Account processo** oppure utilizzando un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona l'opzione per l'utilizzo di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere un account di accesso e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  È consigliabile scegliere di rappresentare l'account di Windows anziché di utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'account di Windows o l'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per la connessione deve essere almeno un membro del ruolo del database predefinito **db_owner** nel database di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire gli account di accesso e le password nella replica](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)  
  
  
