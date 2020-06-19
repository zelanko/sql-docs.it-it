---
title: Rimuovere il server di controllo del mirroring da una sessione di mirroring del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], turning off
- witness [SQL Server], removing
- database mirroring [SQL Server], witness
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d5ede54aca3588a6fcd7cee8759112b606eac752
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934034"
---
# <a name="remove-the-witness-from-a-database-mirroring-session-sql-server"></a>Rimuovere il server di controllo del mirroring da una sessione di mirroring del database (SQL Server)
  In questo argomento verrà descritto come rimuovere un server di controllo del mirroring da una sessione di mirroring del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante una sessione di mirroring del database, il proprietario del database può disabilitare il server di controllo del mirroring in qualsiasi momento.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per rimuovere il server di controllo del mirroring utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la rimozione del server di controllo del mirroring](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-remove-the-witness"></a>Per rimuovere il server di controllo del mirroring  
  
1.  Connettersi all'istanza del server principale e fare clic sul nome del server per espandere l'albero di server nel riquadro **Esplora oggetti** .  
  
2.  Espandere **Database**e selezionare il database di cui si desidera rimuovere il server di controllo del mirroring.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Server mirror**. Verrà visualizzata la pagina **mirroring** della finestra di dialogo **Proprietà database** .  
  
4.  Per rimuovere il server di controllo del mirroring, eliminare l'indirizzo di rete del server dal campo **Server di controllo del mirroring** .  
  
    > [!NOTE]  
    >  Se si passa dalla modalità a protezione elevata con failover automatico alla modalità a prestazioni elevate, il contenuto del campo **Server di controllo del mirroring** viene automaticamente cancellato.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-remove-the-witness"></a>Per rimuovere il server di controllo del mirroring  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] in qualsiasi istanza del server partner.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Eseguire l'istruzione seguente:  
  
     [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) *nome_database* SET WITNESS OFF  
  
     dove *nome_database* è il nome del database con mirroring.  
  
     Nell'esempio seguente viene rimosso il server di controllo del mirroring dal database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="follow-up-after-removing-the-witness"></a><a name="FollowUp"></a>Completamento: dopo la rimozione del server di controllo del mirroring  
 La disattivazione del server di controllo del mirroring comporta la modifica della [modalità operativa](database-mirroring-operating-modes.md)in base all'impostazione del livello di protezione delle transazioni:  
  
-   Se il livello di protezione delle transazioni è impostato su FULL (impostazione predefinita), nella sessione viene utilizzata la modalità sincrona a protezione elevata senza failover automatico.  
  
-   Se la protezione delle transazioni è impostata su OFF, la sessione viene eseguita in modo asincrono (in modalità a prestazioni elevate) senza richiedere quorum. Ogni volta che la protezione delle transazioni è disattivata, è consigliabile disattivare anche il server di controllo.  
  
> [!TIP]  
>  L'impostazione della sicurezza delle transazioni per il database viene registrata per ogni partner nelle colonne **mirroring_safety_level** e **mirroring_safety_level_desc** della vista del catalogo [sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Aggiungere un server di controllo del mirroring del database tramite l'autenticazione di Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Aggiunta o sostituzione di un server di controllo del mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Modificare la sicurezza delle transazioni in una sessione di mirroring del database &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [Aggiungere un server di controllo del mirroring del database utilizzando l'autenticazione di Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [Server di controllo del mirroring del database](database-mirroring-witness.md)  
  
  
