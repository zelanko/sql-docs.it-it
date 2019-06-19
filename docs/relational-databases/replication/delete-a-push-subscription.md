---
title: Eliminare una sottoscrizione push | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 463a6516b70c80d9e248ddb1502f34129a8ab0e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453640"
---
# <a name="delete-a-push-subscription"></a>Eliminazione di una sottoscrizione push
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come eliminare una sottoscrizione push in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 **Contenuto dell'articolo**  
  
-   **Per eliminare una sottoscrizione push, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Eliminare una sottoscrizione push dal server di pubblicazione (dalla cartella **Pubblicazioni locali** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) o dal Sottoscrittore (dalla cartella **Sottoscrizioni locali** ). Se si elimina una sottoscrizione, gli oggetti o i dati non vengono rimossi automaticamente dalla sottoscrizione, ma è necessario rimuoverli manualmente.  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>Per eliminare una sottoscrizione push dal server di pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Espandere la pubblicazione associata alla sottoscrizione che si desidera eliminare.  
  
4.  Fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Elimina**.  
  
5.  Nella finestra di dialogo di conferma specificare se connettersi al Sottoscrittore per eliminare le informazioni sulla sottoscrizione. Se si deseleziona la casella di controllo **Connetti al Sottoscrittore** , è necessario connettersi al Sottoscrittore in un secondo momento per eliminare le informazioni.  
  
#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>Per eliminare una sottoscrizione push dal Sottoscrittore  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Sottoscrizioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione che si desidera eliminare e quindi scegliere **Elimina**.  
  
4.  Nella finestra di dialogo di conferma specificare se connettersi al server di pubblicazione per eliminare le informazioni sulla sottoscrizione. Se si deseleziona la casella di controllo **Connetti al server di pubblicazione** , sarà necessario connettersi al server di pubblicazione in seguito per eliminare le informazioni.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 È possibile eliminare sottoscrizioni push a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione a cui appartiene la sottoscrizione.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per eliminare una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Specificare i parametri **@publication** e **@subscriber**. Specificare il valore **all** per il parametro **@article**. (Facoltativo) Se non è possibile accedere al database di distribuzione, specificare il valore **1** per il parametro **@ignore_distributor** per eliminare la sottoscrizione senza rimuovere gli oggetti correlati nel database di distribuzione.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) per rimuovere i metadati di replica nel database di sottoscrizione.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>Per eliminare una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), specificando **@publication**, **@subscriber** e **@subscriber_db**. (Facoltativo) Se non è possibile accedere al database di distribuzione, specificare il valore **1** per il parametro **@ignore_distributor** per eliminare la sottoscrizione senza rimuovere gli oggetti correlati nel database di distribuzione.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md). Specificare i parametri **@publisher**, **@publisher_db**e **@publication**. per rimuovere i metadati di merge dal database di sottoscrizione.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene eliminata una sottoscrizione push di una pubblicazione transazionale.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 In questo esempio viene eliminata una sottoscrizione push di una pubblicazione di tipo merge.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 Le classi RMO utilizzate per l'eliminazione di una sottoscrizione push dipendono dal tipo di pubblicazione per cui viene creata la sottoscrizione push.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Per eliminare una sottoscrizione push di una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> .  
  
4.  Impostare l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che la sottoscrizione sia esistente. Se il valore di questa proprietà è **false**, le proprietà di sottoscrizioni sono state definite in modo non corretto nel passaggio 2 oppure la sottoscrizione non esiste.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> .  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>Per eliminare una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> .  
  
4.  Impostare l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che la sottoscrizione sia esistente. Se il valore di questa proprietà è **false**, le proprietà di sottoscrizioni sono state definite in modo non corretto nel passaggio 2 oppure la sottoscrizione non esiste.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> .  
  
###  <a name="PShellExample"></a> Esempi (RMO)  
 È possibile eliminare sottoscrizioni push a livello di programmazione tramite gli oggetti RMO (Replication Management Objects).  
  
 [!code-cs[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [Procedure consigliate per la sicurezza della replica](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
