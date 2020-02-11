---
title: Disabilitare o riattivare un avviso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], reactivating
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- alerts [SQL Server], disabling
- reactivating alerts
- removing alerts
ms.assetid: 4cb37dc6-1134-405d-8590-58b44dcf63b2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 638ce62d8dd12764681c2b65a271d9ae13bb5d83
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68189333"
---
# <a name="disable-or-reactivate-an-alert"></a>Disabilitazione o riattivazione di un avviso
  In questo argomento viene descritto come disabilitare o riattivare un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avviso [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Agent [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]tramite o.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per disabilitare o riattivare un avviso utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per impostazione predefinita, i membri del ruolo predefinito del server **sysadmin** possono modificare le informazioni nell'avviso. Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>Per disabilitare o riattivare un avviso  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server che contiene l'avviso da disabilitare o riattivare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Avvisi** .  
  
4.  Fare clic con il pulsante destro del mouse sull'avviso da abilitare e selezionare **Abilita** . Per disabilitare un avviso, fare clic con il pulsante destro del mouse sull'avviso da disabilitare e selezionare **Disabilita**.  
  
5.  Verrà visualizzata la finestra di dialogo **Disabilita avviso** o **Abilita avviso** indicante lo stato del processo. Al termine, fare clic su **Chiudi**.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>Per disabilitare o riattivare un avviso  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- changes the enabled setting of Test Alert to 0  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_alert  
        @name = N'Test Alert',  
        @enabled = 0 ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_update_alert &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql).  
  
  
