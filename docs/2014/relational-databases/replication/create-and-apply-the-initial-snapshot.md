---
title: Creare e applicare lo snapshot iniziale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a69d4805a21cfbd83bd9a8d79b5150460d4977be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721683"
---
# <a name="create-and-apply-the-initial-snapshot"></a>Creazione e applicazione dello snapshot iniziale
  In questo argomento viene descritto come creare e applicare lo snapshot iniziale in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects). Per le pubblicazioni di tipo merge che utilizzano filtri con parametri è necessario uno snapshot a due parti. Per altre informazioni, vedere [Creazione di uno snapshot per una pubblicazione di tipo merge con filtri con parametri](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 **Contenuto dell'articolo**  
  
-   **Per creare e applicare lo snapshot iniziale, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Per impostazione predefinita, se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è in esecuzione, l'agente snapshot genera uno snapshot subito dopo la creazione di una pubblicazione mediante la Creazione guidata nuova pubblicazione. Sempre per impostazione predefinita, tale snapshot viene quindi applicato dall'agente di distribuzione (per la replica snapshot e transazionale) o dall'agente di merge (per le sottoscrizioni di tipo merge) per tutte le sottoscrizioni. È anche possibile generare uno snapshot utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md).  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>Per creare uno snapshot in Management Studio  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera creare uno snapshot, quindi scegliere **Visualizza stato agente snapshot**.  
  
4.  Nella finestra di dialogo **Visualizza stato agente snapshot - \<Pubblicazione>** fare clic su **Avvia**.  
  
 Al termine della generazione dello snapshot, verrà visualizzato un messaggio del tipo "[100%] Generato uno snapshot di 17 articoli."  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>Per creare uno snapshot in Monitoraggio replica  
  
1.  In Monitoraggio replica espandere un gruppo di server di pubblicazione nel riquadro di sinistra e quindi espandere un server di pubblicazione.  
  
2.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera generare uno snapshot, quindi scegliere **Genera snapshot**.  
  
3.  Per visualizzare lo stato del agente di snapshot, fare clic sulla scheda **agenti** . Per informazioni più dettagliate, fare clic con il pulsante destro del mouse sul agente di snapshot nella griglia e quindi scegliere **Visualizza dettagli**.  
  
#### <a name="to-apply-a-snapshot"></a>Per applicare uno snapshot  
  
1.  Al termine della generazione, lo snapshot verrà applicato mediante la sincronizzazione della sottoscrizione con l'agente di distribuzione o l'agente di merge:  
  
    -   Se l'agente è impostato per l'esecuzione continua, ovvero l'impostazione predefinita per la replica transazionale, lo snapshot verrà applicato automaticamente al termine della generazione.  
  
    -   Se è invece impostato per l'esecuzione in base a una pianificazione, lo snapshot verrà applicato alla successiva esecuzione pianificata dell'agente.  
  
    -   Se l'agente è impostato per l'esecuzione su richiesta, lo snapshot verrà applicato alla successiva esecuzione dell'agente.  
  
     Per ulteriori informazioni sulla sincronizzazione delle sottoscrizioni, vedere [Synchronize a Push Subscription](synchronize-a-push-subscription.md) e [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Gli snapshot iniziali possono essere creati a livello di programmazione creando ed eseguendo un processo dell'agente snapshot o eseguendo il file eseguibile dell'agente snapshot da un file batch. Dopo la generazione, lo snapshot iniziale viene trasferito e applicato al Sottoscrittore la prima volta che la sottoscrizione viene sincronizzata. Se si esegue l'agente snapshot da un prompt dei comandi o un file batch, sarà necessario rieseguirlo ogni volta che lo snapshot esistente diventa non valido.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>Per creare ed eseguire un processo dell'agente snapshot per generare lo snapshot iniziale  
  
1.  Creare una pubblicazione snapshot, transazionale o di tipo merge. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di una pubblicazione](publish/create-a-publication.md).  
  
2.  Eseguire [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql). Specificare **@publication** e i parametri seguenti:  
  
    -   **@job_login, che specifica** le credenziali dell'autenticazione di Windows con cui l'agente snapshot viene eseguito nel database di distribuzione.  
  
    -   **@job_password**, che corrisponde alla password per le credenziali di Windows specificate.  
  
    -   (Facoltativo) Valore **0** per **@publisher_security_mode** se l'agente utilizzerà l'autenticazione di SQL Server per la connessione al server di pubblicazione. In questo caso, è necessario specificare anche le informazioni di accesso per l' **@publisher_login** autenticazione **@publisher_password**SQL Server per e.  
  
    -   (Facoltativo) Pianificazione della sincronizzazione per il processo dell'agente snapshot. Per altre informazioni, vedere [specificare le pianificazioni della sincronizzazione](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
3.  Aggiungere articoli alla pubblicazione. Per altre informazioni, vedere [definire un articolo](publish/define-an-article.md).  
  
4.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_startpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql), specificando il valore **@publication** dal passaggio 1.  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>Per eseguire l'agente snapshot per generare lo snapshot iniziale  
  
1.  Creare una pubblicazione snapshot, transazionale o di tipo merge. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di una pubblicazione](publish/create-a-publication.md).  
  
2.  Aggiungere articoli alla pubblicazione. Per altre informazioni, vedere [definire un articolo](publish/define-an-article.md).  
  
3.  Dal prompt dei comandi o in un file batch avviare l' [Agente merge repliche](agents/replication-snapshot-agent.md) eseguendo **snapshot.exe**con gli argomenti della riga di comando seguenti:  
  
    -   **-Pubblicazione**  
  
    -   **-Editore**  
  
    -   **-Database di distribuzione**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     Se si usano l'autenticazione di SQL Server, è inoltre necessario specificare gli argomenti seguenti:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene illustrato come creare una pubblicazione transazionale e aggiungere un processo dell'agente snapshot per la nuova pubblicazione (utilizzando le variabili di scripting **SQLCMD** ). Viene inoltre avviato il processo.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubinitialsnapshot.sql#sp_trangenerate_snapshot)]  
  
 In questo esempio viene creata una pubblicazione di tipo merge e viene aggiunto un processo dell'agente snapshot (utilizzando le variabili **sqlcmd** ) per la pubblicazione. Viene inoltre avviato il processo.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubinitialsnapshot.sql#sp_mergegenerate_snapshot)]  
  
 Con gli argomenti della riga di comando seguenti l'agente snapshot viene avviato per generare lo snapshot per una pubblicazione di tipo merge.  
  
> [!NOTE]  
>  Le interruzioni di riga sono state aggiunte per agevolare la lettura. I comandi in un file batch devono essere inseriti in un'unica riga.  
  
 [!code-sql[HowTo#startmergesnapshot_10](../../snippets/tsql/SQL15/replication/howto/tsql/createmergesnapshot_10.bat)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 L'agente snapshot genera gli snapshot al termine della creazione di una pubblicazione. È possibile generare questi snapshot a livello di programmazione tramite gli oggetti RMO (Replication Management Objects) e l'accesso diretto tramite codice gestito alle funzionalità dell'agente di replica. Gli oggetti utilizzati dipendono dal tipo di replica. L'agente snapshot può essere avviato in modo sincrono tramite l'oggetto <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> o in modo asincrono tramite il processo dell'agente. Dopo la generazione, lo snapshot iniziale viene trasferito e applicato al Sottoscrittore la prima volta che la sottoscrizione viene sincronizzata. È necessario rieseguire l'agente ogni volta che lo snapshot esistente non contiene più dati validi e aggiornati. Per altre informazioni, vedere [Gestire le pubblicazioni](publish/maintain-publications.md).  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali, utilizzare i [servizi di crittografia](https://go.microsoft.com/fwlink/?LinkId=34733) forniti da [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>Per generare lo snapshot iniziale per una pubblicazione snapshot o transazionale avviando il processo dell'agente snapshot (modo asincrono)  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication>. Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per caricare le proprietà rimanenti dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono state definite in modo non corretto nel passaggio 2 oppure la pubblicazione non esiste.  
  
4.  Se il valore di <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> è `false`, chiamare <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> per creare il processo dell'agente snapshot per questa pubblicazione.  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> per avviare il processo dell'agente che genera lo snapshot per la pubblicazione.  
  
6.  (Facoltativo) Quando il valore di <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> è `true`, lo snapshot è disponibile per i Sottoscrittori.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>Per generare lo snapshot iniziale per una pubblicazione snapshot o transazionale eseguendo il processo dell'agente snapshot (modo sincrono)  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e impostare le seguenti proprietà obbligatorie:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> : nome del server di pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> : nome del database di pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> : nome della pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> : nome del server di distribuzione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> : valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> per utilizzare l'autenticazione di Windows per le connessioni al server di pubblicazione o valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valori relativi a <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni al server di pubblicazione. L'autenticazione di Windows è la scelta consigliata.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> : valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> per utilizzare l'autenticazione di Windows per le connessioni al server di distribuzione o valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valori relativi a <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni al server di distribuzione. L'autenticazione di Windows è la scelta consigliata.  
  
2.  Impostare il valore <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> o <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> per <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>Per generare lo snapshot iniziale per una pubblicazione di tipo merge avviando il processo dell'agente snapshot (modo asincrono)  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication>. Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per caricare le proprietà rimanenti dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono state definite in modo non corretto nel passaggio 2 oppure la pubblicazione non esiste.  
  
4.  Se il valore di <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> è `false`, chiamare <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> per creare il processo dell'agente snapshot per questa pubblicazione.  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> per avviare il processo dell'agente che genera lo snapshot per la pubblicazione.  
  
6.  (Facoltativo) Quando il valore di <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> è `true`, lo snapshot è disponibile per i Sottoscrittori.  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>Per generare lo snapshot iniziale per una pubblicazione di tipo merge eseguendo il processo dell'agente snapshot (modo sincrono)  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> e impostare le seguenti proprietà obbligatorie:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> : nome del server di pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> : nome del database di pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> : nome della pubblicazione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> : nome del server di distribuzione  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> : valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> per utilizzare l'autenticazione di Windows per le connessioni al server di pubblicazione o valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valori relativi a <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni al server di pubblicazione. L'autenticazione di Windows è la scelta consigliata.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> : valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> per utilizzare l'autenticazione di Windows per le connessioni al server di distribuzione o valore <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> e valori relativi a <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni al server di distribuzione. L'autenticazione di Windows è la scelta consigliata.  
  
2.  Impostare un valore di <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> per <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Esempi (RMO)  
 In questo esempio viene eseguito l'agente snapshot in modo sincrono per generare lo snapshot iniziale per una pubblicazione transazionale.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 In questo esempio viene avviato l'agente snapshot in modo asincrono per generare lo snapshot iniziale per una pubblicazione transazionale.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Creare una sottoscrizione push](create-a-push-subscription.md)   
 [Specificare le pianificazioni della sincronizzazione](specify-synchronization-schedules.md)   
 [Creare e applicare lo snapshot](create-and-apply-the-snapshot.md)   
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Concetti di Replication Management Objects](concepts/replication-management-objects-concepts.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)   
 [Concetti relativi alle stored procedure del sistema di replica](concepts/replication-system-stored-procedures-concepts.md)   
 [Utilizzo di sqlcmd con variabili di scripting](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
