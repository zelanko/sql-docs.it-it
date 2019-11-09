---
title: Eliminare una pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa08a7f84cd413f1212cc73d4242b5da70fd33eb
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882284"
---
# <a name="delete-a-publication"></a>Delete a Publication
  In questo argomento viene descritto come eliminare una pubblicazione in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 **Contenuto dell'argomento**  
  
-   **Per eliminare una pubblicazione, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Eliminare le pubblicazioni dalla cartella **Pubblicazioni locali** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-a-publication"></a>Per eliminare una pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione che si desidera eliminare e quindi scegliere **Elimina**.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 È possibile eliminare pubblicazioni a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione eliminato.  
  
> [!NOTE]  
>  L'eliminazione di una pubblicazione non comporta la rimozione degli oggetti pubblicati dal database di pubblicazione o degli oggetti corrispondenti dal database di sottoscrizione. Utilizzare il comando `DROP <object>` per rimuovere manualmente questi oggetti, se necessario.  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>Per eliminare una pubblicazione snapshot o transazionale  
  
1.  Eseguire una delle operazioni seguenti:  
  
    -   Per eliminare una singola pubblicazione, eseguire [sp_droppublication](/sql/relational-databases/system-stored-procedures/sp-droppublication-transact-sql) nel database di pubblicazione del server di pubblicazione.  
  
    -   Per eliminare tutte le pubblicazioni e rimuovere tutti gli oggetti di replica da un database pubblicato, eseguire [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) nel server di pubblicazione. Specificare il valore `tran` per **\@tipo**. (Facoltativo) Se il server di distribuzione non è accessibile oppure se lo stato del database è sospetto oppure offline, specificare il valore **1** per **\@force**. (Facoltativo) Specificare il nome del database per **\@dbname** se [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) non viene eseguita nel database di pubblicazione.  
  
        > [!NOTE]  
        >  Specificando il valore **1** per **\@force**, è possibile che nel database rimangano oggetti di pubblicazione correlati alla replica.  
  
2.  (Facoltativo) Se il database non contiene altre pubblicazioni, eseguire [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) per disabilitare la pubblicazione del database corrente usando la replica snapshot o transazionale.  
  
3.  (Facoltativo) Nel database di sottoscrizione del Sottoscrittore eseguire [sp_subscription_cleanup](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) per rimuovere gli eventuali metadati di replica rimanenti nel database di sottoscrizione.  
  
#### <a name="to-delete-a-merge-publication"></a>Per eliminare una pubblicazione di tipo merge  
  
1.  Eseguire una delle operazioni seguenti:  
  
    -   Per eliminare una singola pubblicazione, eseguire [sp_dropmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql) nel database di pubblicazione del server di pubblicazione.  
  
    -   Per eliminare tutte le pubblicazioni e rimuovere tutti gli oggetti di replica da un database pubblicato, eseguire [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) nel server di pubblicazione. Specificare il valore `merge` per **\@tipo**. (Facoltativo) Se il server di distribuzione non è accessibile oppure se lo stato del database è sospetto oppure offline, specificare il valore **1** per **\@force**. (Facoltativo) Specificare il nome del database per **\@dbname** se [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) non viene eseguita nel database di pubblicazione.  
  
        > [!NOTE]  
        >  Specificando il valore **1** per **\@force**, è possibile che nel database rimangano oggetti di pubblicazione correlati alla replica.  
  
2.  (Facoltativo) Se il database non contiene altre pubblicazioni, eseguire [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) per disabilitare la pubblicazione del database corrente usando la replica di tipo merge.  
  
3.  (Facoltativo) Nel database di sottoscrizione del Sottoscrittore eseguire [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql) per rimuovere gli eventuali metadati di replica rimanenti nel database di sottoscrizione.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene illustrato come rimuovere una pubblicazione transazionale e disabilitare la pubblicazione transazionale per un database. Si presuppone che in precedenza siano state rimosse tutte le sottoscrizioni. Per ulteriori informazioni, vedere [Delete a Pull Subscription](../delete-a-pull-subscription.md) o [Delete a Push Subscription](../delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_droppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droppublication)]  
  
 In questo esempio viene illustrato come rimuovere una pubblicazione di tipo merge e disabilitare la pubblicazione di tipo merge per un database. Si presuppone che in precedenza siano state rimosse tutte le sottoscrizioni. Per ulteriori informazioni, vedere [Delete a Pull Subscription](../delete-a-pull-subscription.md) o [Delete a Push Subscription](../delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergepublication)]  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 È possibile eliminare pubblicazioni a livello di programmazione tramite gli oggetti RMO (Replication Management Objects). Le classi RMO utilizzate per rimuovere una pubblicazione dipendono dal tipo di pubblicazione rimossa.  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>Per rimuovere una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
4.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che la pubblicazione sia esistente. Se il valore di questa proprietà è `false`, le proprietà di pubblicazione sono state definite in modo non corretto nel passaggio 3 oppure la pubblicazione non esiste.  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> .  
  
6.  (Facoltativo) Se per il database non esistono altre pubblicazioni transazionali, è possibile disabilitare il database per la pubblicazione transazionale come illustrato di seguito:  
  
    1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> . Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'istanza di <xref:Microsoft.SqlServer.Management.Common.ServerConnection> restituita al passaggio 1.  
  
    2.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, verificare che il database esista.  
  
    3.  Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> su `false`.  
  
    4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  Chiudere le connessioni.  
  
#### <a name="to-remove-a-merge-publication"></a>Per rimuovere una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
4.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che la pubblicazione sia esistente. Se il valore di questa proprietà è `false`, le proprietà di pubblicazione sono state definite in modo non corretto nel passaggio 3 oppure la pubblicazione non esiste.  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> .  
  
6.  (Facoltativo) Se per il database non esistono altre pubblicazioni di tipo merge, è possibile disabilitare il database per la pubblicazione di tipo merge come illustrato di seguito:  
  
    1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> . Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'istanza di <xref:Microsoft.SqlServer.Management.Common.ServerConnection> restituita al passaggio 1.  
  
    2.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se il metodo restituisce `false`, verificare che il database esista.  
  
    3.  Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> su `false`.  
  
    4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  Chiudere le connessioni.  
  
###  <a name="PShellExample"></a> Esempi (RMO)  
 Nell'esempio seguente viene eliminata una pubblicazione transazionale. Se per il database non esistono altre pubblicazioni transazionali, verrà anche disabilitata la pubblicazione transazionale.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 Nell'esempio seguente viene eliminata una pubblicazione di tipo merge. Se per il database non esistono altre pubblicazioni di tipo merge, verrà anche disabilitata la pubblicazione di tipo merge.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>Vedere anche  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Pubblicare dati e oggetti di database](publish-data-and-database-objects.md)  
  
  
