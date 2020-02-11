---
title: Creare una sottoscrizione pull | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8868957d7c479de3a51a599deed42c34d6676eb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721593"
---
# <a name="create-a-pull-subscription"></a>Creazione di una sottoscrizione pull
  In questo argomento viene descritto come creare una sottoscrizione pull in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 L'impostazione della sottoscrizione pull per la replica P2P è possibile dallo script, ma non è disponibile tramite la procedura guidata.  
  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Creare una sottoscrizione pull nel server di pubblicazione o nel Sottoscrittore tramite la Creazione guidata sottoscrizione. Attenersi alle indicazioni presenti nelle pagine della procedura guidata per:  
  
-   Specificare il server di pubblicazione e la pubblicazione.  
  
-   Selezionare la posizione di esecuzione degli agenti di replica. Per una sottoscrizione pull, selezionare **Esegui ogni agente nel relativo Sottoscrittore (sottoscrizioni pull)** nella pagina **Posizione in cui eseguire l'agente di distribuzione** o nella pagina **Posizione in cui eseguire l'agente di merge** , a seconda del tipo di pubblicazione.  
  
-   Specificare i Sottoscrittori e i database di sottoscrizione.  
  
-   Specificare gli accessi e le password utilizzati per le connessioni stabilite dagli agenti di replica:  
  
    -   Per effettuare sottoscrizioni di pubblicazioni snapshot e transazionali, specificare le credenziali nella pagina **Sicurezza agente di distribuzione** .  
  
    -   Per effettuare sottoscrizioni di pubblicazioni di tipo merge, specificare le credenziali nella pagina **Sicurezza agente di merge** .  
  
     Per informazioni sulle autorizzazioni richieste per ogni agente, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
-   Specificare una pianificazione della sincronizzazione e definire quando il Sottoscrittore dovrà essere inizializzato.  
  
-   Specificare le opzioni aggiuntive per le pubblicazioni di tipo merge: il tipo di sottoscrizione, i valori dei filtri con parametri e le informazioni per la sincronizzazione tramite HTTPS se la pubblicazione è abilitata per la sincronizzazione Web.  
  
-   Specificare le opzioni aggiuntive per le pubblicazioni transazionali che consentono l'aggiornamento delle sottoscrizioni, indicando se si desidera che i Sottoscrittori eseguano immediatamente il commit delle modifiche nel server di pubblicazione o se devono aggiungerle a una coda e le credenziali utilizzate per stabilire una connessione dal Sottoscrittore al server di pubblicazione.  
  
-   Facoltativamente, creare lo script della sottoscrizione.  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>Per creare una sottoscrizione pull dal server di pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera creare una o più sottoscrizioni e scegliere **Nuove sottoscrizioni**.  
  
4.  Completare i passaggi della Creazione guidata nuova sottoscrizione.  
  
#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>Per creare una sottoscrizione pull dal Sottoscrittore  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** .  
  
3.  Fare clic col pulsante destro del mouse sulla cartella **Sottoscrizioni locali** e quindi scegliere **Nuove sottoscrizioni**.  
  
4.  Nella pagina **Pubblicazione** della Creazione guidata nuova sottoscrizione selezionare **\<Trova server di pubblicazione SQL Server** o **\<Trova server di pubblicazione Oracle>** nell'elenco a discesa **Server di pubblicazione**.  
  
5.  Connettersi al server di pubblicazione nella finestra di dialogo **Connetti a server** .  
  
6.  Selezionare una pubblicazione nella pagina **Pubblicazione** .  
  
7.  Completare i passaggi della Creazione guidata nuova sottoscrizione.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 È possibile creare sottoscrizioni pull a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipenderanno dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per creare una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Nel server di pubblicazione eseguire [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) per verificare che la pubblicazione supporti le sottoscrizioni pull.  
  
    -   Se il valore di **allow_pull** nel set di risultati è **1**, la pubblicazione supporta le sottoscrizioni pull.  
  
    -   Se il valore di **allow_pull** è **0**, eseguire [SP_CHANGEPUBLICATION &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), specificando **allow_pull** **@property** per `true` e **@value**per.  
  
2.  Nel Sottoscrittore eseguire [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Specificare **@publisher** e **@publication**. Per informazioni sull'aggiornamento delle sottoscrizioni, vedere [Creazione di una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
3.  Nel Sottoscrittore eseguire [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Specificare le opzioni seguenti:  
  
    -   Parametri **@publisher**, **@publisher_db**e **@publication** .  
  
    -   Le [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenziali di Windows con cui viene eseguito il agente di distribuzione nel Sottoscrittore per **@job_login** e. **@job_password**  
  
        > [!NOTE]  
        >  Le connessioni effettuate con l'autenticazione integrata di Windows utilizzano sempre le credenziali **@job_login** di **@job_password**Windows specificate da e. L'agente di distribuzione attiva sempre la connessione locale al Sottoscrittore utilizzando l'autenticazione integrata di Windows. Per impostazione predefinita, l'agente si connetterà al server di distribuzione con l'autenticazione integrata di Windows.  
  
    -   (Facoltativo) Impostare il valore **0** per **@distributor_security_mode** e specificare le informazioni di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei parametri **@distributor_login** e **@distributor_password**, se è necessario utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione al server di distribuzione.  
  
    -   Specificare una pianificazione per il processo dell'agente di distribuzione da eseguire per la sottoscrizione. Per altre informazioni, vedere [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
4.  Nel server di pubblicazione eseguire [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) per registrare la sottoscrizione pull. Specificare **@publication**, **@subscriber**e **@destination_db**. Specificare il valore **pull** per **@subscription_type**.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Per creare una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) per verificare che la pubblicazione supporti le sottoscrizioni pull.  
  
    -   Se il valore di **allow_pull** nel set di risultati è **1**, la pubblicazione supporta le sottoscrizioni pull.  
  
    -   Se il valore di **allow_pull** è **0**, eseguire [SP_CHANGEMERGEPUBLICATION &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), specificando **allow_pull** **@property** per `true` e **@value**per.  
  
2.  Nel Sottoscrittore eseguire [sp_addmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Specificare **@publisher**, **@publisher_db** **@publication**, e i parametri seguenti:  
  
    -   **@subscriber_type**-specificare **local** per una sottoscrizione client e **Global** per una sottoscrizione server.  
  
    -   **@subscription_priority**-Specificare una priorità per la sottoscrizione (da**0,00** a **99,99**). Questo parametro è obbligatorio solo per una sottoscrizione server.  
  
         Per altre informazioni, vedere [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  Nel Sottoscrittore eseguire [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Specificare i parametri seguenti:  
  
    -   **@publisher**, **@publisher_db**e **@publication**.  
  
    -   Le credenziali di Windows con cui viene eseguito il agente di merge nel Sottoscrittore per **@job_login** e. **@job_password**  
  
        > [!NOTE]  
        >  Le connessioni effettuate con l'autenticazione integrata di Windows utilizzano sempre le credenziali **@job_login** di **@job_password**Windows specificate da e. L'agente di merge attiva sempre la connessione locale al Sottoscrittore utilizzando l'autenticazione integrata di Windows. Per impostazione predefinita, l'agente si connetterà al database di distribuzione e al server di pubblicazione con l'autenticazione integrata di Windows.  
  
    -   (Facoltativo) Impostare il valore **0** per **@distributor_security_mode** e specificare le informazioni di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei parametri **@distributor_login** e **@distributor_password**, se è necessario utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione al server di distribuzione.  
  
    -   (Facoltativo) Impostare il valore **0** per **@publisher_security_mode** e specificare le informazioni di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei parametri **@publisher_login** e **@publisher_password**, se è necessario utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione al server di pubblicazione.  
  
    -   Una pianificazione per il processo dell'agente di merge per la sottoscrizione. Per altre informazioni, vedere [Creazione di una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
4.  Nel server di pubblicazione eseguire [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Specificare **@publication**, **@subscriber** **@subscriber_db**, e il valore **pull** per **@subscription_type**. In questo modo la sottoscrizione pull viene registrata.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 Nell'esempio seguente viene creata una sottoscrizione pull di una pubblicazione transazionale. Il primo batch viene eseguito nel Sottoscrittore e il secondo batch viene eseguito nel server di pubblicazione. I valori per l'account di accesso e la relativa password vengono specificati in fase di esecuzione tramite variabili di scripting sqlcmd.  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 Nell'esempio seguente viene creata una sottoscrizione pull di una pubblicazione di tipo merge. Il primo batch viene eseguito nel Sottoscrittore e il secondo batch viene eseguito nel server di pubblicazione. I valori di account di accesso e password vengono forniti in fase di esecuzione tramite variabili di scripting **SQLCMD** .  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 Le classi RMO utilizzate per la creazione di una sottoscrizione pull dipendono dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per creare una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione sia al Sottoscrittore che al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication> utilizzando la connessione al server di pubblicazione creata nel passaggio 1. Specificare <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, le proprietà specificate nel passaggio 2 non sono corrette oppure la pubblicazione non esiste nel server.  
  
4.  Eseguire un'operazione con AND logico bit per bit (`&` in Visual C# e `And` in Visual Basic) tra la proprietà <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Se il risultato è <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, impostare <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> sul risultato di un'operazione con OR logico bit per bit (`|` in Visual C# e `Or` in Visual Basic) tra <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Chiamare quindi <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per abilitare le sottoscrizioni pull.  
  
5.  Se il database di sottoscrizione non esiste, crearlo utilizzando la classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Per ulteriori informazioni, vedere [creazione, modifica e rimozione di database](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription>.  
  
7.  Impostare le proprietà seguenti per la sottoscrizione:  
  
    -   La connessione <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al Sottoscrittore creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   Nome del database di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome della pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   I campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> per fornire le credenziali per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con il quale verrà eseguito l'agente di distribuzione nel Sottoscrittore. Questo account viene utilizzato per attivare connessioni locali al Sottoscrittore e stabilire connessioni remote con l'autenticazione di Windows.  
  
        > [!NOTE]  
        >  Non è obbligatorio impostare <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> quando la sottoscrizione viene creata da un membro del ruolo predefinito del server `sysadmin`, tuttavia si tratta di un'impostazione consigliata. In questo caso l'agente rappresenterà l'account di SQL Server Agent. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
    -   (Facoltativo) Impostare il valore `true` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> per creare un processo dell'agente, utilizzato per sincronizzare la sottoscrizione. Se si specifica `false` (impostazione predefinita), la sottoscrizione può essere sincronizzata solo a livello di programmazione ed è necessario specificare proprietà aggiuntive di <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> per l'accesso all'oggetto dalla proprietà <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A>. Per altre informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
        > [!NOTE]  
        >  SQL Server Agent non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Se si specifica il valore `true` per Sottoscrittori SQL Server Express, il processo dell'agente non viene creato. Tuttavia, i metadati importanti correlati alla sottoscrizione vengono archiviati nel Sottoscrittore.  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al database di distribuzione.  
  
8.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> .  
  
9. Utilizzando l'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication> creata nel passaggio 2, chiamare il metodo <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> per registrare la sottoscrizione pull nel server di pubblicazione. Se la registrazione esiste già, viene generata un'eccezione.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Per creare una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Creare una connessione sia al Sottoscrittore che al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> utilizzando la connessione al server di pubblicazione creata nel passaggio 1. Specificare <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, le proprietà specificate nel passaggio 2 non sono corrette oppure la pubblicazione non esiste nel server.  
  
4.  Eseguire un'operazione con AND logico bit per bit (`&` in Visual C# e `And` in Visual Basic) tra la proprietà <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Se il risultato è <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, impostare <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> sul risultato di un'operazione con OR logico bit per bit (`|` in Visual C# e `Or` in Visual Basic) tra <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Chiamare quindi <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per abilitare le sottoscrizioni pull.  
  
5.  Se il database di sottoscrizione non esiste, crearlo utilizzando la classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Per ulteriori informazioni, vedere [creazione, modifica e rimozione di database](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription>.  
  
7.  Impostare le proprietà seguenti per la sottoscrizione:  
  
    -   La connessione <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al Sottoscrittore creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   Nome del database di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome della pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   I campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> per fornire le credenziali per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con il quale verrà eseguito l'agente di merge nel Sottoscrittore. Questo account viene utilizzato per attivare connessioni locali al Sottoscrittore e stabilire connessioni remote con l'autenticazione di Windows.  
  
        > [!NOTE]  
        >  Non è obbligatorio impostare <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> quando la sottoscrizione viene creata da un membro del ruolo predefinito del server `sysadmin`, tuttavia si tratta di un'impostazione consigliata. In questo caso l'agente rappresenterà l'account di SQL Server Agent. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
    -   (Facoltativo) Impostare il valore `true` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> per creare un processo dell'agente, utilizzato per sincronizzare la sottoscrizione. Se si specifica `false` (impostazione predefinita), la sottoscrizione può essere sincronizzata solo a livello di programmazione ed è necessario specificare proprietà aggiuntive di <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> per l'accesso all'oggetto dalla proprietà <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A>. Per altre informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al database di distribuzione.  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione.  
  
8.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> .  
  
9. Utilizzando l'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> creata nel passaggio 2, chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> per registrare la sottoscrizione pull nel server di pubblicazione. Se la registrazione esiste già, viene generata un'eccezione.  
  
###  <a name="PShellExample"></a> Esempio (RMO)  
 In questo esempio viene creata una sottoscrizione pull di una pubblicazione transazionale. Le credenziali dell'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzate per creare il processo dell'agente di distribuzione vengono passate in fase di esecuzione.  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 In questo esempio viene creata una sottoscrizione pull di una pubblicazione di tipo merge. Le credenziali dell'account di Windows utilizzate per creare il processo dell'agente di merge vengono passate in fase di esecuzione.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 In questo esempio viene creata una sottoscrizione pull di una pubblicazione di tipo merge senza creare un processo dell'agente associato e i metadati di sottoscrizione in [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql). Le credenziali dell'account di Windows utilizzate per creare il processo dell'agente di merge vengono passate in fase di esecuzione.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 In questo esempio viene creata una sottoscrizione pull di una pubblicazione di tipo merge che può essere sincronizzata su Internet con la sincronizzazione Web. Le credenziali dell'account di Windows utilizzate per creare il processo dell'agente di merge vengono passate in fase di esecuzione. Per altre informazioni, vedere [Configure Web Synchronization](configure-web-synchronization.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](view-and-modify-pull-subscription-properties.md)   
 [Configurare la sincronizzazione Web](configure-web-synchronization.md)   
 [Sottoscrivere le pubblicazioni](subscribe-to-publications.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)  
  
  
