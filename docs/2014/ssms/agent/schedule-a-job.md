---
title: Pianificare un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abb84377c48778d0c7244c13620fe192b5421ad6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369333"
---
# <a name="schedule-a-job"></a>Schedule a Job
  In questo argomento viene descritto come pianificare un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Prima di iniziare:** ,  
  
     [Sicurezza](#Security)  
  
-   **Per pianificare un processo utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>Per creare e collegare una pianificazione a un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, espandere **Processi**, fare clic con il pulsante destro del mouse sul processo che si vuole pianificare e scegliere **Proprietà**.  
  
3.  Selezionare la pagina **Pianificazioni** e quindi fare clic su **Nuovo**.  
  
4.  Nella casella **Nome** digitare un nome per la nuova pianificazione.  
  
5.  Deselezionare la casella di controllo **Abilitata** se non si desidera attivare la pianificazione subito dopo la relativa creazione.  
  
6.  Per **Tipo pianificazione**, selezionare una delle opzioni seguenti:  
  
    -   Fare clic su **Avvia automaticamente all'avvio di SQL Server Agent** per avviare il processo all'avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
    -   Fare clic su **Avvia quando la CPU diventa inattiva** per avviare il processo quando la CPU raggiunge una condizione di inattività.  
  
    -   Fare clic su **Periodica** se si desidera eseguire ripetutamente una pianificazione. Per impostare la pianificazione periodica, completare i gruppi **Frequenza**, **Frequenza giornaliera**e **Durata** della finestra di dialogo.  
  
    -   Fare clic su **Singola occorrenza** se si desidera che la pianificazione venga eseguita una sola volta. Per impostare la pianificazione di tipo **Singola occorrenza** , completare il gruppo **Singola occorrenza** nella finestra di dialogo.  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>Per collegare una pianificazione a un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, espandere **Processi**, fare clic con il pulsante destro del mouse sul processo che si vuole pianificare e scegliere **Proprietà**.  
  
3.  Selezionare la pagina **Pianificazioni** , quindi fare clic su **Seleziona**.  
  
4.  Selezionare la pianificazione da collegare, quindi scegliere **OK**.  
  
5.  Nella finestra di dialogo **Proprietà processo** , fare doppio clic sulla pianificazione collegata.  
  
6.  Verificare che l'opzione **Data inizio** sia impostata correttamente. In caso contrario, impostare la data desiderata per l'avvio della pianificazione, quindi fare clic su **OK**.  
  
7.  Nella finestra di dialogo **Proprietà processo** scegliere **OK**.  
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-schedule-a-job"></a>Per pianificare un processo  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql) e [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql).  
  
##  <a name="SMO"></a> Utilizzo di SQL Server Management Objects  
 Usare la classe `JobSchedule` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere[SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
