---
title: Creare un passaggio di processo di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 193805128ec3e557d219561bc29a93e9540fd5b1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798247"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
  In questo argomento viene descritto come creare e definire passaggi del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che consentono di eseguire comandi e query di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o SQL Server Management Objects.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare i passaggi di un processo di SQL Server utilizzando i comandi e/o le query di Analysis Services con:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se il passaggio del processo utilizza un comando di Analysis Services, l'istruzione del comando deve essere un metodo **Execute** di Servizi di XML for Analysis Services. L'istruzione non può includere un elemento Envelope SOAP (Simple Object Access Protocol) completo o un metodo **Discover** di XML for Analysis. A differenza di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , i passaggi di processo di **Agent non supportano le buste SOAP complete e il metodo** Discover [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni su XML for Analysis Services, vedere [Panoramica di XML for Analysis (XMLA)](https://msdn.microsoft.com/library/ms187190.aspx).  
  
-   Se il passaggio del processo utilizza una query di Analysis Services, l'istruzione della query deve essere una query di espressioni MDX. Per ulteriori informazioni su MDX, vedere [nozioni fondamentali sulle query mdx &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
  
-   Per eseguire un passaggio di processo in cui viene utilizzato il sottosistema Analysis Services, è necessario che l'utente sia membro del ruolo predefinito del server **sysadmin** o che sia autorizzato ad accedere a un account proxy valido definito per l'utilizzo di questo sottosistema. L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o l'account proxy deve inoltre essere amministratore di Analysis Services, nonché un account di dominio Windows valido.  
  
-   Solo i membri del ruolo predefinito del server **sysadmin** sono autorizzati a scrivere l'output di un passaggio del processo in un file. Se il passaggio del processo viene eseguito da utenti appartenenti al ruolo di database **SQLAgentUserRole** nel database **msdb** , sarà possibile scrivere l'output solo in una tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent scrive l'output del passaggio di processo nella tabella **sysjobstepslog** del database **msdb** .  
  
-   Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Per creare un passaggio di processo di un comando di Analysis Services  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per altre informazioni sulla creazione di un processo, vedere [Creazione di processi](create-jobs.md).  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Comando di SQL Server Analysis Services**.  
  
6.  Nell'elenco **Esegui come** selezionare un proxy definito per l'utilizzo del sottosistema Comando di Analysis Services. Un utente membro del ruolo predefinito del server **sysadmin** è inoltre autorizzato a selezionare **Account del servizio SQL Server Agent** per l'esecuzione di questo passaggio del processo.  
  
7.  Selezionare il **Server** in cui verrà eseguito il passaggio del processo oppure digitare il nome del server desiderato.  
  
8.  Nella casella **Comando** immettere l'istruzione da eseguire oppure fare clic su **Apri** per selezionare l'istruzione desiderata.  
  
9. Fare clic sulla pagina **Avanzate** per definire le opzioni relative al passaggio del processo, ad esempio l'azione che dovrà essere eseguita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in caso di esito positivo o negativo del passaggio del processo, il numero di tentativi di esecuzione del passaggio del processo e il percorso in cui scrivere l'output del passaggio del processo.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Per creare un passaggio del processo di una query di Analysis Services  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per altre informazioni sulla creazione di un processo, vedere [Creazione di processi](create-jobs.md).  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
4.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
5.  Nell'elenco **Tipo** fare clic su **Query di SQL Server Analysis Services**.  
  
6.  Nell'elenco **Esegui come** selezionare un proxy definito per l'utilizzo del sottosistema Query di Analysis Services. Un utente membro del ruolo predefinito del server **sysadmin** è inoltre autorizzato a selezionare **Account del servizio SQL Server Agent** per l'esecuzione di questo passaggio del processo.  
  
7.  Selezionare il **Server** e il **Database** in cui verrà eseguito il passaggio del processo oppure digitare il nome del server o del database desiderato.  
  
8.  Nella casella **Comando** immettere l'istruzione da eseguire oppure fare clic su **Apri** per selezionare l'istruzione desiderata.  
  
9. Fare clic sulla pagina **Avanzate** per definire le opzioni relative al passaggio del processo, ad esempio l'azione che dovrà essere eseguita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in caso di esito positivo o negativo del passaggio del processo, il numero di tentativi di esecuzione del passaggio del processo e il percorso in cui scrivere l'output del passaggio del processo.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Uso di Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Per creare un passaggio di processo di un comando di Analysis Services  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- Creates a job step that uses XMLA to create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database ',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command = N' <Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_jobstep &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Per creare un passaggio del processo di una query di Analysis Services  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_jobstep &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per creare un passaggio di processo di uno script di PowerShell**  
  
 Utilizzare la classe `JobStep` tramite un linguaggio di programmazione, come XMLA o MDX. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
