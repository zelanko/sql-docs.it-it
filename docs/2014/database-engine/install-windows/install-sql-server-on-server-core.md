---
title: Installare SQL Server 2014 in Server Core | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29523dba8417a89261fed72da801898513796c17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775773"
---
# <a name="install-sql-server-2014-on-server-core"></a>Installare SQL Server 2014 in Server Core
  È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. In questo argomento vengono fornite informazioni dettagliate specifiche dell'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in Server Core.  
  
 L'opzione di installazione Server Core per il sistema operativo [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] offre un ambiente minimo per l'esecuzione di ruoli del server specifici. Ciò consente di ridurre i requisiti di manutenzione e gestione e la superficie di attacco per i ruoli del server in questione. Per altre informazioni sul Server principale come implementato nel [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)], vedere [Server Core per Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=202439) (https://go.microsoft.com/fwlink/?LinkId=202439). Per altre informazioni sull'implementazione di Server Core in [!INCLUDE[win8srv](../../includes/win8srv-md.md)], vedere [Server Core for Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx) (Server Core per Windows Server 2012).  
  
## <a name="prerequisites"></a>Prerequisiti  
  
|Requisito|Modalità di installazione|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|Incluso in installazioni Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Se non è abilitato, per impostazione predefinita viene abilitato durante l'installazione.<br /><br /> Non è possibile eseguire le versioni 2.0, 3.0 e 3.5 side-by-side in un computer. Durante l'installazione di .NET Framework 3.5 SP1 si ottengono automaticamente i livelli 2.0 e 3.0.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|Incluso in installazioni Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. Se non è abilitato, per impostazione predefinita viene abilitato durante l'installazione.<br /><br /> In un computer con sistema operativo Windows Server, è necessario scaricare e installare .NET Framework 3.5 SP1 prima di eseguire il programma di installazione per installare i componenti dipendenti da .NET 3.5 SP1.<br /><br /> Per altre informazioni sui requisiti e indicazioni su come acquisire e abilitare .NET Framework 3.5 nel [!INCLUDE[win8srv](../../includes/win8srv-md.md)], vedere [considerazioni sulla distribuzione di Microsoft .NET Framework 3.5](https://msdn.microsoft.com/library/windows/hardware/hh975396) (https://msdn.microsoft.com/library/windows/hardware/hh975396).|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|Per tutte le edizioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , ad eccezione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], uno dei prerequisiti di installazione prevede l'installazione di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile.<br /><br /> Per la [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)], scaricare il [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile dalla [Microsoft.NET Framework 4 (programma di installazione autonomo) per Server Core](https://go.microsoft.com/fwlink/?LinkId=220467) (https://go.microsoft.com/fwlink/?LinkId=220467)e installarlo prima di procedere con il programma di installazione.|  
|Windows Installer 4.5|Fornito con installazioni Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|Windows PowerShell 2.0|Fornito con installazioni Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
  
##  <a name="BK_SupportedFeatures"></a> Supported Features  
 Utilizzare la tabella seguente per identificare le funzionalità supportate in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in un'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|Funzionalità|Supportato|  
|-------------|---------------|  
|Servizi[!INCLUDE[ssDE](../../includes/ssde-md.md)] |Yes|  
|Replica[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Yes|  
|Ricerca full-text|Yes|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Yes|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|no|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|No|  
|Connettività strumenti client|Yes|  
|Server Integration Services<sup>[1]</sup>|Yes|  
|Compatibilità con le versioni precedenti di strumenti client.|no|  
|SDK di strumenti client|no|  
|Documentazione online di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |No|  
|Strumenti di gestione - Di base|Solo remoto<sup>[2]</sup>|  
|Strumenti di gestione - Completa|Solo remoto<sup>[2]</sup>|  
|Controller di Riesecuzione distribuita|no|  
|Client Riesecuzione distribuita|Solo remoto<sup>[2]</sup>|  
|SDK di Connettività SQL Client|Yes|  
|Microsoft Sync Framework|Sì<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|No|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|No|  
  
 <sup>[1] </sup>Per altre informazioni sul nuovo Server Integration Services e sulle relative funzionalità in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere [Integration Services &#40;SSIS&#41; Server](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md).  
  
 <sup>[2] </sup>Installazione di queste funzionalità in Server Core non è supportata. Questi componenti possono essere installati in un server diverso da [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core e connessi ai servizi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] installati in Server Core.  
  
 <sup>[3] </sup>Microsoft Sync Framework non è incluso nel [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pacchetto di installazione. È possibile scaricare la versione appropriata di Sync Framework da questa [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=221788) (https://go.microsoft.com/fwlink/?LinkId=221788) e installarla in un computer che esegue l'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
## <a name="supported-scenario-matrix"></a>Matrice di scenario supportata  
 Nella tabella seguente viene illustrata la matrice di scenario supportata per l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in un'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 e [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|||  
|-|-|  
|Edizioni di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Tutti i [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] edizioni a 64 bit<sup>[1]</sup>|  
|Lingua di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Tutte le lingue|  
|Lingua di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella combinazione lingua/impostazioni locali del sistema operativo|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows il lingua giapponese<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua tedesca<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua cinese (Cina)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua araba (Arabia Saudita)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua tailandese (Thai)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua turca<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua portoghese (Portogallo)<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in lingua inglese nel sistema operativo Windows in lingua inglese|  
|Edizione di Windows|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bit x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 bit x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bit x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bit x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bit x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 bit x64 Web Server Core|  
  
 <sup>[1] </sup>Installare la versione a 32 bit di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] edizioni non è supportata in Server Core.  
  
## <a name="upgrading"></a>Aggiornamento  
 Nelle installazioni Server Core è supportato l'aggiornamento da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## <a name="installation"></a>Installazione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non supporta l'installazione tramite apposita procedura guidata nel sistema operativo Server Core. In caso di installazione in Server Core, il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prevede il supporto della modalità non interattiva completa tramite il parametro /Q o della modalità non interattiva semplice tramite il parametro /QS. Per altre informazioni, vedere [Installare SQL Server 2014 dal prompt dei comandi](install-sql-server-from-the-command-prompt.md).  
  
> [!IMPORTANT]  
>  Non è possibile eseguire l'installazione side-by-side di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer che esegue [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core.  
  
 Indipendentemente dal metodo di installazione, è necessario confermare l'accettazione delle condizioni di licenza del software come utente singolo o per conto di un'entità, a meno che l'utilizzo del software non sia disciplinato da un contratto separato, ad esempio un contratto multilicenza [!INCLUDE[msCoName](../../includes/msconame-md.md)] o un contratto di terze parti con un fornitore di software indipendente o un OEM.  
  
 Le condizioni di licenza vengono visualizzate per la revisione e l'accettazione nell'interfaccia utente del programma di installazione. Le installazioni automatiche che utilizzano i parametri /Q o /QS devono includere il parametro /IACCEPTSQLSERVERLICENSETERMS. È possibile esaminare separatamente le condizioni di licenza alla pagina relativa alle [condizioni di licenza software Microsoft](https://go.microsoft.com/fwlink/?LinkId=148209).  
  
> [!NOTE]  
>  A seconda della modalità di ricezione del software, ad esempio attraverso un contratto multilicenza [!INCLUDE[msCoName](../../includes/msconame-md.md)] , l'utilizzo del software potrebbe essere soggetto a condizioni aggiuntive.  
  
 Per installare funzionalità specifiche, utilizzare il parametro /FEATURES e specificare la funzionalità padre oppure i valori delle funzionalità. Per ulteriori informazioni sui parametri delle funzionalità e sul relativo utilizzo, vedere le sezioni seguenti.  
  
### <a name="feature-parameters"></a>Parametri delle funzionalità  
  
|Parametro della funzionalità|Descrizione|  
|-----------------------|-----------------|  
|SQLENGINE|Viene installato solo il [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|REPLICATION|Viene installato il componente di replica insieme al [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|FULLTEXT|Viene installato il componente FullText insieme al [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|AS|Vengono installati tutti i componenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|IS|Vengono installati tutti i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|CONN|Vengono installati i componenti di connettività.|  
  
 Vedere l'esempio seguente relativo all'utilizzo di parametri delle funzionalità:  
  
|Parametro e valori|Descrizione|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Viene installato solo il [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|/FEATURES=SQLEngine,FullText|Installa il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e il componente full-text.|  
|/FEATURES=SQLEngine,Conn|Vengono installati il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e i componenti di connettività.|  
|/FEATURES=SQLEngine,AS,IS,Conn|Vengono installati il [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i componenti di connettività.|  
  
### <a name="installation-options"></a>Opzione di installazione  
 Il programma di installazione supporta le seguenti opzioni di installazione durante l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in un sistema operativo Server Core:  
  
1.  **Installazione dalla riga di comando**  
  
     Per installare funzionalità specifiche tramite l'opzione di installazione del prompt dei comandi, utilizzare il parametro /FEATURES e specificare la funzionalità padre o i valori delle funzionalità. Di seguito è riportato un esempio di utilizzo dei parametri dalla riga di comando.  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Installazione tramite il file di configurazione**  
  
     Il programma di installazione supporta l'utilizzo del file di configurazione solo tramite il prompt dei comandi. Il file di configurazione è un file di testo con la struttura di base di un parametro (coppia nome/valore) e un commento descrittivo. L'estensione del file di configurazione specificato al prompt dei comandi deve essere INI. Vedere gli esempi di ConfigurationFile.INI seguenti:  
  
    -   Installazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
         L'esempio seguente illustra come installare una nuova istanza autonoma che include il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   Installazione dei componenti di connettività  
  
         Nell'esempio seguente viene illustrato come installare i componenti di connettività.  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True  
  
        ```  
  
    -   Installazione di tutte le funzionalità supportate  
  
         Nell'esempio seguente viene illustrato come installare tutte le funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supportate in Server Core.  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     Negli esempi seguenti è illustrato come avviare il programma di installazione usando un file di configurazione.  
  
    -   File di configurazione  
  
         Di seguito sono riportati alcuni esempi di utilizzo del file di configurazione.  
  
        -   Per specificare il file di configurazione al prompt dei comandi:  
  
        ```  
        Setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   Per specificare le password al prompt dei comandi anziché nel file di configurazione:  
  
        ```  
        Setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         Se il file DefaultSetup.ini si trova nelle cartelle \x86 e \x64, al livello radice dei supporti di origine di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aprirlo e aggiungere il parametro *Features* al file.  
  
         Se il file DefaultSetup.ini non esiste, è possibile crearlo e copiarlo nelle cartelle \x86 e \x64, al livello radice dei supporti di origine di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="configuring-remote-access-of-includessnoversionincludesssnoversion-mdmd-running-on-server-core"></a>Configurazione dell'accesso remoto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in Server Core  
 Eseguire le azioni descritte di seguito per configurare l'accesso remoto di un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in esecuzione in un'installazione Server Core di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Abilitare connessioni remote nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Per abilitare connessioni remote, utilizzare in locale SQLCMD.exe ed eseguire le istruzioni seguenti nell'istanza Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>Abilitare e avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 Per impostazione predefinita, il servizio Browser è disabilitato.  Se risulta disabilitato in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in Server Core, eseguire il comando riportato di seguito dal prompt dei comandi per abilitarlo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Dopo averlo abilitato, eseguire il comando seguente dal prompt dei comandi per avviarlo:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Creazione di eccezioni in Windows Firewall  
 Per creare eccezioni per l'accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows Firewall, seguire i passaggi specificati in [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Abilitare TCP/IP nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Il protocollo TCP/IP può essere abilitato tramite Windows PowerShell per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Server Core. Eseguire la procedura seguente:  
  
1.  Avviare Gestione attività nel computer in cui è in esecuzione [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core.  
  
2.  Nella scheda **Applicazioni** fare clic su **Nuova attività**.  
  
3.  Nella finestra di dialogo **Crea una nuova attività** digitare **sqlps.exe** nel campo **Apri** , quindi fare clic su **OK**. Viene aperta la finestra di **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell**.  
  
4.  Nella finestra di **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** eseguire lo script seguente per abilitare il protocollo TCP/IP:  
  
```  
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>Disinstallazione  
 Dopo aver eseguito l'accesso a un computer in cui è in esecuzione [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, si dispone di un ambiente desktop limitato con un prompt dei comandi di amministratore. Il prompt può essere utilizzato per avviare la disinstallazione di un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per disinstallare un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], avviare l'operazione dal prompt dei comandi in modalità non interattiva completa tramite il parametro /Q o in modalità non interattiva semplice tramite il parametro /QS. Il parametro /QS consente di tenere traccia dello stato di avanzamento tramite l'interfaccia utente, ma non supporta input. /Q viene eseguito in modalità non interattiva senza alcuna interfaccia utente.  
  
 Per disinstallare un'istanza esistente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Per rimuovere un'istanza denominata, specificare il nome dell'istanza anziché il nome "MSSQLSERVER" dell'esempio precedente.  
  
> [!WARNING]
>  Se si chiude il prompt dei comandi inavvertitamente, è possibile avviare un nuovo prompt dei comandi eseguendo la procedura descritta di seguito.  
> 
>  1.  Premere Ctrl+Maiusc+Esc per visualizzare Gestione attività.  
> 2.  Nella scheda **Applicazioni** fare clic su **Nuova attività**.  
> 3.  Nella finestra di dialogo **Crea una nuova attività** digitare **cmd** nel campo **Apri** e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di SQL Server 2014 tramite un File di configurazione](install-sql-server-using-a-configuration-file.md)   
 [Installare SQL Server 2014 dal Prompt dei comandi](install-sql-server-from-the-command-prompt.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Server Core Installation Option Getting Started Guide](https://go.microsoft.com/fwlink/?LinkId=221422)  (Guida introduttiva alle opzioni di installazione di Server Core)  
 [Configurazione di un'installazione Server Core: Panoramica](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Failover Cluster Cmdlets in Windows PowerShell Listed by Task Focus](https://go.microsoft.com/fwlink/?LinkId=221419)  (Cmdlet del cluster di failover in Windows PowerShell elencati per attività)  
 [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters](https://go.microsoft.com/fwlink/?LinkId=221421) (Mapping di comandi Cluster.exe a cmdlet di Windows PowerShell per i cluster di failover)  
  
  
