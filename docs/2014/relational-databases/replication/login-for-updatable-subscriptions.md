---
title: Account di accesso per sottoscrizioni aggiornabili | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ccf1a79b2dc27bbc49628d11a0c6fb0cf0e4e50
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816623"
---
# <a name="login-for-updatable-subscriptions"></a>Account di accesso per sottoscrizioni aggiornabili
  Se si seleziona **Replica** nella pagina **Sottoscrizioni aggiornabili** di questa procedura guidata è necessario specificare un account nel Sottoscrittore nel cui contesto vengono stabilite le connessioni al server di pubblicazione per sottoscrizioni ad aggiornamento immediato. Le connessioni vengono utilizzate dai trigger che si attivano presso il Sottoscrittore e propagano le modifiche al server di pubblicazione. Questo account è necessario anche se si seleziona **Accoda le modifiche ed esegui il commit appena possibile** nella pagina **Sottoscrizioni aggiornabili** , perché per impostazione predefinita la Creazione guidata nuova sottoscrizione configura gli aggiornamenti in coda con la possibilità di passare, se necessario, ad aggiornamenti immediati.  
  
> [!IMPORTANT]  
>  È consigliabile concedere all'account specificato per la connessione solo le autorizzazioni necessarie per l'inserimento, l'aggiornamento e l'eliminazione dei dati delle viste create dalla replica nel database di pubblicazione. Concedere autorizzazioni per le viste del database di pubblicazione con nome formattato come **syncobj_***\<NumeroEsadecimale>* all'account configurato in ogni Sottoscrittore.  
  
 Sono disponibili tre opzioni per il tipo di connessione:  
  
-   Un server collegato o remoto già definito.  
  
-   Un server collegato creato dalla replica. La connessione viene eseguita con le credenziali specificate in questa procedura guidata.  
  
-   Un server collegato creato dalla replica. La connessione viene eseguita con le credenziali dell'utente che apporta la modifica presso il Sottoscrittore.  
  
 In questa procedura guidata è possibile specificare le prime due opzioni. L'ultima opzione può essere specificata solo usando [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Specificare il valore **1** per il parametro **@security_mode**.  
  
## <a name="options"></a>Opzioni  
 **Crea un server collegato che stabilisce la connessione utilizzando l'autenticazione di SQL Server**  
 La replica crea un server collegato utilizzando le credenziali specificate nei campi **Nome account di accesso** e **Password** .  
  
 **Nome account di accesso**  
 Consente di immettere un nome account di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dispone solo delle autorizzazioni descritte in questo argomento.  
  
 **Password**  
 Consente di immettere una password complessa per l'account di accesso specificato nel campo **Nome account di accesso**.  
  
 **Conferma password**  
 Consente di immettere nuovamente la password per confermarla.  
  
 **Usa un server collegato o remoto già definito**  
 Per questa opzione è necessario un server collegato o remoto già definito. Per altre informazioni, vedere [Server collegati &#40;motore di database&#41;](../linked-servers/linked-servers-database-engine.md) e [Server remoti](../../database-engine/configure-windows/remote-servers.md). Accertarsi che l'account di accesso utilizzato per il server collegato o remoto disponga di una password complessa e delle sole autorizzazioni descritte in questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](security/view-and-modify-replication-security-settings.md)   
 [Sottoscrizioni aggiornabili per la replica transazionale](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
