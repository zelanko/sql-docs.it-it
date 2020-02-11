---
title: Abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 963fe86b0d5939c82bffb9c07d5adacbadadba89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68199418"
---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>Abilitazione delle sottoscrizioni aggiornabili per le pubblicazioni transazionali
  In questo argomento viene descritto come abilitare l'aggiornamento delle sottoscrizioni per pubblicazioni transazionali in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali nella pagina **Tipo di pubblicazione** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](create-a-publication.md). Dopo aver creato la pubblicazione, non è più possibile attivare le sottoscrizioni aggiornabili.  
  
 Per utilizzare le sottoscrizioni aggiornabili, è inoltre necessario configurare le opzioni della Creazione guidata nuova sottoscrizione. Per altre informazioni, vedere [Creazione di una sottoscrizione aggiornabile di una pubblicazione transazionale](../publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
#### <a name="to-enable-updating-subscriptions"></a>Per attivare le sottoscrizioni aggiornabili  
  
1.  Nella pagina **Tipo di pubblicazione** della Creazione guidata nuova pubblicazione, selezionare **Pubblicazione transazionale con sottoscrizioni aggiornabili**.  
  
2.  Nella pagina **Sicurezza agente** , specificare le impostazioni di sicurezza per l'agente di lettura coda, per l'agente snapshot e per l'agente di lettura log. Per ulteriori informazioni sulle autorizzazioni necessarie per l'account con cui viene eseguito l'agente di lettura coda, vedere [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
    > [!NOTE]  
    >  L'agente di lettura coda viene configurato anche se si utilizzano solo le sottoscrizioni ad aggiornamento immediato.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 Quando si crea una pubblicazione transazionale a livello di programmazione utilizzando stored procedure di replica, è possibile abilitare sottoscrizioni ad aggiornamento immediato o in coda.  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>Per creare una pubblicazione che supporta sottoscrizioni ad aggiornamento immediato  
  
1.  Se necessario, creare un processo dell'agente di lettura log per il database di pubblicazione.  
  
    -   Se per il database di pubblicazione esiste già un processo dell'agente di lettura log, procedere con il passaggio 2.  
  
    -   Per sapere se un processo dell'agente di lettura log esiste già per un database pubblicato, eseguire [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql) nel database di pubblicazione nel server di pubblicazione. Se il set di risultati è vuoto, sarà necessario creare un processo dell'agente di lettura log.  
  
    -   Nel server di pubblicazione eseguire [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql). Specificare le [!INCLUDE[msCoName](../../../includes/msconame-md.md)] credenziali di Windows utilizzate per l'esecuzione dell' **@job_name** agente **@password**per e. Se l'agente utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per **@publisher_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per **@publisher_login** e **@publisher_password**.  
  
2.  Eseguire [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), specificando il valore **true** per il parametro **@allow_sync_tran**.  
  
3.  Nel server di pubblicazione eseguire [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Specificare il nome della pubblicazione usato nel passaggio 2 **@publication** per e le credenziali di Windows con cui viene eseguito **@job_name** il **@password**agente di snapshot per e. Se l'agente utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per **@publisher_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per **@publisher_login** e **@publisher_password**. Verrà creato un processo dell'agente snapshot per la pubblicazione.  
  
4.  Aggiungere articoli alla pubblicazione. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
5.  Nel Sottoscrittore creare una sottoscrizione aggiornabile per la pubblicazione. Per altre informazioni, vedere [Creazione di una sottoscrizione aggiornabile di una pubblicazione transazionale](../publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>Per creare una pubblicazione che supporta sottoscrizioni ad aggiornamento in coda  
  
1.  Se necessario, creare un processo dell'agente di lettura log per il database di pubblicazione.  
  
    -   Se per il database di pubblicazione esiste già un processo dell'agente di lettura log, procedere con il passaggio 2.  
  
    -   Per sapere se un processo dell'agente di lettura log esiste già per un database pubblicato, eseguire [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql) nel database di pubblicazione nel server di pubblicazione. Se il set di risultati è vuoto, sarà necessario creare un processo dell'agente di lettura log.  
  
    -   Nel server di pubblicazione eseguire [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql). Specificare le credenziali di Windows utilizzate per l'esecuzione dell' **@job_name** agente **@password**per e. Se l'agente utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per **@publisher_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per **@publisher_login** e **@publisher_password**.  
  
2.  Se necessario, creare un processo dell'agente di lettura coda per il server di distribuzione.  
  
    -   Se per il database di distribuzione esiste già un processo dell'agente di lettura coda, procedere con il passaggio 3.  
  
    -   Per sapere se un processo dell'agente di lettura coda esiste già per un database di distribuzione, eseguire [sp_helpqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql) nel database di distribuzione nel server di distribuzione. Se il set di risultati è vuoto, sarà necessario creare un processo dell'agente di lettura coda.  
  
    -   Nel database di distribuzione eseguire [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql). Specificare le credenziali di Windows utilizzate per l'esecuzione dell' **@job_name** agente **@password**per e. Queste credenziali vengono utilizzate quando l'agente di lettura coda si connette al server di pubblicazione e al Sottoscrittore. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](../security/replication-agent-security-model.md).  
  
3.  Eseguire [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), specificando il valore **true** per il parametro **@allow_queued_tran** e il valore **pub wins**, **sub reinit** o **sub wins** per **@conflict_policy**.  
  
4.  Nel server di pubblicazione eseguire [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Specificare il nome della pubblicazione usato nel passaggio 3 **@publication** per e le credenziali di Windows con cui viene eseguito **@snapshot_job_name** il **@password**agente di snapshot per e. Se l'agente utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per **@publisher_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per **@publisher_login** e **@publisher_password**. Verrà creato un processo dell'agente snapshot per la pubblicazione.  
  
5.  Aggiungere articoli alla pubblicazione. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
6.  Nel Sottoscrittore creare una sottoscrizione aggiornabile per la pubblicazione. Per altre informazioni, vedere [Creazione di una sottoscrizione aggiornabile di una pubblicazione transazionale](../publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>Per modificare i criteri per la gestione dei conflitti per una pubblicazione che consente le sottoscrizioni ad aggiornamento in coda  
  
1.  Nel database di pubblicazione nel server di pubblicazione eseguire [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Specificare il valore **conflict_policy** per **@property** e i criteri desiderati per la gestione dei conflitti **pub wins**, **sub reinit**o **sub wins** per **@value**.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 In questo esempio viene creata una pubblicazione che supporta le sottoscrizioni pull ad aggiornamento immediato e in coda.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubupdate.sql#sp_createtranupdatingpub)]  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di risoluzione dei conflitti per l'aggiornamento in coda &#40;SQL Server Management Studio&#41;](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Tipi di pubblicazioni per la replica transazionale](../transactional/transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Create a Publication](create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Utilizzo di sqlcmd con variabili di scripting](../../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
