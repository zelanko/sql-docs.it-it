---
title: Visualizzare e modificare le proprietà delle sottoscrizioni push | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- push subscriptions [SQL Server replication], properties
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], modifying
- modifying replication properties, push subscriptions
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ff13200783ab81e8402fe4bc97774898c97f85e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810933"
---
# <a name="view-and-modify-push-subscription-properties"></a>Visualizzazione e modifica delle proprietà delle sottoscrizioni push
  In questo argomento viene descritto come modificare le proprietà delle sottoscrizioni push in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 **Contenuto dell'argomento**  
  
-   **Per visualizzare e modificare le proprietà delle sottoscrizioni push, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Visualizzare e modificare le proprietà della sottoscrizione push dal server di pubblicazione nella:  
  
-   Il **proprietà sottoscrizione - \<Publisher >: \<Databasepubblicazione >** nella finestra di dialogo è disponibile da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Scheda **Tutte le sottoscrizioni** , disponibile in Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md).  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-management-studio"></a>Per visualizzare e modificare le proprietà della sottoscrizione push in Management Studio  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Espandere la pubblicazione appropriata, fare clic con il pulsante destro del mouse su una sottoscrizione, quindi su **Proprietà**.  
  
4.  Se necessario, modificare le proprietà e quindi fare clic su **OK**.  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-replication-monitor"></a>Per visualizzare e modificare le proprietà della sottoscrizione push in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Proprietà**.  
  
4.  Se necessario, modificare le proprietà e quindi fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile modificare le sottoscrizioni push e accedere alle relative proprietà a livello di programmazione utilizzando stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per visualizzare le proprietà di una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql). Specificare **@publication**, **@subscriber**e il valore **all** per **@article**.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)specificando **@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per modificare le proprietà di una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changesubscriber](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)specificando **@subscriber** e gli eventuali parametri per le proprietà del Sottoscrittore da modificare.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql). Specificare **@publication**, **@subscriber**, **@destination_db**, il valore **all** per **@article**, la proprietà della sottoscrizione da modificare come **@property**e il nuovo valore come **@value**. In questo modo vengono modificate le impostazioni di sicurezza per la sottoscrizione push.  
  
3.  (Facoltativo) Per modificare le proprietà del pacchetto DTS (Data Transformation Services) di una sottoscrizione, eseguire [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql) nel database di sottoscrizione del Sottoscrittore. Specificare l'ID del processo dell'agente di distribuzione per **@jobid** e le proprietà del pacchetto DTS seguenti:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     In questo modo le proprietà del pacchetto DTS di una sottoscrizione verranno modificate.  
  
    > [!NOTE]  
    >  Per ottenere l'ID del processo, eseguire [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql).  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Per visualizzare le proprietà di una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql). Specificare **@publication** e **@subscriber**.  
  
2.  Nel server di pubblicazione, eseguire [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)specificando **@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Per modificare le proprietà di una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql). Specificare **@publication**, **@subscriber**, **@subscriber_db**, la proprietà della sottoscrizione da modificare come **@property**e il nuovo valore come **@value**.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 Le classi RMO utilizzate per la visualizzazione o la modifica delle proprietà di una sottoscrizione push dipendono dal tipo di pubblicazione per cui viene creata la sottoscrizione push.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per visualizzare o modificare le proprietà di una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Impostare l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del passaggio 1 per l'impostazione della proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
6.  (Facoltativo) Per modificare le proprietà, specificare un nuovo valore per una delle proprietà dell'oggetto <xref:Microsoft.SqlServer.Replication.TransSubscription> che è possibile impostare, quindi chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Facoltativo) Per visualizzare le nuove impostazioni, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> per ricaricare le proprietà per la sottoscrizione.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-merge-publication"></a>Per visualizzare o modificare le proprietà di una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Impostare l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del passaggio 1 per l'impostazione della proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
6.  (Facoltativo) Per modificare le proprietà, specificare un nuovo valore per una delle proprietà dell'oggetto <xref:Microsoft.SqlServer.Replication.MergeSubscription> che è possibile impostare, quindi chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Facoltativo) Per visualizzare le nuove impostazioni, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> per ricaricare le proprietà per la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare le informazioni ed eseguire attività per una sottoscrizione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
