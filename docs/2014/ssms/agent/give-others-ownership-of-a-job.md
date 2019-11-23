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
ms.openlocfilehash: 20bd8904f8dfabd81f3f16ef7bed4c6bf1084c0d
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798225"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
  In questo argomento viene descritto come riassegnare la proprietà dei processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a un altro utente.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
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
>  Se si assegna la proprietà di un processo a un utente che non è membro del ruolo predefinito del server **sysadmin** e il processo sta eseguendo operazioni per le quali sono necessari account proxy, ad esempio l'esecuzione del pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)], verificare che l'utente possa accedere all'account proxy. In caso contrario, verrà generato un errore.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per informazioni dettagliate, vedere [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProc2"></a> Con SQL Server Management Studio  
 **Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**e quindi **Processi**, fare clic con il pulsante destro del mouse sul processo e scegliere **Proprietà**.  
  
3.  Nell'elenco **Proprietario** selezionare un account di accesso. Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
     L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
##  <a name="TsqlProc2"></a> Con Transact-SQL  
 **Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra query immettere le istruzioni seguenti che usano la [sp_manage_jobs_by_login &#40;stored procedure di sistema Transact-&#41; SQL](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql) . In questo esempio tutti i processi di `danw` vengono riassegnati a `fran??oisa`.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'fran??oisa' ;  
    GO  
    ```  
  
##  <a name="SMOProc2"></a>Utilizzo di SQL Server Management Objects  

### <a name="to-give-others-ownership-of-a-job"></a>Per assegnare ad altri utenti la proprietà di un processo
  
1.  Chiamare la classe `Job` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per un esempio di codice, vedere [Pianificazione delle attività amministrative automatiche in SQL Server Agent](sql-server-agent.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di processi](implement-jobs.md)   
 [Creare processi](create-jobs.md)  
