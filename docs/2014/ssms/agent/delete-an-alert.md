---
title: Eliminare un avviso | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], deleting
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- removing alerts
ms.assetid: c982b208-e2d1-4d34-8cee-940b9baf6586
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f6da8b7376e03ff5c0ab516aeaef0e6ac538b48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62523631"
---
# <a name="delete-an-alert"></a>Delete an Alert
  In questo argomento viene descritto come [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eliminare gli avvisi [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Agent [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]tramite o.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per eliminare un avviso tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Quando si rimuove un avviso, vengono rimosse anche le notifiche associate.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono eliminare gli avvisi.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-an-alert"></a>Per eliminare un avviso  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server che contiene l'avviso di SQL Server Agent da eliminare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Avvisi** .  
  
4.  Fare clic con il pulsante destro del mouse sull'avviso da eliminare e scegliere **Elimina**.  
  
5.  Nella finestra di dialogo **Elimina oggetto** verificare che sia selezionato l'avviso corretto, quindi fare clic su **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-delete-an-alert"></a>Per eliminare un avviso  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- deletes the SQL Server Agent alert called 'Test Alert.'  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_alert  
       @name = N'Test Alert' ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere s[sp_delete_alert &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-delete-alert-transact-sql).  
  
  
