---
title: Sicurezza agente di distribuzione (peer-to-peer)
description: Viene descritta la pagina "Sicurezza agente di distribuzione" per una topologia di replica peer-to-peer in SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f1c0fdf14be0fd4fa436fbfea079a8fb689e8dd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653661"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>Sicurezza agente di distribuzione (replica peer-to-peer)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La pagina **Sicurezza agente di distribuzione** consente di specificare gli account utilizzati per eseguire l'agente di distribuzione e per stabilire connessioni ai computer in una topologia peer-to-peer. Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md) e [Procedure consigliate per la sicurezza della replica](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Se l'agente di distribuzione per una sottoscrizione è già stato configurato in un'esecuzione precedente della procedura guidata, non è possibile modificare le credenziali utilizzate in questa procedura. Se vengono specificate nuove credenziali, queste verranno ignorate. Per modificare le credenziali, utilizzare la finestra di dialogo **Proprietà sottoscrizione** . Per altre informazioni, vedere [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opzioni  
 Fare clic sul pulsante delle proprietà ( **...** ) nella riga di ciascun Sottoscrittore per accedere alla finestra di dialogo **Sicurezza agente di distribuzione** . Per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dagli agenti, fare clic su **?** nella finestra di dialogo **Sicurezza agente di distribuzione** .  
  
 Dopo l'immissione delle impostazioni in una delle finestre di dialogo, le informazioni di connessione per il Sottoscrittore vengono visualizzate nella griglia.  
  
 **Agente per Sottoscrittore**  
 Nome di ciascun peer.  
  
 **Database peer**  
 Il database nel peer che fungerà da database di pubblicazione e da database di sottoscrizione.  
  
 **Connessione al server di distribuzione**  
 Contesto in cui viene creata la connessione al server di distribuzione. Le connessioni locali vengono create sempre mediante il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente. In questa procedura guidata vengono create sottoscrizioni push (la connessione locale è quella stabilita con il server di distribuzione), pertanto in questo campo viene sempre visualizzato: **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>'** .  
  
 **Connessione al Sottoscrittore**  
 Contesto in cui viene creata la connessione al Sottoscrittore. La connessione può essere creata tramite il contesto dell'account di Windows utilizzato per l'esecuzione dell'agente o nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo campo viene visualizzato uno dei valori seguenti: **Usa l'account di accesso '\<Login>'** , **Rappresenta '\<Domain>\\<Login\>'** o **Rappresenta '\<Computer>\\<Login\>'** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
