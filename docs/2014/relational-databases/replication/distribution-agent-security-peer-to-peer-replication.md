---
title: Sicurezza agente di distribuzione (replica peer-to-peer) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78d8baed7783459db79bb9facb0141cc570c4127
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765513"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>Sicurezza agente di distribuzione (replica peer-to-peer)
  La pagina **Sicurezza agente di distribuzione** consente di specificare gli account utilizzati per eseguire l'agente di distribuzione e per stabilire connessioni ai computer in una topologia peer-to-peer. Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md) e [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Se l'agente di distribuzione per una sottoscrizione è già stato configurato in un'esecuzione precedente della procedura guidata, non è possibile modificare le credenziali utilizzate in questa procedura. Se vengono specificate nuove credenziali, queste verranno ignorate. Per modificare le credenziali, utilizzare la finestra di dialogo **Proprietà sottoscrizione** . Per altre informazioni, vedere [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opzioni  
 Fare clic sul pulsante delle proprietà (**...**) nella riga di ciascun Sottoscrittore per accedere alla finestra di dialogo **Sicurezza agente di distribuzione** . Per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dagli agenti, fare clic su **?** nella finestra di dialogo **Sicurezza agente di distribuzione** .  
  
 Dopo l'immissione delle impostazioni in una delle finestre di dialogo, le informazioni di connessione per il Sottoscrittore vengono visualizzate nella griglia.  
  
 **Agente per Sottoscrittore**  
 Nome di ciascun peer.  
  
 **Database peer**  
 Il database nel peer che fungerà da database di pubblicazione e da database di sottoscrizione.  
  
 **Connessione al server di distribuzione**  
 Contesto in cui viene creata la connessione al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente. Questa procedura guidata vengono create sottoscrizioni push (la connessione locale è la connessione al server di distribuzione), pertanto in questo campo viene sempre visualizzato: **Rappresentare '\<dominio >\\< Login\>'** oppure **rappresentare '\<Computer >\\< Login\>'**.  
  
 **Connessione al Sottoscrittore**  
 Contesto in cui viene creata la connessione al Sottoscrittore. La connessione può essere creata tramite il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente o nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il campo viene visualizzato uno dei seguenti: **Account di accesso di Usa '\<account di accesso >'**, **rappresenta '\<dominio >\\< account di accesso\>'** oppure **Impersonate '\<Computer >\\< account di accesso\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;programmazione Transact-SQL della replica&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
