---
title: Assegnare ad altri la proprietà di un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f22d153d55674d5dd615ab50848e4a7fd85a6dcb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800233"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
  In questo argomento viene descritto come riassegnare la proprietà dei processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a un altro utente.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [sicurezza](#Security)  
  
-   **Per assegnare ad altri utenti la proprietà di un processo usando:**  
  
     [SQL Server Management Studio](#SSMSProc2)  
  
     [Transact-SQL](#TsqlProc2)  
  
     [SQL Server Management Objects](#SMOProc2)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Per creare un processo, è necessario che l'utente sia membro di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o del ruolo predefinito del server **sysadmin** . Un processo può essere modificato solo dal proprietario o dai membri del ruolo **sysadmin** . Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
 L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
###  <a name="Security"></a> Sicurezza  
 Per motivi di sicurezza, solo il proprietario del processo o un membro del ruolo **sysadmin** può modificare la definizione del processo. Solo i membri del ruolo predefinito del server **sysadmin** possono assegnare la proprietà di un processo ad altri utenti ed eseguire qualsiasi processo, indipendentemente dal proprietario.  
  
> [!NOTE]  
>  Se si assegna la proprietà di un processo a un utente che non è membro del ruolo predefinito del server **sysadmin** e il processo sta eseguendo operazioni per le quali sono necessari account proxy, ad esempio l'esecuzione del pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] , verificare che l'utente possa accedere all'account proxy. In caso contrario, verrà generato un errore.  
  
####  <a name="Permissions"></a> Permissions  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProc2"></a> Utilizzo di SQL Server Management Studio  
 **Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**e quindi **Processi**, fare clic con il pulsante destro del mouse sul processo e scegliere **Proprietà**.  
  
3.  Nell'elenco **Proprietario** selezionare un account di accesso. Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
     L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
##  <a name="TsqlProc2"></a> Utilizzo di Transact-SQL  
 **Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra query immettere le istruzioni seguenti che usano il [sp_manage_jobs_by_login &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql) stored procedure di sistema. In questo esempio tutti i processi di `danw` vengono riassegnati a `fran??oisa`.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'fran??oisa' ;  
    GO  
    ```  
  
##  <a name="SMOProc2"></a> Utilizzo di SQL Server Management Objects  
 **Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  Chiamare la classe `Job` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per un codice di esempio, vedere [Pianificazione delle attività amministrative automatiche in SQL Server Agent](sql-server-agent.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di processi](implement-jobs.md)   
 [Crea processi](create-jobs.md)  
  
  
