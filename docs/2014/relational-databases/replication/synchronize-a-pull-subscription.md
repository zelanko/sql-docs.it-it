---
title: Sincronizzare una sottoscrizione pull | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8a7a607221599d599438352eab5add1cc94e5d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186237"
---
# <a name="synchronize-a-pull-subscription"></a>Sincronizzazione di una sottoscrizione pull
  In questo argomento viene descritto come sincronizzare una sottoscrizione pull in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agenti di replica](agents/replication-agents-overview.md)o RMO (Replication Management Objects).  
  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Le sottoscrizioni vengono sincronizzate dall'agente di distribuzione, per la replica snapshot e transazionale, o dall'agente di merge, per la replica di tipo merge. Gli agenti possono essere in esecuzione continuamente, essere in esecuzione su richiesta o essere in esecuzione su una pianificazione. Per altre informazioni sull'impostazione delle pianificazioni della sincronizzazione, vedere [Specificare le pianificazioni della sincronizzazione](specify-synchronization-schedules.md).  
  
 Sincronizzare una sottoscrizione su richiesta dalla cartella **Sottoscrizioni locali** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Per sincronizzare una sottoscrizione pull su richiesta in Management Studio  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Sottoscrizioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione che si desidera sincronizzare e quindi scegliere **Visualizza stato sincronizzazione**.  
  
4.  Nella finestra di dialogo **Visualizza stato sincronizzazione - \<Sottoscrittore>:\<DatabaseSottoscrizione>** fare clic su **Avvia**. Al termine della sincronizzazione verrà visualizzato il messaggio **Sincronizzazione completata** .  
  
5.  Scegliere **Chiudi**.  
  
##  <a name="ReplProg"></a> Replication Agents  
 Le sottoscrizioni pull possono essere sincronizzate a livello di programmazione e su richiesta richiamando il file eseguibile dell'agente di replica appropriato dal prompt dei comandi. Il file eseguibile dell'agente di replica richiamato dipenderà dal tipo di pubblicazione a cui appartiene la sottoscrizione pull. Per altre informazioni, vedere [Replication Agents](agents/replication-agents-overview.md).  
  
> [!NOTE]  
>  Gli agenti di replica si connettono al server locale con le credenziali dell'autenticazione di Windows dell'utente che avvia l'agente dal prompt dei comandi. Tali credenziali di Windows vengono inoltre utilizzate per la connessione ai server remoti tramite l'autenticazione integrata di Windows.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>Per avviare l'agente di distribuzione dal prompt dei comandi o da un file batch  
  
1.  Dal prompt dei comandi o in un file batch, avviare l' [Agente distribuzione repliche](agents/replication-distribution-agent.md) eseguendo **distrib.exe**con gli argomenti della riga di comando seguenti:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è inoltre necessario specificare gli argomenti seguenti:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>Per avviare l'agente di merge dal prompt dei comandi o da un file batch  
  
1.  Dal prompt dei comandi o in un file batch, avviare l' [Agente merge repliche](agents/replication-merge-agent.md) eseguendo **replmerg.exe**con gli argomenti della riga di comando seguenti:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è inoltre necessario specificare gli argomenti seguenti:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> Esempi (agenti di replica)  
 Nell'esempio seguente viene avviato l'agente di distribuzione per sincronizzare una sottoscrizione pull. Tutte le connessioni vengono eseguite con l'autenticazione di Windows.  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 Nell'esempio seguente viene avviato l'agente di merge per sincronizzare una sottoscrizione pull. Tutte le connessioni vengono eseguite con l'autenticazione di Windows.  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 È possibile sincronizzare le sottoscrizioni pull a livello di programmazione tramite gli oggetti RMO (Replication Management Objects) e l'accesso tramite codice gestito alle funzionalità dell'agente di replica. Le classi utilizzate per la sincronizzazione di una sottoscrizione pull dipendono dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
> [!NOTE]  
>  Se si desidera avviare una sincronizzazione eseguita in modo autonomo senza effetti sull'applicazione, avviare l'agente in modo asincrono. Se invece si desidera monitorare i risultati della sincronizzazione e ricevere callback dall'agente durante il processo di sincronizzazione (ad esempio per la visualizzazione di una barra di stato) è necessario avviare l'agente in modo sincrono. Per i sottoscrittori di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] , l'agente deve essere avviato in modo sincrono.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per sincronizzare una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> e impostare le proprietà seguenti:  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome della pubblicazione a cui appartiene la sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Nome del database di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   La connessione creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà rimanenti della sottoscrizione. Se il metodo restituisce `false`, verificare che la sottoscrizione esista.  
  
4.  Avviare l'agente di distribuzione nel Sottoscrittore in uno dei modi seguenti:  
  
    -   Chiamare il metodo <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> nell'istanza di <xref:Microsoft.SqlServer.Replication.TransPullSubscription> creata al passaggio 2. Questo metodo consente di avviare l'agente di distribuzione in modo asincrono e il controllo viene restituito immediatamente all'applicazione durante l'esecuzione del processo dell'agente. Non è possibile chiamare questo metodo per i Sottoscrittori [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] se la sottoscrizione è stata creata con il valore `false` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (impostazione predefinita).  
  
    -   Recuperare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> dalla proprietà <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> e chiamare il metodo <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> . Questo metodo avvia l'agente in modo sincrono e il controllo rimane al processo dell'agente in esecuzione. Nella modalità sincrona è possibile gestire l'evento <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> durante l'esecuzione dell'agente.  
  
        > [!NOTE]  
        >  Se è stato specificato un valore di `false` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predefinito) durante la creazione della sottoscrizione pull, è anche necessario specificare <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>e facoltativamente <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> poiché il processo dell'agente correlati metadati per la sottoscrizione non sono disponibili nel [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>Per sincronizzare una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> e impostare le proprietà seguenti:  
  
    -   Nome del database di sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   Nome della pubblicazione a cui appartiene la sottoscrizione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Nome del database pubblicato per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   Nome del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   La connessione creata nel passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà rimanenti della sottoscrizione. Se il metodo restituisce `false`, verificare che la sottoscrizione esista.  
  
4.  Avviare l'agente di merge nel Sottoscrittore in uno dei modi seguenti:  
  
    -   Chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> nell'istanza di <xref:Microsoft.SqlServer.Replication.MergePullSubscription> creata al passaggio 2. Questo metodo consente di avviare l'agente di merge in modo asincrono e il controllo viene restituito immediatamente all'applicazione durante l'esecuzione del processo dell'agente. Non è possibile chiamare questo metodo per i Sottoscrittori [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] se la sottoscrizione è stata creata con il valore `false` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (impostazione predefinita).  
  
    -   Recuperare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> dalla proprietà <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> e chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> . Questo metodo avvia l'agente di merge in modo sincrono e il controllo rimane al processo dell'agente in esecuzione. Nella modalità sincrona è possibile gestire l'evento <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> durante l'esecuzione dell'agente.  
  
        > [!NOTE]  
        >  Se si specifica un valore `false` per <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predefinito) durante la creazione della sottoscrizione pull, è necessario anche specificare <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>, e Se lo si desidera <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>, e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> perché l'agente metadati correlati al processo per la sottoscrizione non è disponibile in [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
###  <a name="PShellExample"></a> Esempi (RMO)  
 In questo esempio viene illustrata la sincronizzazione di una sottoscrizione pull di una pubblicazione transazionale, con avvio asincrono dell'agente utilizzando il processo dell'agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 In questo esempio viene illustrata la sincronizzazione di una sottoscrizione pull di una pubblicazione transazionale, con avvio sincrono dell'agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 In questo esempio viene illustrata la sincronizzazione di una sottoscrizione pull di una pubblicazione di tipo merge, con avvio asincrono dell'agente utilizzando il processo dell'agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 In questo esempio viene illustrata la sincronizzazione di una sottoscrizione pull di una pubblicazione di tipo merge, con avvio sincrono dell'agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 In questo esempio viene illustrata la sincronizzazione di una sottoscrizione pull di una pubblicazione di tipo merge con la sincronizzazione tramite il Web. La sottoscrizione è stata creata senza il processo dell'agente e i metadati correlati, pertanto l'agente deve essere avviato in modo sincrono e vengono fornite informazioni aggiuntive sulla sottoscrizione.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](synchronize-data.md)   
 [Creare una sottoscrizione pull](create-a-pull-subscription.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)  
  
  
