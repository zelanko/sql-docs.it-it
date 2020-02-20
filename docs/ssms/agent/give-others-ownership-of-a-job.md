---
title: Give Others Ownership of a Job
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0e87d9d46392674a8df15b6409c81a9568d9b8ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242374"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come riassegnare la proprietà dei processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a un altro utente.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per assegnare ad altri utenti la proprietà di un processo usando:**  
  
    [SQL Server Management Studio](#SSMSProc2)  
  
    [Transact-SQL](#TsqlProc2)  
  
    [SQL Server Management Objects](#SMOProc2)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
Per creare un processo, è necessario che l'utente sia membro di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o del ruolo predefinito del server **sysadmin** . Un processo può essere modificato solo dal proprietario o dai membri del ruolo **sysadmin** . Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
### <a name="Security"></a>Sicurezza  
Per motivi di sicurezza, solo il proprietario del processo o un membro del ruolo **sysadmin** può modificare la definizione del processo. Solo i membri del ruolo predefinito del server **sysadmin** possono assegnare la proprietà di un processo ad altri utenti ed eseguire qualsiasi processo, indipendentemente dal proprietario.  
  
> [!NOTE]  
> Se si assegna la proprietà di un processo a un utente che non è membro del ruolo predefinito del server **sysadmin** e il processo sta eseguendo operazioni per le quali sono necessari account proxy, ad esempio l'esecuzione del pacchetto [!INCLUDE[ssIS](../../includes/ssis_md.md)] , verificare che l'utente possa accedere all'account proxy. In caso contrario, verrà generato un errore.  
  
#### <a name="Permissions"></a>Autorizzazioni  
Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMSProc2"></a>Utilizzo di SQL Server Management Studio  
**Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**e quindi **Processi**, fare clic con il pulsante destro del mouse sul processo e scegliere **Proprietà**.  
  
3.  Nell'elenco **Proprietario** selezionare un account di accesso. Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
    L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
## <a name="TsqlProc2"></a>Utilizzo di Transact-SQL  
**Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query immettere le istruzioni seguenti che usano la stored procedure di sistema [sp_manage_jobs_by_login (Transact-SQL)](https://msdn.microsoft.com/832ec15a-6e92-4eb5-8c4a-af4dba79fbaa) . In questo esempio tutti i processi di `danw` vengono riassegnati a `françoisa`.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
## <a name="SMOProc2"></a>Utilizzo di SQL Server Management Objects  
**Per assegnare ad altri utenti la proprietà di un processo**  
  
1.  Chiamare la classe **Job** tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per un codice di esempio, vedere [Pianificazione delle attività amministrative automatiche in SQL Server Agent](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md).  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione di processi](../../ssms/agent/implement-jobs.md)  
[Crea processi](../../ssms/agent/create-jobs.md)  
  
