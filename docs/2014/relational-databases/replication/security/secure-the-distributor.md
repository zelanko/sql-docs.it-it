---
title: Proteggere il database di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bb6f278b18381d1b3d3defdb53a7c40a6f673ad
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135501"
---
# <a name="secure-the-distributor"></a>Sicurezza del database di distribuzione
  Gli agenti di replica che si connettono al server di distribuzione sono l'agente di lettura log, l'agente snapshot, l'agente di lettura coda, l'agente di distribuzione e l'agente di merge. È importante fornire un account di accesso appropriato per ognuno di questi agenti seguendo il principio di concedere i diritti minimi necessari nonché proteggere l'archiviazione di tutte le password:  
  
-   Per informazioni sulla gestione di account di accesso e password, vedere [Gestire gli account di accesso e le password nella replica](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
-   Per informazioni sulle autorizzazioni richieste per ogni agente, vedere [Replication Agent Security Model](replication-agent-security-model.md).  
  
 Oltre a gestire correttamente account di accesso e password, è fondamentale comprendere il ruolo del collegamento del server remoto **repl_distributor** e dell'account **distributor_admin** .  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>Protezione della connessione dal server di pubblicazione al server di distribuzione  
 Per supportare la comunicazione necessaria quando le stored procedure amministrative vengono eseguite nel server di pubblicazione e aggiornare le informazioni nel server di distribuzione, il server remoto **repl_distributor**viene configurato automaticamente durante la replica. La voce del server remoto **repl_distributor** viene utilizzata per le comunicazioni con il database di distribuzione indipendentemente dal fatto che il database di distribuzione sia contenuto nell'istanza del server di pubblicazione (un server di distribuzione locale) o risieda in un'istanza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remota (un server di distribuzione remoto).  
  
 Quando il database di distribuzione è contenuto in un'istanza locale, una password casuale viene generata e configurata automaticamente. Quando invece si trova in un'istanza remota, l'amministratore configura una password condivisa durante l'installazione del server di pubblicazione e del server di distribuzione. Tale password viene quindi utilizzata per fornire l'autenticazione del traffico che attraversa il collegamento **repl_distributor** .  
  
 Il server di distribuzione utilizza la voce del server remoto **repl_distributor** per verificare che il server chiamante sia configurato come server di pubblicazione nel server di distribuzione, convalida la password fornita dal server di pubblicazione e quindi verifica in fase di esecuzione che la stored procedure sia una stored procedure di replica.  
  
 La password configurata per la voce del server remoto **repl_distributor** durante l'installazione viene associata all'account di accesso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] distributor_admin **di**, che viene aggiunto al ruolo predefinito del server **sysadmin** nel server di distribuzione. L'account di accesso **distributor_admin** viene utilizzato dalle stored procedure di replica durante la connessione al server di distribuzione.  
  
> [!NOTE]  
>  Non modificare manualmente la password di **distributor_admin** . Utilizzare sempre la stored procedure **sp_changedistributor_password** o le finestre di dialogo **Proprietà database di distribuzione** o **Aggiorna password di replica** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], in quanto le modifiche apportate alle password vengono successivamente applicate alle pubblicazioni locali in modo automatico.  
  
## <a name="snapshot-folder-security"></a>Sicurezza della cartella snapshot  
 Verificare che la condivisione snapshot disponga di accesso in lettura per l'account con il quale viene eseguito l'agente di merge (per la replica di tipo merge) o l'agente di distribuzione (per la replica snapshot o transazionale) e di accesso in scrittura per l'account con il quale viene eseguito l'agente snapshot. Per altre informazioni sulla cartella snapshot, vedere [Proteggere la cartella snapshot](secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](view-and-modify-replication-security-settings.md)   
 [Abilitare connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Sicurezza della replica di SQL Server](view-and-modify-replication-security-settings.md)  
  
  
