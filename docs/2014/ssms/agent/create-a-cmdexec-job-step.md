---
title: Creare un passaggio di processo di CmdExec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ba283ef2ff426521c881f733bc29465eebc0c76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798163"
---
# <a name="create-a-cmdexec-job-step"></a>Create a CmdExec Job Step
  In questo argomento viene descritto come creare e definire [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un passaggio di processo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Agent in in cui viene utilizzato un programma eseguibile [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[tsql](../../includes/tsql-md.md)] un comando del sistema operativo tramite, o SQL Server Management Objects.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare un passaggio di processo CmdExec utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono creare passaggi di processo CmdExec. Questi passaggi di processo vengono eseguiti nel contesto dell'account di servizio SQL Server Agent a meno che l'utente **sysadmin** crei un account proxy. Gli utenti che non sono membri del ruolo **sysadmin** possono creare passaggi di processo CmdExec se hanno accesso a un account proxy CmdExec.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-cmdexec-job-step"></a>Per creare un passaggio del processo di CmdExec  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espanderla.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** selezionare **Sistema operativo (CmdExec)**.  
  
6.  Nell'elenco **Esegui come** selezionare l'account proxy con le credenziali che verranno utilizzate dal processo. Per impostazione predefinita, questi passaggi di processo vengono eseguiti nel contesto dell'account di servizio SQL Server Agent.  
  
7.  Nella casella **Elabora codice di uscita di un comando eseguito correttamente** digitare un valore compreso tra 0 e 999999.  
  
8.  Nella casella **Comando** digitare il comando di sistema operativo o programma eseguibile. Per un esempio vedere "Utilizzo di Transact-SQL".  
  
9. Fare clic sulla pagina **Avanzate** per impostare le opzioni relative ai passaggi di processo, ad esempio l'operazione da eseguire se il passaggio di processo ha esito positivo o negativo, il numero di tentativi che devono essere eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'esecuzione del passaggio di processo e il file in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può scrivere l'output del passaggio di processo. L'output del passaggio di processo può essere scritto in un file di sistema unicamente dai membri del ruolo predefinito del server **sysadmin** .  
  
##  <a name="TSQL"></a> Con Transact-SQL  
  
### <a name="to-create-a-cmdexec-job-step"></a>Per creare un passaggio del processo di CmdExec  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- creates a job step that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
##  <a name="SMO"></a>Utilizzo di SQL Server Management Objects  

### <a name="to-create-a-cmdexec-job-step"></a>Per creare un passaggio del processo di CmdExec
  
 Usare la classe `JobStep` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell.  
