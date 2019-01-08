---
title: Avviare, arrestare, sospendere, riprendere, riavviare il motore di Database, SQL Server Agent o servizio SQL Server Browser | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4b70ae7a69ce316b98c892c4dbf4059bfbc97ca4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360903"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser
  In questo argomento viene illustrato come avviare, i comandi arrestare, i comandi sospendere, i comandi riprendere o riavviare [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], i comandi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser usando Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , i comandi [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], i comandi **net** da un prompt dei comandi, i comandi [!INCLUDE[tsql](../../includes/tsql-md.md)], i comandi or PowerShell.  
  
-   **Prima di iniziare:**  
  
    -   [Descrizione dei servizi](#Services)  
  
    -   [Informazioni aggiuntive](#MoreInformation)  
  
    -   [Sicurezza](#Security)  
  
-   **Istruzioni relative all'utilizzo di:**  
  
    -   [Gestione configurazione SQL Server](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [Comandi net da una finestra del prompt dei comandi](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Services"></a> Descrizione dei servizi [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono programmi eseguibili che vengono eseguiti come servizi Windows. I programmi che vengono eseguiti come servizi Windows rimangono in esecuzione anche se sullo schermo del computer non viene rilevata alcuna attività.  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)] servizio**  
 Processo eseguibile dato da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] può essere l'istanza predefinita (una per computer) o una delle molte istanze denominate del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Usare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per determinare quali istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] vengono installate nel computer. L'istanza predefinita (se installata) è indicata come **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)**. Le istanze denominate (se installate) sono indicate come **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (<nome_istanza>)**. Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express viene installato come **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS)**.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent**  
 Servizio di Windows che esegue attività amministrative pianificate, ovvero processi e avvisi. Per altre informazioni, vedere [SQL Server Agent](../../ssms/agent/sql-server-agent.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser**  
 Servizio di Windows che rimane in attesa delle richieste in arrivo per le risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornisce ai client informazioni sulle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer. Viene usata una singola istanza del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser per tutte le istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer.  
  
###  <a name="MoreInformation"></a> Informazioni aggiuntive  
  
-   Sospendendo il servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] si impedisce a nuovi utenti di connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)], ma si consente a quelli già connessi di continuare a lavorare finché le connessioni non vengono interrotte. Sospendere il servizio quando si desidera attendere che gli utenti completino il loro lavoro prima di arrestare il servizio. In questo modo, gli utenti possono completare le transazioni in corso. Riprendi consente al [!INCLUDE[ssDE](../../includes/ssde-md.md)] di accettare nuove connessioni. Non è possibile sospendere né riprendere il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] viene visualizzato lo stato corrente dei servizi tramite le icone seguenti.  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gestione configurazione**  
  
    -   Una freccia verde sull'icona accanto al nome del servizio indica che il servizio è stato avviato.  
  
    -   Un quadrato rosso sull'icona accanto al nome del servizio indica che il servizio è stato arrestato.  
  
    -   Due linee blu verticali sull'icona accanto al nome del servizio indica che il servizio è stato sospeso.  
  
    -   Quando il [!INCLUDE[ssDE](../../includes/ssde-md.md)]viene riavviato, un quadrato rosso indica che il servizio è stato arrestato, dopodiché una freccia verde indicherà che il servizio è stato avviato correttamente.  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   Una freccia bianca su un cerchio verde accanto al nome del servizio indica che il servizio è stato avviato.  
  
    -   Un quadrato bianco su un cerchio rosso accanto al nome del servizio indica che il servizio è stato arrestato.  
  
    -   Due linee bianche verticali su un cerchio blu accanto al nome del servizio indica che il servizio è stato sospeso.  
  
-   Se si usano Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]solo le opzioni possibili saranno disponibili. Ad esempio, se il servizio è già avviato, l'opzione **Avvia** non sarà disponibile.  
  
-   Se l'esecuzione avviene su un cluster, il servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verrà gestito al meglio tramite Amministrazione cluster.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per impostazione predefinita, solo i membri del gruppo di amministratori locale possono avviare, arrestare, mettere in pausa, riprendere o riavviare un servizio. Per concedere a utenti non amministratori la possibilità di gestire servizi, vedere [Concedere agli utenti i privilegi per gestire i servizi in Windows Server 2003](https://support.microsoft.com/kb/325349). Il processo è analogo ad altre versioni di Windows.  
  
 L'arresto il [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando il [!INCLUDE[tsql](../../includes/tsql-md.md)] `SHUTDOWN` comando richiede l'appartenenza al **sysadmin** o **serveradmin** ruoli predefiniti del server e non è trasferibile.  
  
##  <a name="SSCMProcedure"></a> Utilizzo di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>Per avviare, arrestare, sospendere, riprendere o riavviare un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
2.  Se viene visualizzata la finestra di dialogo **Controllo account utente** fare clic su **Sì**.  
  
3.  Nel riquadro a sinistra di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Servizi di SQL Server**.  
  
4.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse su **SQL Server (MSSQLServer)** o su un'istanza denominata, quindi fare clic su **Avvia**, **Arresta**, **Sospendi**, **Riprendi**o **Riavvia**.  
  
5.  Fare clic su **OK** per chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Per avviare un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con le opzioni di avvio, vedere [Configurare le opzioni di avvio del server &#40;Gestione configurazione SQL Server&#41;](scm-services-configure-server-startup-options.md).  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-includessnoversionincludesssnoversion-mdmd-browser-or-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>Per avviare, arrestare, sospendere, riprendere o riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser o un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
2.  Se viene visualizzata la finestra di dialogo **Controllo account utente** fare clic su **Sì**.  
  
3.  Nel riquadro a sinistra di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fare clic su **Servizi di SQL Server**.  
  
4.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse su **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser**, **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (MSSQLServer)** o **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (<nome_istanza>)** per un'istanza denominata e quindi fare clic su **Avvia**, **Arresta**, **Sospendi**, **Riprendi** o **Riavvia**.  
  
5.  Fare clic su **OK** per chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Non è possibile sospendere Agent.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>Per avviare, arrestare, sospendere, riprendere o riavviare un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  In Esplora oggetti connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], fare clic con il pulsante destro del mouse sull'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] da avviare, quindi fare clic su **Avvia**, **Arresta**, **Sospendi**, **Riprendi**o **Riavvia**.  
  
     Oppure, in Server registrati fare clic con il pulsante destro del mouse sull'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] da avviare, selezionare **Controllo servizi**e quindi fare clic su **Avvia**, **Arresta**, **Sospendi**, **Riprendi**o **Riavvia**.  
  
2.  Se viene visualizzata la finestra di dialogo **Controllo account utente** fare clic su **Sì**.  
  
3.  Se viene richiesto di eseguire l'azione, fare clic su **Sì**.  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>Per avviare, arrestare o riavviare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
1.  In Esplora oggetti connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], fare clic con il pulsante destro del mouse su **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent**, quindi fare clic su **Avvia**, **Arresta**o **Riavvia**.  
  
2.  Se viene visualizzata la finestra di dialogo **Controllo account utente** fare clic su **Sì**.  
  
3.  Se viene richiesto di eseguire l'azione, fare clic su **Sì**.  
  
##  <a name="CommandPrompt"></a> Utilizzo dei comandi net dalla finestra del prompt dei comandi  
 I servizi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere avviati, arrestati o sospesi usando i comandi [!INCLUDE[msCoName](../../includes/msconame-md.md)] di **di** Windows.  
  
###  <a name="dbDefault"></a> Per avviare l'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Al prompt dei comandi digitare uno dei comandi seguenti:  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     oppure  
  
     **net start MSSQLSERVER**  
  
###  <a name="dbNamed"></a> Per avviare un'istanza denominata del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Al prompt dei comandi digitare uno dei comandi seguenti. Sostituire *\<instancename>* con il nome dell'istanza da gestire.  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     oppure  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="dbStartup"></a> Per avviare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] con le opzioni di avvio  
  
-   Aggiungere le opzioni di avvio alla fine dell'istruzione **net start "SQL Server (MSSQLSERVER)"** , separate da uno spazio. Quando vengono avviate con **net start**, le opzioni di avvio usano una barra (/) anziché un trattino (-).  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     oppure  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  Per altre informazioni sulle opzioni di avvio, vedere [Opzioni di avvio del servizio del motore di database](database-engine-service-startup-options.md).  
  
###  <a name="agDefault"></a> Per avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sull'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Al prompt dei comandi digitare uno dei comandi seguenti:  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     oppure  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="agNamed"></a> Per avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent su un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Al prompt dei comandi digitare uno dei comandi seguenti. Sostituire *instancename* con il nome dell'istanza da gestire.  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     oppure  
  
     **net start SQLAgent$** *instancename*  
  
 Per informazioni sull'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in modalità dettagliata per la risoluzione dei problemi, vedere [Applicazione sqlagent90](../../tools/sqlagent90-application.md).  
  
###  <a name="Browser"></a> Per avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   Al prompt dei comandi digitare uno dei comandi seguenti:  
  
     **net start "SQL Server Browser"**  
  
     oppure  
  
     **net start SQLBrowser**  
  
###  <a name="pauseStop"></a> Per sospendere o arrestare servizi dalla finestra del prompt dei comandi  
  
-   Per sospendere o arrestare servizi modificare i comandi nei modi seguenti.  
  
    -   Per sospendere un servizio, sostituire **net start** con **net pause**.  
  
    -   Per arrestare un servizio, sostituire **net start** con **net stop**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile arrestare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] tramite l'istruzione `SHUTDOWN`.  
  
#### <a name="to-stop-the-includessdeincludesssde-mdmd-using-includetsqlincludestsql-mdmd"></a>Per arrestare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   Per attendere il completamento delle stored procedure e delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] attualmente in esecuzione e quindi arrestare [!INCLUDE[ssDE](../../includes/ssde-md.md)], eseguire l'istruzione seguente.  
  
    ```tsql  
    SHUTDOWN;   
    ```  
  
-   Per arrestare immediatamente il [!INCLUDE[ssDE](../../includes/ssde-md.md)], eseguire l'istruzione seguente.  
  
    ```tsql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 Per altre informazioni sul `SHUTDOWN` istruzione, vedere [arresto &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/shutdown-transact-sql).  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
#### <a name="to-start-and-stop-includessdeincludesssde-mdmd-services"></a>Per avviare e arrestare i servizi del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
1.  In una finestra del prompt dei comandi avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell eseguendo il comando seguente.  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  Al prompt dei comandi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, eseguire il comando seguente. Sostituire `computername` con il nome del computer.  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (get-item .).ManagedComputer  
  
    ```  
  
3.  Identificare il servizio che si desidera arrestare o avviare. Selezionare una delle righe seguenti. Sostituire `instancename` con il nome dell'istanza denominata.  
  
    -   Per ottenere un riferimento all'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   Per ottenere un riferimento a un'istanza denominata del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   Per ottenere un riferimento al servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sull'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   Per ottenere un riferimento al servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent su un'istanza denominata del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   Per ottenere un riferimento al servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser.  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  Completare l'esempio per avviare e quindi arrestare il servizio selezionato.  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare SQL Server con la configurazione minima](start-sql-server-with-minimal-configuration.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
