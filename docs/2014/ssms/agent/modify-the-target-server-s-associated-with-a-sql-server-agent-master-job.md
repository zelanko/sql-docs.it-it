---
title: Modificare i server di destinazione associati a un processo master di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 176e73b6-08aa-48ec-b349-e84b431e65cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61173f4b9ef6c8f836b3654bdc5b7366a8a54461
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62654064"
---
# <a name="modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>Modificare i server di destinazione associati a un processo master di SQL Server Agent
  In questo argomento verrà descritto come modificare i server di destinazione associati a un processo master di SQL Server Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare i server di destinazione associati a un processo master di SQL Server Agent utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Un processo master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere destinato sia a server locali sia a server remoti.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È possibile modificare solo i processi di cui si è proprietari, a meno che non si appartenga al ruolo predefinito del server **sysadmin** . Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>Per modificare i server di destinazione associati a un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server contenente il processo in cui si desidera modificare il server di destinazione.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Processi** .  
  
4.  Fare clic con il pulsante destro del mouse sul processo in cui si vuole modificare il server di destinazione e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà processo -**_nome_processo_ selezionare **Server di destinazione** in **Seleziona una pagina**. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo: nuova pagina &#40;di destinazione processo&#41;](job-properties-new-job-targets-page.md).  
  
6.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-delete-a-target-server-currently-associated-with-a-sql-server-agent-master-job"></a>Per eliminare un server di destinazione attualmente associato a un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- removes the server SEATTLE2 from processing the Weekly Sales Backupsjob   
    -- assumes that the Weekly Sales Backups job exists  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_delete_jobserver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql).  
  
#### <a name="to-associate-a-target-server-with-the-current-sql-server-agent-master-job"></a>Per associare un server di destinazione al processo master corrente di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2   
    -- assumes that the Weekly Sales Backups job already exists and that   
    -- SEATTLE2 is registered as a target server for the current instance  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_jobserver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql).  
  
  
