---
title: Account di accesso per sottoscrizioni aggiornabili | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d242fc31411bc0fdb05cca1f65355f49acec575a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85640424"
---
# <a name="login-for-updatable-subscriptions"></a>Account di accesso per sottoscrizioni aggiornabili
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Per l'aggiornamento immediato, se si seleziona **Replica** nella pagina **Sottoscrizioni aggiornabili** di questa procedura guidata, è necessario specificare un account nel Sottoscrittore nel cui contesto vengono stabilite le connessioni al server di pubblicazione. 
  
 Le connessioni vengono usate dai trigger che si attivano presso il Sottoscrittore e propagano le modifiche al server di pubblicazione. Questo account è necessario anche se si seleziona **Accoda le modifiche ed esegui il commit appena possibile** nella pagina **Sottoscrizioni aggiornabili**. Per impostazione predefinita, la Creazione guidata nuova sottoscrizione configura gli aggiornamenti in coda con la possibilità di passare, se necessario, ad aggiornamenti immediati.  
  
> **IMPORTANTE** È consigliabile concedere all'account specificato per la connessione solo le autorizzazioni necessarie per l'inserimento, l'aggiornamento e l'eliminazione dei dati delle viste create dalla replica nel database di pubblicazione, non altre autorizzazioni. Concedere autorizzazioni nelle viste del database di pubblicazione con il formato dei nomi **syncobj_** _\<HexadecimalNumber>_ all'account configurato presso ogni Sottoscrittore.  
  
 Sono disponibili tre opzioni per il tipo di connessione:  
  
-   Un server collegato o remoto già definito.  
  
-   Un server collegato creato dalla replica. La connessione viene eseguita con le credenziali specificate in questa procedura guidata.  
  
-   Un server collegato creato dalla replica. La connessione viene eseguita con le credenziali dell'utente che apporta la modifica presso il Sottoscrittore.  
  
 In questa procedura guidata è possibile specificare le prime due opzioni. L'ultima opzione può essere specificata solo usando [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Specificare il valore **1** per il parametro `@security_mode`.  
  
## <a name="options"></a>Opzioni  
 **Crea un server collegato che stabilisce la connessione utilizzando l'autenticazione di SQL Server**  
 La replica crea un server collegato utilizzando le credenziali specificate nei campi **Nome account di accesso** e **Password** .  
  
 **Accesso**  
 Consente di immettere un account di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dispone solo delle autorizzazioni descritte in questo argomento.  
  
 **Password**  
 Consente di immettere una password complessa per l'account di accesso specificato nel campo **Nome account di accesso**.  
    
 **Usa un server collegato o remoto già definito**  
 Per questa opzione è necessario un server collegato o remoto già definito. Per altre informazioni, vedere [Server collegati &#40;motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) e [Server remoti](../../database-engine/configure-windows/remote-servers.md). Accertarsi che l'account di accesso utilizzato per il server collegato o remoto disponga di una password complessa e delle sole autorizzazioni descritte in questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Sottoscrizione delle pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
