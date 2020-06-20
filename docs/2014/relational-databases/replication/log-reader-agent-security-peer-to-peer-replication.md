---
title: Sicurezza agente di lettura log (replica peer-to-peer) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae5c8d56c1d51290c35a04c22474fcc04ddff61d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065906"
---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Sicurezza agente di lettura log (replica peer-to-peer)
   La pagina **Sicurezza agente di lettura log** consente di specificare gli account con cui viene eseguito l'agente di lettura in ogni peer e vengono stabilite le connessioni. Per informazioni sulle autorizzazioni necessarie per gli agenti e le procedure migliori per la sicurezza della replica, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md) e [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  esiste un agente di lettura log per ogni database pubblicato tramite la replica transazionale. Se l'agente di lettura log per un database è già stato configurato per una pubblicazione nel corso di una precedente esecuzione di questa procedura guidata oppure per un'altra pubblicazione transazionale nello stesso database, in questa procedura guidata non è possibile modificare le credenziali utilizzate dall'agente di lettura log. Se vengono specificate nuove credenziali, queste verranno ignorate. Per modificare le credenziali utilizzare la finestra di dialogo **Proprietà pubblicazione** . Per altre informazioni, vedere [visualizzare e modificare le impostazioni di sicurezza della replica](security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opzioni  
 Fare clic sul pulsante delle proprietà (**...**) nella riga di ogni peer per accedere alla finestra di dialogo **Sicurezza agente di lettura log** . Per ulteriori informazioni sulle autorizzazioni necessarie per gli account utilizzati dall'agente, fare clic su **?** nella finestra di dialogo **Sicurezza agente di lettura log** visualizzata.  
  
 Dopo aver immesso le impostazioni nella finestra di dialogo, nella griglia vengono visualizzate le informazioni sulla connessione per il Sottoscrittore.  
  
 **Agenti per il server di pubblicazione**  
 Nome di ogni istanza del server peer.  
  
 **Database peer**  
 Database che funge da database di pubblicazione e da database di sottoscrizione in ogni peer.  
  
 **Connessione al server di distribuzione**  
 Contesto in cui viene creata la connessione al server di distribuzione. La connessione locale al server di distribuzione viene sempre eseguita utilizzando il contesto dell' [!INCLUDE[msCoName](../../includes/msconame-md.md)] account di Windows con cui viene eseguito l'agente, pertanto in questo campo viene sempre visualizzato rappresenta **' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '**.  
  
 **Connessione server di pubblicazione**  
 Contesto nel quale viene stabilita la connessione al server di pubblicazione. La connessione al server di pubblicazione può essere effettuata utilizzando un account [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accesso di oppure utilizzando il contesto dell'account di Windows con cui viene eseguito l'agente. Nel campo viene visualizzato uno dei seguenti elementi: **Usa account di accesso ' \<Login> '**, **rappresenta ' \<Domain> \\<account di accesso \> '** o **rappresenta ' \<Computer> \\<account di accesso \> '**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di stabilire tutte le connessioni utilizzando il contesto dell'account di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;la programmazione Transact-SQL della replica&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Replica transazionale peer-to-peer](transactional/peer-to-peer-transactional-replication.md)  
  
  
