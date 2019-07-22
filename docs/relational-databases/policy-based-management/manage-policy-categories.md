---
title: Gestire categorie di criteri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policycategories.f1
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6f0600f663e00e0318a933e7824f3e0b78166f55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087192"
---
# <a name="manage-policy-categories"></a>Gestione categorie di criteri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come applicare uno o tutti i criteri disponibili in una categoria all'istanza intera di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per applicare i criteri di categoria a un'istanza di SQL Server utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando si utilizza [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se la casella di controllo **Imponi sottoscrizioni di database** non è selezionata, la categoria di criteri deve essere applicata singolarmente a ogni parte appropriata del server, ad esempio uno o più database o tabelle.  
  
-   Se si specifica una categoria di criteri non esistente, verrà creata una nuova categoria di criteri e la sottoscrizione sarà obbligatoria per tutti i database all'esecuzione della stored procedure. Se la sottoscrizione obbligatoria per la nuova categoria viene successivamente cancellata, la sottoscrizione sarà valida solo per il database specificato come *target_object*. Per altre informazioni sulla modifica dell'impostazione di una sottoscrizione obbligatoria, vedere [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Questa stored procedure viene eseguita nel contesto del proprietario corrente della stessa.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>Per applicare i criteri di categoria a un'istanza di SQL Server  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera applicare i criteri di categoria.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse su **Gestione criteri** e selezionare **Gestione categorie**.  
  
     Le informazioni seguenti sono disponibili nella finestra di dialogo **Gestione categorie di criteri** :  
  
     **Nome**  
     Nome della categoria di criteri.  
  
     **Imponi sottoscrizioni di database**  
     Impone a tutti i database presenti nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di applicare i criteri contenuti nella categoria.  
  
4.  Selezionare o deselezionare una o tutte le caselle di controllo in **Imponi sottoscrizioni di database** per applicare la categoria di criteri all'istanza di SQL Server.  
  
5.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>Per applicare i criteri di categoria a un'istanza di SQL Server  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE msdb;  
    GO  
    -- configures the specified database to subscribe to a policy category that is named 'Table Naming Policies'.  
    EXEC dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
    , @target_object = N'AdventureWorks2012'  
    , @policy_category = N'Table Naming Policies';  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_syspolicy_add_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md).  
  
  
