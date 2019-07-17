---
title: Visualizzare e modificare le proprietà delle sottoscrizioni pull | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06bfc2148f7a367fa02d94109e9b5b8a250fd1f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198981"
---
# <a name="view-and-modify-pull-subscription-properties"></a>Visualizzazione e modifica delle proprietà delle sottoscrizioni pull
  In questo argomento viene descritto come modificare le proprietà delle sottoscrizioni pull in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 **Contenuto dell'argomento**  
  
-   **Per visualizzare e modificare le proprietà delle sottoscrizioni pull tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Visualizzare le proprietà delle sottoscrizioni pull dal server di pubblicazione o dal sottoscrittore nella finestra di dialogo **Proprietà sottoscrizione - \<ServerPubblicazione>: \<DatabasePubblicazione>** disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Nel Sottoscrittore è disponibile un numero maggiore di proprietà ed è inoltre possibile modificare le proprietà. Le proprietà possono inoltre essere visualizzate sul server di pubblicazione nella scheda **Tutte le sottoscrizioni** , disponibile in Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md).  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>Per visualizzare le proprietà delle sottoscrizioni pull dal server di pubblicazione in Management Studio  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Espandere la pubblicazione appropriata, fare clic con il pulsante destro del mouse su una sottoscrizione, quindi su **Proprietà**.  
  
4.  Visualizzare le proprietà e quindi fare clic su **OK**.  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>Per visualizzare e modificare le proprietà delle sottoscrizioni pull dal Sottoscrittore in Management Studio  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Sottoscrizioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Proprietà**.  
  
4.  Se necessario, modificare le proprietà e quindi fare clic su **OK**.  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>Per visualizzare le proprietà delle sottoscrizioni pull dal server di pubblicazione in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Proprietà**.  
  
4.  Visualizzare le proprietà e quindi fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile modificare le sottoscrizioni pull e accedere alle relative proprietà a livello di programmazione utilizzando stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per visualizzare le proprietà di una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Nel Sottoscrittore eseguire [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql). Specificare i parametri **@publisher** , **@publisher_db** e **@publication** . In tal modo verranno restituite le informazioni sulla sottoscrizione archiviate nelle tabelle di sistema del Sottoscrittore.  
  
2.  Nel Sottoscrittore eseguire [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql). Specificare i parametri **@publisher** , **@publisher_db** , **@publication** e uno dei valori seguenti per **@publication_type** .  
  
    -   **0** : la sottoscrizione appartiene a una pubblicazione transazionale.  
  
    -   **1** : la sottoscrizione appartiene a una pubblicazione snapshot.  
  
3.  Nel server di pubblicazione eseguire [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql). Specificare **@publication** e **@subscriber** .  
  
4.  Nel server di pubblicazione eseguire [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), specificando **@subscriber** . In tal modo verranno visualizzate le informazioni sul Sottoscrittore.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per modificare le proprietà di una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Nel Sottoscrittore eseguire [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql), specificando **@publisher** , **@publisher_db** , **@publication** , il valore **0** (transazionale) o **1** (snapshot) per **@publication_type** , la proprietà della sottoscrizione da modificare come **@property** e il nuovo valore come **@value** .  
  
2.  (Facoltativo) Nel database di sottoscrizione del Sottoscrittore eseguire [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql). Specificare l'ID del processo dell'agente di distribuzione per **@jobid** e le proprietà del pacchetto DTS (Data Transformation Services) seguenti:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     In questo modo le proprietà del pacchetto DTS di una sottoscrizione verranno modificate.  
  
    > [!NOTE]  
    >  Per ottenere l'ID del processo, eseguire [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql).  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>Per visualizzare le proprietà di una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Nel Sottoscrittore eseguire [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql). Specificare i parametri **@publisher** , **@publisher_db** e **@publication** .  
  
2.  Nel Sottoscrittore eseguire [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql). Specificare i parametri **@publisher** , **@publisher_db** , **@publication** e il valore 2 per **@publication_type** .  
  
3.  Nel server di pubblicazione eseguire [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) per visualizzare le informazioni sulla sottoscrizione. Per restituire informazioni su una sottoscrizione specifica, è necessario specificare **@publication** , **@subscriber** e il valore **pull** per **@subscription_type** .  
  
4.  Nel server di pubblicazione eseguire [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), specificando **@subscriber** . In tal modo verranno visualizzate le informazioni sul Sottoscrittore.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>Per modificare le proprietà di una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Nel Sottoscrittore eseguire [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql). Specificare i parametri **@publication** , **@publisher** , **@publisher_db** , la proprietà della sottoscrizione da modificare come **@property** e il nuovo valore come **@value** .  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 Le classi RMO utilizzate per la visualizzazione o la modifica delle proprietà di una sottoscrizione pull dipendono dal tipo di pubblicazione per cui viene creata la sottoscrizione pull.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Per visualizzare o modificare le proprietà di una sottoscrizione pull di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> .  
  
4.  Impostare la connessione del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste nel server.  
  
6.  (Facoltativo) Per modificare le proprietà, specificare un nuovo valore per una delle proprietà dell'oggetto <xref:Microsoft.SqlServer.Replication.TransPullSubscription> che è possibile impostare, quindi chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Facoltativo) Per visualizzare le nuove impostazioni, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> per ricaricare le proprietà per l'articolo.  
  
8.  Chiudere tutte le connessioni.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>Per visualizzare o modificare le proprietà di una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> .  
  
4.  Impostare la connessione del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste nel server.  
  
6.  (Facoltativo) Per modificare le proprietà, specificare un nuovo valore per una delle proprietà dell'oggetto <xref:Microsoft.SqlServer.Replication.MergePullSubscription> che è possibile impostare, quindi chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Facoltativo) Per visualizzare le nuove impostazioni, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> per ricaricare le proprietà per l'articolo.  
  
8.  Chiudere tutte le connessioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
