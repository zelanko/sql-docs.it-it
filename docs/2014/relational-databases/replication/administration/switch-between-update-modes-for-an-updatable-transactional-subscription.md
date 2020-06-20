---
title: Passare da una modalità di aggiornamento all'altra per una sottoscrizione transazionale aggiornabile | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c31814d1e2ab6fac64ffcde883f3cac2439828a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055732"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Passaggio da una modalità di aggiornamento all'altra per una sottoscrizione transazionale aggiornabile
  In questo argomento viene descritto come passare da una modalità di aggiornamento all'altra per una sottoscrizione con transazione aggiornabile in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Per specificare la modalità per le sottoscrizioni aggiornabili, utilizzare la Creazione guidata nuova sottoscrizione. Per informazioni sull'impostazione della modalità durante l'uso di questa procedura guidata, vedere [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../view-and-modify-pull-subscription-properties.md).  
  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   È possibile eseguire il failover dall'aggiornamento immediato a quello in coda in qualsiasi momento. In seguito, sarà tuttavia possibile tornare all'aggiornamento immediato solo dopo la connessione del Sottoscrittore e del server di pubblicazione e l'applicazione da parte dell'agente di lettura coda di tutti i messaggi in sospeso nella coda al server di pubblicazione.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Se una sottoscrizione ad aggiornamento di una pubblicazione transazionale supporta il failover da una modalità di aggiornamento a un'altra, è possibile passare a livello programmatico tra le modalità di aggiornamento, al fine di gestire situazioni in cui la connettività cambia per un breve periodo di tempo. La modalità di aggiornamento può essere impostata a livello di programmazione e su richiesta utilizzando le stored procedure di replica. Per altre informazioni, vedere [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
> [!NOTE]  
>  Per cambiare la modalità di aggiornamento dopo avere creato la sottoscrizione, è necessario impostare la proprietà **update_mode** sul valore **failover** , che consente di passare dall'aggiornamento immediato all'aggiornamento in coda, oppure sul valore **queued failover** , che consente di passare dall'aggiornamento in coda all'aggiornamento immediato, quando viene creata la sottoscrizione. Queste proprietà vengono impostate automaticamente nella Creazione guidata nuova sottoscrizione.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Per impostare la modalità di aggiornamento per una sottoscrizione push  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Sottoscrizioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione per la quale si desidera impostare la modalità di aggiornamento e quindi scegliere **Imposta metodo di aggiornamento**.  
  
4.  Nella finestra di dialogo **Imposta metodo di aggiornamento- \<Subscriber> \<SubscriptionDatabase> :** selezionare **aggiornamento immediato** o **aggiornamento in coda**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Per impostare la modalità di aggiornamento per una sottoscrizione pull  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione- \<Publisher> : \<PublicationDatabase> ** selezionare un valore per **replicare immediatamente** le modifiche o le **modifiche della coda** per l'opzione del metodo di aggiornamento del **Sottoscrittore** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Per ulteriori informazioni sull'accesso alla finestra di dialogo **Proprietà sottoscrizione- \<Publisher> : \<PublicationDatabase> ** , vedere [visualizzare e modificare le proprietà delle sottoscrizioni pull](../view-and-modify-pull-subscription-properties.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Per passare da una modalità di aggiornamento all'altra  
  
1.  Verificare che la sottoscrizione supporti il failover eseguendo [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql) per una sottoscrizione pull o [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) per una sottoscrizione push. Se il valore di **update mode** nel set di risultati è **3** o **4**, il failover è supportato.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_setreplfailovermode](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql). Specificare **@publisher** , **@publisher_db** , **@publication** e uno dei valori seguenti per **@failover_mode** :  
  
    -   **queued** : viene eseguito il failover all'aggiornamento in coda in caso di perdita temporanea della connettività.  
  
    -   **immediate** : viene eseguito il failover all'aggiornamento immediato quando la connettività viene ripristinata.  
  
## <a name="see-also"></a>Vedere anche  
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
