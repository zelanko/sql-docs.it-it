---
title: Creare un passaggio di processo Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1249027630830b768d5d0a08b539f71d5b4af00d
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095539"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come eliminare un passaggio del processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che esegue script [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects.  
  
Gli script per passaggi di processo possono chiamare stored procedure e stored procedure estese. Un singolo passaggio di processo [!INCLUDE[tsql](../../includes/tsql-md.md)] può contenere più batch e comandi GO incorporati. Per ulteriori informazioni sulla creazione di un processo, vedere [Creazione di processi](../../ssms/agent/create-jobs.md).  
  
**Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
    [Security](#Security)  
  
-   **Per creare un passaggio di processo Transact-SQL utilizzando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Security"></a>Security  
Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Per creare un passaggio di processo Transact-SQL  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Transact-SQL Script (TSQL)**.  
  
6.  Nella casella **Comando** digitare i batch di comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure fare clic su **Apri** per selezionare un file [!INCLUDE[tsql](../../includes/tsql-md.md)] da utilizzare come comando.  
  
7.  Fare clic su **Analizza** per controllare la sintassi.  
  
8.  Se la sintassi è corretta, viene visualizzato un messaggio che informa che l'analisi è stata completata. Se viene rilevato un errore, correggere la sintassi prima di continuare.  
  
9. Fare clic sulla pagina **Avanzate** per impostare le opzioni del passaggio di processo, ad esempio l'azione che verrà eseguita se il passaggio di processo ha esito positivo o negativo, il numero di tentativi di esecuzione del passaggio che verranno eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e il file o la tabella in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent scriverà l'output del passaggio di processo. L'output del passaggio di processo può essere scritto in un file di sistema unicamente dai membri del ruolo predefinito del server **sysadmin** . Gli utenti di SQL Server Agent possono registrare l'output in una tabella.  
  
10. Se l'utente è membro del ruolo predefinito del server **sysadmin** e intende eseguire questo passaggio di processo con un diverso account di accesso SQL, selezionare l'account di accesso SQL dall'elenco **Esegui come utente** .  
  
## <a name="TSQL"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Per creare un passaggio di processo Transact-SQL  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- creates a job step that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Utilizzo di SQL Server Management Objects  
**Per creare un passaggio di processo Transact-SQL**  
  
Usare la classe **JobStep** tramite un linguaggio di programmazione a scelta, ad esempio Visual Basic, Visual C# o PowerShell.  
  
