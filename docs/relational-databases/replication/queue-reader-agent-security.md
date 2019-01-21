---
title: Sicurezza agente di lettura coda | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d37032b9c13d9447ba5879e5e29bd91256c75398
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133439"
---
# <a name="queue-reader-agent-security"></a>Sicurezza agente di lettura coda
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Sicurezza agente di lettura coda** consente di specificare l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con cui viene eseguito l'agente di lettura coda e vengono stabilite le connessioni locali al server di distribuzione. L'agente si connette al server di pubblicazione utilizzando l'account specificato nella finestra di dialogo **Proprietà server di pubblicazione** , alla quale è possibile accedere dalla finestra di dialogo **Proprietà server di distribuzione** . L'agente si connette al Sottoscrittore utilizzando lo stesso contesto dell'agente di distribuzione per la sottoscrizione. Per altre informazioni, vedere [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 L'account deve essere valido è deve essere stata specificata la password corretta. Gli account e le password vengono convalidati solo dopo l'avvio dell'esecuzione di un agente.  
  
## <a name="options"></a>Opzioni  
 **Account processo**  
 Consente di immettere l'account di Windows con cui viene eseguito l'agente di lettura coda nel server di distribuzione. L'account di Windows specificato deve essere almeno membro del ruolo predefinito del database **db_owner** nel server di distribuzione.  
  
 **Password** e **Conferma password**  
 Immettere la password per l'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Controllo di identità e accesso (replica)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Procedure consigliate per la sicurezza della replica](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
