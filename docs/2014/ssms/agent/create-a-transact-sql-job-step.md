---
title: Creare un passaggio di processo Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 383a85bbbad6675c629f7789a09dca4cb0666559
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211445"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
  In questo argomento viene descritto come eliminare un passaggio del processo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che esegue script [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects.  
  
 Gli script per passaggi di processo possono chiamare stored procedure e stored procedure estese. Un singolo passaggio di processo [!INCLUDE[tsql](../../includes/tsql-md.md)] può contenere più batch e comandi GO incorporati. Per ulteriori informazioni sulla creazione di un processo, vedere [Creazione di processi](create-jobs.md).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare un passaggio di processo Transact-SQL utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Per creare un passaggio di processo Transact-SQL  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Transact-SQL Script (TSQL)** .  
  
6.  Nella casella **Comando** digitare i batch di comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure fare clic su **Apri** per selezionare un file [!INCLUDE[tsql](../../includes/tsql-md.md)] da utilizzare come comando.  
  
7.  Fare clic su **Analizza** per controllare la sintassi.  
  
8.  Se la sintassi è corretta, viene visualizzato un messaggio che informa che l'analisi è stata completata. Se viene rilevato un errore, correggere la sintassi prima di continuare.  
  
9. Fare clic sulla pagina **Avanzate** per impostare le opzioni del passaggio di processo, ad esempio l'azione che verrà eseguita se il passaggio di processo ha esito positivo o negativo, il numero di tentativi di esecuzione del passaggio che verranno eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e il file o la tabella in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent scriverà l'output del passaggio di processo. L'output del passaggio di processo può essere scritto in un file di sistema unicamente dai membri del ruolo predefinito del server **sysadmin** . Gli utenti di SQL Server Agent possono registrare l'output in una tabella.  
  
10. Se l'utente è membro del ruolo predefinito del server **sysadmin** e intende eseguire questo passaggio di processo con un diverso account di accesso SQL, selezionare l'account di accesso SQL dall'elenco **Esegui come utente** .  
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Per creare un passaggio di processo Transact-SQL  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Per altre informazioni, vedere [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="SMO"></a> Utilizzo di SQL Server Management Objects  
 **Per creare un passaggio di processo Transact-SQL**  
  
 Usare la classe `JobStep` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell.  
  
  
