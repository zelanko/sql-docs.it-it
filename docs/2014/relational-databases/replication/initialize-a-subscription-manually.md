---
title: Inizializzare manualmente una sottoscrizione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bd621890bad3bc42fb2d4d5289d71efcbdbcc2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721663"
---
# <a name="initialize-a-subscription-manually"></a>Inizializzazione manuale di una sottoscrizione
  In questo argomento si descrive come inizializzare manualmente una sottoscrizione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Anche se per inizializzare una sottoscrizione viene in genere utilizzato lo snapshot iniziale, è possibile inizializzare le sottoscrizioni di pubblicazioni senza uno snapshot, purché lo schema e i dati iniziali siano già presenti nel Sottoscrittore.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se in un database pubblicato tramite la replica transazionale sono in corso delle attività nell'intervallo di tempo che intercorre tra la copia dei dati e dello schema nel Sottoscrittore e l'inizializzazione manuale della sottoscrizione, è possibile che le modifiche risultanti da tali attività non vengano replicate nel Sottoscrittore.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 Per inizializzare manualmente una sottoscrizione a una pubblicazione, copiare lo schema e, se necessario, i dati nel database di sottoscrizione. Lo schema e i dati devono corrispondere a quelli presenti nel database di pubblicazione. Specificare quindi che la sottoscrizione non richiede schema e dati nella pagina **Inizializzazione sottoscrizioni** della Creazione guidata nuova sottoscrizione. Per ulteriori informazioni sull'accesso a questa procedura guidata, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](initialize-a-transactional-subscription-without-a-snapshot.md) e [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
 Quando si sincronizza la sottoscrizione per la prima volta, gli oggetti e i metadati necessari per la replica vengono copiati nel database di sottoscrizione.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>Per inizializzare manualmente una sottoscrizione a una pubblicazione  
  
1.  Verificare che lo schema e i dati vengano copiati nel database di sottoscrizione.  
  
2.  Deselezionare la casella di controllo **Inizializza** nella pagina **Inizializzazione sottoscrizioni** della Creazione guidata nuova sottoscrizione. Eseguire questa procedura per ogni sottoscrizione che richiede la copia solo degli oggetti e dei metadati di replica.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 È possibile inizializzare manualmente le sottoscrizioni tramite le stored procedure di replica.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>Per inizializzare manualmente una sottoscrizione pull di una pubblicazione transazionale  
  
1.  Verificare che lo schema e i dati esistano nel database di sottoscrizione. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Specificare **@publication**, **@subscriber**, il nome del database nel Sottoscrittore contenente i dati pubblicati per **@destination_db**, il valore **pull** per **@subscription_type**e il valore **Replication support only** per **@sync_type**. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
3.  Nel Sottoscrittore eseguire [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Per le sottoscrizioni di aggiornamento, vedere[Creare una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
4.  Nel Sottoscrittore eseguire [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
5.  Avviare l'agente di distribuzione per trasferire gli oggetti di replica e scaricare le modifiche più recenti dal server di pubblicazione. Per altre informazioni, vedere [Sincronizzazione di una sottoscrizione pull](synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>Per inizializzare manualmente una sottoscrizione push di una pubblicazione transazionale  
  
1.  Verificare che lo schema e i dati esistano nel database di sottoscrizione. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Specificare il nome del database nel Sottoscrittore contenente i dati pubblicati per **@destination_db**, il valore **push** per **@subscription_type**e il valore **Replication support only** per **@sync_type**. Per le sottoscrizioni di aggiornamento, vedere[Creare una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Per altre informazioni, vedere [Creazione di una sottoscrizione push](create-a-push-subscription.md).  
  
4.  Avviare l'agente di distribuzione per trasferire gli oggetti di replica e scaricare le modifiche più recenti dal server di pubblicazione. Per altre informazioni, vedere [Sincronizzazione di una sottoscrizione push](synchronize-a-push-subscription.md).  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>Per inizializzare manualmente una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Verificare che lo schema e i dati esistano nel database di sottoscrizione. Questa verifica può essere eseguita ripristinando un backup del database di pubblicazione nel Sottoscrittore.  
  
2.  Nel server di pubblicazione eseguire [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Specificare **@publication**, **@subscriber** **@subscriber_db**, e il valore **pull** per **@subscription_type**. In questo modo la sottoscrizione pull viene registrata.  
  
3.  Nel database di sottoscrizione del Sottoscrittore contenente i dati pubblicati eseguire [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Specificare il valore **none** per **@sync_type**.  
  
4.  Nel Sottoscrittore eseguire [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
5.  Avviare l'agente di merge per trasferire gli oggetti di replica e scaricare le modifiche più recenti dal server di pubblicazione. Per altre informazioni, vedere [Sincronizzazione di una sottoscrizione pull](synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>Per inizializzare manualmente una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Verificare che lo schema e i dati esistano nel database di sottoscrizione. Questa verifica può essere eseguita ripristinando un backup del database di pubblicazione nel Sottoscrittore.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Specificare il nome del database nel Sottoscrittore contenente i dati pubblicati per **@subscriber_db**, il valore **push** per **@subscription_type**e il valore None per. **** **@sync_type**  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql). Per altre informazioni, vedere [Creazione di una sottoscrizione push](create-a-push-subscription.md).  
  
4.  Avviare l'agente di merge per trasferire gli oggetti di replica e scaricare le modifiche più recenti dal server di pubblicazione. Per altre informazioni, vedere [Sincronizzazione di una sottoscrizione push](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Backup e ripristino di database replicati](administration/back-up-and-restore-replicated-databases.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)  
  
  
