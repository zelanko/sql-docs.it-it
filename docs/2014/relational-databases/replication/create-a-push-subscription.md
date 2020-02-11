---
title: Creare una sottoscrizione push | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b571bec94c873b830654126e39d75d554599e5fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721733"
---
# <a name="create-a-push-subscription"></a>Creazione di una sottoscrizione push
  In questo argomento viene descritto come creare una sottoscrizione push in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects). Per informazioni sulla creazione di una sottoscrizione push per un[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sottoscrittore non, vedere [creare una sottoscrizione per un Sottoscrittore non SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Creare una sottoscrizione push nel server di pubblicazione o nel Sottoscrittore utilizzando la Creazione guidata nuova sottoscrizione. Attenersi alle indicazioni presenti nelle pagine della procedura guidata per:  
  
-   Specificare il server di pubblicazione e la pubblicazione.  
  
-   Selezionare la posizione di esecuzione degli agenti di replica. Per una sottoscrizione push, selezionare **Esegui tutti gli agenti nel server di distribuzione (sottoscrizioni push)** nella pagina **Posizione in cui eseguire l'agente di distribuzione** o nella pagina **Posizione in cui eseguire l'agente di merge** , in base al tipo di pubblicazione.  
  
-   Specificare i Sottoscrittori e i database di sottoscrizione.  
  
-   Specificare gli accessi e le password utilizzati per le connessioni stabilite dagli agenti di replica:  
  
    -   Per effettuare sottoscrizioni di pubblicazioni snapshot e transazionali, specificare le credenziali nella pagina **Sicurezza agente di distribuzione** .  
  
    -   Per effettuare sottoscrizioni di pubblicazioni di tipo merge, specificare le credenziali nella pagina **Sicurezza agente di merge** .  
  
     Per informazioni sulle autorizzazioni richieste per ogni agente, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
-   Specificare una pianificazione della sincronizzazione e definire quando il Sottoscrittore dovrà essere inizializzato.  
  
-   Specificare le opzioni aggiuntive per le pubblicazioni di tipo merge, ovvero tipo di sottoscrizione e valori per il filtro con parametri.  
  
-   Specificare le opzioni aggiuntive per le pubblicazioni transazionali che consentono l'aggiornamento delle sottoscrizioni, indicando se si desidera che i Sottoscrittori eseguano immediatamente il commit delle modifiche nel server di pubblicazione o se devono aggiungerle a una coda e le credenziali utilizzate per stabilire una connessione dal Sottoscrittore al server di pubblicazione.  
  
-   Facoltativamente, creare lo script della sottoscrizione.  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>Per creare una sottoscrizione push dal server di pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera creare una o più sottoscrizioni e scegliere **Nuove sottoscrizioni**.  
  
4.  Completare i passaggi della Creazione guidata nuova sottoscrizione.  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>Per creare una sottoscrizione push dal Sottoscrittore  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** .  
  
3.  Fare clic col pulsante destro del mouse sulla cartella **Sottoscrizioni locali** e quindi scegliere **Nuove sottoscrizioni**.  
  
4.  Nella pagina **Pubblicazione** della Creazione guidata nuova sottoscrizione selezionare **\<Trova server di pubblicazione SQL Server** o **\<Trova server di pubblicazione Oracle>** nell'elenco a discesa **Server di pubblicazione**.  
  
5.  Connettersi al server di pubblicazione nella finestra di dialogo **Connetti a server** .  
  
6.  Selezionare una pubblicazione nella pagina **Pubblicazione** .  
  
7.  Completare i passaggi della Creazione guidata nuova sottoscrizione.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 Le sottoscrizioni push possono essere create a livello di programmazione utilizzando stored procedure di replica. Le stored procedure utilizzate dipenderanno dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per creare una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)per verificare che la pubblicazione supporti le sottoscrizioni push.  
  
    -   Se il valore di **allow_push** è **1**, le sottoscrizioni push sono supportate.  
  
    -   Se il valore di **allow_push** è **0**, eseguire [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), specificando **allow_push** **@property** per `true` e **@value**per.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Specificare **@publication**, **@subscriber** e **@destination_db**. Specificare il valore **push** per **@subscription_type**. Per informazioni sull'aggiornamento delle sottoscrizioni, vedere [creare una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md) .  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Specificare le opzioni seguenti:  
  
    -   Parametri **@subscriber**, **@subscriber_db**e **@publication** .  
  
    -   Le [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenziali di Windows con cui viene eseguito il agente di distribuzione nel server **@job_login** di **@job_password**distribuzione per e.  
  
        > [!NOTE]  
        >  Le connessioni effettuate con l'autenticazione integrata di Windows utilizzano sempre le credenziali **@job_login** di **@job_password**Windows specificate da e. L'agente di distribuzione esegue sempre la connessione locale al server di distribuzione utilizzando l'autenticazione integrata di Windows. Per impostazione predefinita, l'agente si connette al Sottoscrittore utilizzando l'autenticazione integrata di Windows.  
  
    -   (Facoltativo) Il valore **0** per **@subscriber_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per **@subscriber_login** e **@subscriber_password**. Specificare questi parametri se è necessario utilizzare l'autenticazione di SQL Server per la connessione al Sottoscrittore.  
  
    -   Specificare una pianificazione per il processo dell'agente di distribuzione da eseguire per la sottoscrizione. Per altre informazioni, vedere [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Quando si crea una sottoscrizione push in un server di pubblicazione per un server di distribuzione remoto, i valori specificati per tutti i parametri, compresi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>Per creare una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)per verificare che la pubblicazione supporti le sottoscrizioni push.  
  
    -   Se il valore di **allow_push** è **1**, la pubblicazione supporta le sottoscrizioni push.  
  
    -   Se il valore di **allow_push** non è **1**, eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), specificando **allow_push** **@property** per `true` e **@value**per.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)specificando i parametri seguenti:  
  
    -   **@publication**. Nome della pubblicazione.  
  
    -   **@subscriber_type**. Per una sottoscrizione client specificare **local** e per una sottoscrizione server specificare **global**.  
  
    -   **@subscription_priority**. Per una sottoscrizione server, specificare una priorità per la pubblicazione utilizzando un valore compreso tra**0.00** e **99.99**.  
  
         Per altre informazioni, vedere [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql). Specificare le opzioni seguenti:  
  
    -   Parametri **@subscriber**, **@subscriber_db**e **@publication** .  
  
    -   Le credenziali di Windows con cui viene eseguito il agente di merge nel server **@job_login** di **@job_password**distribuzione per e.  
  
        > [!NOTE]  
        >  Le connessioni effettuate con l'autenticazione integrata di Windows utilizzano sempre le credenziali **@job_login** di **@job_password**Windows specificate da e. L'agente di merge esegue sempre la connessione locale al server di distribuzione utilizzando l'autenticazione integrata di Windows. Per impostazione predefinita, l'agente si connette al Sottoscrittore utilizzando l'autenticazione integrata di Windows.  
  
    -   (Facoltativo) Il valore **0** per **@subscriber_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per **@subscriber_login** e **@subscriber_password**. Specificare questi parametri se è necessario utilizzare l'autenticazione di SQL Server per la connessione al Sottoscrittore.  
  
    -   (Facoltativo) Il valore **0** per **@publisher_security_mode** e le informazioni sull'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per **@publisher_login** e **@publisher_password**. Specificare questi valori se è necessario utilizzare l'autenticazione di SQL Server per la connessione al server di pubblicazione.  
  
    -   Una pianificazione per il processo dell'agente di merge per la sottoscrizione. Per altre informazioni, vedere [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Quando si crea una sottoscrizione push in un server di pubblicazione per un server di distribuzione remoto, i valori specificati per tutti i parametri, compresi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 Nell'esempio seguente viene creata una sottoscrizione push a una pubblicazione transazionale. I valori dell'account di accesso e della password vengono forniti in fase di esecuzione tramite le variabili di scripting di **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpushsub.sql#sp_addtranpushsubscription_agent)]  
  
 Nell'esempio seguente viene creata una sottoscrizione push a una pubblicazione di tipo merge. I valori dell'account di accesso e della password vengono forniti in fase di esecuzione tramite le variabili di scripting di **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepushsub.sql#sp_addmergepushsubscriptionagent)]  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 È possibile creare sottoscrizioni push a livello di programmazione tramite gli oggetti RMO (Replication Management Objects). Le classi RMO utilizzate per la creazione di una sottoscrizione push dipendono dal tipo di pubblicazione per cui viene creata la sottoscrizione.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali, utilizzare i [servizi di crittografia](https://go.microsoft.com/fwlink/?LinkId=34733) offerti da [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per creare una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication> utilizzando la connessione al server di pubblicazione creata nel passaggio 1. Specificare <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, le proprietà specificate nel passaggio 2 non sono corrette oppure la pubblicazione non esiste nel server.  
  
4.  Eseguire un'operazione con AND logico bit per bit (`&` in Visual C# e `And` in Visual Basic) tra la proprietà <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se il risultato è <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, impostare <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> sul risultato di un'operazione con OR logico bit per bit (`|` in Visual C# e `Or` in Visual Basic) tra <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Chiamare quindi <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per abilitare le sottoscrizioni push.  
  
5.  Se il database di sottoscrizione non esiste, crearlo utilizzando la classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Per ulteriori informazioni, vedere [creazione, modifica e rimozione di database](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
7.  Impostare le proprietà seguenti per la sottoscrizione:  
  
    -   La connessione <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al server di pubblicazione creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome del Sottoscrittore per <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome del database di pubblicazione per <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome della pubblicazione per <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   I campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> di <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> per fornire le credenziali per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con il quale verrà eseguito l'agente di distribuzione nel server di distribuzione. Questo account viene utilizzato per attivare connessioni locali al server di distribuzione e stabilire connessioni remote con l'autenticazione di Windows.  
  
        > [!NOTE]  
        >  Non è obbligatorio impostare <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> quando la sottoscrizione viene creata da un membro del ruolo predefinito del server `sysadmin`, tuttavia si tratta di un'impostazione consigliata. In questo caso l'agente rappresenterà l'account di SQL Server Agent. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
    -   (Facoltativo) Impostare il valore `true` (impostazione predefinita) per <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> per creare un processo dell'agente, utilizzato per sincronizzare la sottoscrizione. Se si specifica `false`, la sottoscrizione può essere sincronizzata solo a livello di programmazione.  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al Sottoscrittore.  
  
8.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> .  
  
    > [!IMPORTANT]  
    >  Quando si crea una sottoscrizione push in un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutte le proprietà, compresa <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>Per creare una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> utilizzando la connessione al server di pubblicazione creata nel passaggio 1. Specificare <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, le proprietà specificate nel passaggio 2 non sono corrette oppure la pubblicazione non esiste nel server.  
  
4.  Eseguire un'operazione con AND logico bit per bit (`&` in Visual C# e `And` in Visual Basic) tra la proprietà <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Se il risultato è <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, impostare <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> sul risultato di un'operazione con OR logico bit per bit (`|` in Visual C# e `Or` in Visual Basic) tra <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> e <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Chiamare quindi <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per abilitare le sottoscrizioni push.  
  
5.  Se il database di sottoscrizione non esiste, crearlo utilizzando la classe <xref:Microsoft.SqlServer.Management.Smo.Database> . Per ulteriori informazioni, vedere [creazione, modifica e rimozione di database](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
7.  Impostare le proprietà seguenti per la sottoscrizione:  
  
    -   La connessione <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al server di pubblicazione creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nome del Sottoscrittore per <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nome del database di pubblicazione per <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nome della pubblicazione per <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   I campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o<xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> di <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> per fornire le credenziali per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con il quale verrà eseguito l'agente di merge nel server di distribuzione. Questo account viene utilizzato per attivare connessioni locali al server di distribuzione e stabilire connessioni remote con l'autenticazione di Windows.  
  
        > [!NOTE]  
        >  Non è obbligatorio impostare <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> quando la sottoscrizione viene creata da un membro del ruolo predefinito del server `sysadmin`, tuttavia si tratta di un'impostazione consigliata. In questo caso l'agente rappresenterà l'account di SQL Server Agent. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
    -   (Facoltativo) Impostare il valore `true` (impostazione predefinita) per <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> per creare un processo dell'agente, utilizzato per sincronizzare la sottoscrizione. Se si specifica `false`, la sottoscrizione può essere sincronizzata solo a livello di programmazione.  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al Sottoscrittore.  
  
    -   (Facoltativo) Impostare i campi <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> quando si utilizza l'autenticazione di SQL Server per la connessione al server di pubblicazione.  
  
8.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> .  
  
    > [!IMPORTANT]  
    >  Quando si crea una sottoscrizione push in un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutte le proprietà, compresa <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
###  <a name="PShellExample"></a> Esempi (RMO)  
 In questo esempio viene creata una nuova sottoscrizione push di una pubblicazione transazionale. Le credenziali dell'account di Windows utilizzate per eseguire il processo dell'agente di distribuzione vengono passate in fase di esecuzione.  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 In questo esempio viene creata una nuova sottoscrizione push di una pubblicazione di tipo merge. Le credenziali dell'account di Windows utilizzate per eseguire il processo dell'agente di merge vengono passate in fase di esecuzione.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](view-and-modify-push-subscription-properties.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Sincronizzare una sottoscrizione push](synchronize-a-push-subscription.md)   
 [Sottoscrivere le pubblicazioni](subscribe-to-publications.md)   
 [Utilizzo di sqlcmd con variabili di scripting](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
