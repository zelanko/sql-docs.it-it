---
title: 'Elenco di controllo: usare PowerShell per verificare PowerPivot per SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0dea40f9c4e4c0672db78ca7e841cb7cedca857e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174350"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>Elenco di controllo: utilizzare PowerShell per verificare PowerPivot per SharePoint
  Senza il superamento della prova di verifica con cui viene confermata l'operatività dei servizi e dei dati in uso, non vengono completate né le installazioni di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] né le operazioni di recupero. In questo articolo viene illustrata la modalità di esecuzione di queste procedure tramite Windows PowerShell. Ogni passaggio è inserito nella relativa sezione in modo da poter accedere direttamente ad attività specifiche. Ad esempio, eseguire lo script nella sezione [Database](#bkmk_databases) di questo argomento per verificare il nome dell'applicazione di servizio e i database del contenuto, se si desidera programmarli per la manutenzione o il backup.

|||
|-|-|
|![Contenuto correlato di PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")|Alla fine dell'argomento è disponibile uno script completo di PowerShell. Utilizzare questo script come punto di partenza per compilarne uno personalizzato per il controllo della distribuzione completa di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] .|

||
|-|
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|

 **In questo argomento**: le voci con le lettere nel sommario seguente corrispondono alle aree del diagramma. Nel diagramma vengono illustrate le operazioni riportate di seguito.

|||
|-|-|
|[Preparazione dell'ambiente di PowerShell](#bkmk_prerequisites)<br /><br /> [Sintomi e azioni consigliate](#bkmk_symptoms)<br /><br /> **(A)** [Servizio Windows Analysis Services](#bkmk_windows_service)<br /><br /> **(B)** [PowerPivotSystemService e PowerPivotEngineService](#bkmk_engine_and_system_service)<br /><br /> **(C)** [Proxy e applicazioni di servizio PowerPivot](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [Database](#bkmk_databases)<br /><br /> [Funzionalità di SharePoint](#bkmk_features)<br /><br /> [Processi timer](#bkmk_timer_jobs)<br /><br /> [Regole di integrità](#bkmk_health_rules)<br /><br /> **(E)** [Log di Servizio di registrazione unificato e di Windows](#bkmk_logs)<br /><br /> [Provider MSOLAP](#bkmk_msolap)<br /><br /> [Libreria client ADOMD.Net](#bkmk_adomd)<br /><br /> [Regole di raccolta dati di integrità](#bkmk_health_collection)<br /><br /> [Soluzioni](#bkmk_solutions)<br /><br /> [Passaggi di verifica manuali](#bkmk_manual)<br /><br /> [Altre risorse](#bkmk_more_resources)<br /><br /> [Script completo di PowerShell](#bkmk_full_script)|![verifica di powershell di powerpivot](../../../sql-server/install/media/ssas-powershell-component-verification.png "verifica di powershell di powerpivot")|

##  <a name="prepare-your-powershell-environment"></a><a name="bkmk_prerequisites"></a>Preparare l'ambiente di PowerShell
 Con i passaggi descritti in questa sezione viene preparato l'ambiente di PowerShell. I passaggi possono non essere necessari, a seconda dell'ambiente di scripting attualmente configurato.

 **Autorizzazioni di PowerShell**

 Aprire una finestra di Powershell o PowerShell ISE (Integrated Scripting Environment) con **privilegi amministrativi**. Se non si dispone di questi privilegi quando si eseguono i comandi, verrà visualizzato un messaggio di errore simile al seguente:

 Get-SPLogEvent: è necessario disporre di **privilegi amministrativi** per il computer per eseguire questo cmdlet.

 **Modulo di SharePoint e [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]**

 Se viene visualizzato un messaggio di errore analogo a quello riportato di seguito quando si eseguono i cmdlet correlati a SharePoint, eseguire il comando Add-PSSnapin:

 Termine 'Get-PowerPivotSystemService' **non riconosciuto come nome di cmdlet**, funzione, programma eseguibile o file script. Verificare l'ortografia del nome, che il percorso sia incluso e corretto, quindi riprovare.

```
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0
```

 **Windows PowerShell**

 Per ulteriori informazioni su PowerShell ISE, vedere [Introduzione a Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) e [Utilizzare Windows PowerShell per amministrare SharePoint 2013](https://technet.microsoft.com/library/ee806878\(v=office.15\).aspx).

|||
|-|-|
|![powerpivot nel set di applicazioni generali sharepoint](../../../sql-server/install/media/ssas-powerpivot-logo.png "powerpivot nel set di applicazioni generali sharepoint")|È possibile verificare facoltativamente la maggior parte dei componenti in Amministrazione centrale utilizzando il dashboard di gestione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Per aprire il dashboard in Amministrazione centrale, fare clic su **Impostazioni generali applicazione**, quindi scegliere **Dashboard di gestione** in **PowerPivot**. Per ulteriori informazioni sul dashboard, vedere [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).|

##  <a name="symptoms-and-recommended-actions"></a><a name="bkmk_symptoms"></a>Sintomi e azioni consigliate
 Nella tabella seguente è riportato un elenco di sintomi o problemi e la sezione suggerita di questo argomento da consultare per consentire la risoluzione del problema.

|Sintomo|Sezione di riferimento|
|-------------|-----------------|
|Aggiornamento dati non in fase di esecuzione|Vedere la sezione [Timer Jobs](#bkmk_timer_jobs) e verificare che **Processo timer di aggiornamento dati PowerPivot** sia online.|
|Dati del dashboard di gestione obsoleti|Vedere la sezione [Processi timer](#bkmk_timer_jobs) e verificare che **Processo timer di elaborazione dashboard di gestione dati PowerPivot** sia online.|
|Alcune parti del dashboard di gestione|Se si installa PowerPivot per SharePoint in una farm che dispone della topologia di Amministrazione centrale, senza Excel Services o PowerPivot per SharePoint, è necessario scaricare e installare la libreria client Microsoft ADOMD.NET se si desidera l'accesso completo ai report incorporati nel dashboard di gestione PowerPivot. Alcuni report nel dashboard utilizzano ADOMD.NET per accedere a dati interni relativi all'integrità del server e all'elaborazione query di PowerPivot nella farm. Vedere la sezione [Libreria client ADOMD.NET](#bkmk_adomd) e l'argomento [Installare ADOMD.NET in server front-end Web in cui viene eseguita Amministrazione centrale](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).|
|\<contenuti futuri>||

##  <a name="analysis-services-windows-service"></a><a name="bkmk_windows_service"></a>Servizio Analysis Services Windows
 Con lo script in questa sezione viene verificata l'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Verificare che il servizio sia **in esecuzione**.

```powershell
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name              DisplayName                                Status
----              -----------                                ------
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running
```

##  <a name="powerpivotsystemservice-and-powerpivotengineservice"></a><a name="bkmk_engine_and_system_service"></a>PowerPivotSystemService e PowerPivotEngineService
 Con gli script in questa sezione si verificano i servizi di sistema [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Sono disponibili un servizio di sistema per una distribuzione di SharePoint 2013 e due servizi per una distribuzione di SharePoint 2010.

 **PowerPivotSystemService**

 Verificare che lo stato sia **online**.

```powershell
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                  Status Applications                             Farm
--------                                  ------ ------------                             ----
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c
```

 **PowerPivotEngineService**

> [!NOTE]
>  **Ignorare questo script se** si utilizza SharePoint 2013. PowerPivotEngineService non fa parte di una distribuzione di SharePoint 2013. Se si esegue il cmdlet Get-PowerPivot**Engine**Service in SharePoint 2013, verrà visualizzato un messaggio di errore simile a quello riportato di seguito. Questo messaggio viene restituito anche se è stato eseguito il comando Add-PSSnapin descritto nella sezione relativa ai prerequisiti di questo argomento.
> 
>  Termine 'Get-PowerPivotEngineService' non è riconosciuto come nome di un cmdlet

 In una distribuzione di SharePoint 2010 verificare che lo stato sia **Online**.

```powershell
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName  : SQL Server Analysis Services
Status    : Online
Name      : MSOLAP$POWERPIVOT
Instances : {POWERPIVOT}
Farm      : SPFarm Name=SharePoint_Config
```

##  <a name="powerpivot-service-applications-and-proxies"></a><a name="bkmk_powerpivot_service_application"></a>Proxy e applicazioni di servizio PowerPivot
 Verificare che lo stato sia **Online**. Tramite l'applicazione Excel Services non viene utilizzato un database dell'applicazione di servizio e pertanto il cmdlet non restituisce un nome di database. Si prenda nota del database utilizzato dall'applicazione di servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in modo da poter verificare che sia online nella sezione del database più avanti in questo argomento.

 **Applicazioni di servizio PowerPivot ed Excel**

 Per una distribuzione di SharePoint 2010, verificare che lo stato sia **Online**.

```powershell
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename, DisplayName, status
```

```Output
TypeName          : PowerPivot Service Application
Name              : PowerPivotServiceApplication1
Status            : Online
UnattendedAccount : PowerPivotUnattendedAccount
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp
Farm              : SPFarm Name=SharePoint_Config
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a

TypeName    : Excel Services Application Web Service Application
DisplayName : Excel Services Application
Status      : Online
```

 **Pool di applicazioni del servizio**

> [!NOTE]
>  Nell'esempio di codice seguente viene restituita innanzitutto la proprietà applicationpool dell'applicazione di servizio [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] predefinita. Il nome viene analizzato dalla stringa e viene utilizzato per ottenere lo stato dell'oggetto pool di applicazioni.
> 
>  Verificare che lo stato sia **online**. Se lo stato non è online o viene visualizzato "errore http" quando si Esplora il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] sito, verificare che le credenziali di identità nei pool di applicazioni IIS siano ancora corrette. Il nome del pool IIS è il valore della proprietà ID restituita dal comando Get-SPServiceApplicationPool.

```powershell
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)

Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                           Status ProcessAccountName Id
----                           ------ ------------------ ------- 
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea
```

 ![Nota](../../../reporting-services/media/rs-fyinote.png "nota") Il pool di applicazioni può anche essere verificato nella pagina Amministrazione centrale **Gestisci applicazioni di servizio**. Fare clic sul nome dell'applicazione di servizio, quindi su **Proprietà** sulla barra multifunzione.

 **Proxy delle applicazioni di servizio PowerPivot ed Excel**

 Verificare che lo stato sia **online**.

```powershell
Get-SPServiceApplicationProxy | Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -Like "*powerpivot*" -Or $_.TypeName -Like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                                 Status UnattendedAccount           DisplayName
--------                                                 ------ -----------------           -----------
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1
Excel Services Application Web Service Application Proxy Online                             Excel Services Application
```

##  <a name="databases"></a><a name="bkmk_databases"></a> Database
 Con lo script seguente viene restituito lo stato dei database dell'applicazione di servizio e di tutti i database del contenuto. Verificare che lo stato sia **Online**.

```powershell
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -Or $_.TypeName -Like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                                                                       Status Server                  TypeName 
----                                                                       ------ ------                  -------- 
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database 
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database
```

##  <a name="sharepoint-features"></a><a name="bkmk_features"></a>Funzionalità di SharePoint
 Verificare che le funzionalità del sito, del Web e della farm siano online.

```powershell
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
DisplayName     Status Scope Farm                         
-----------     ------ ----- ----                         
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config
```

##  <a name="timer-jobs"></a><a name="bkmk_timer_jobs"></a>Processi timer
 Verificare che i processi timer siano **Online**. EngineService di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] non è installato in SharePoint 2013, pertanto tramite lo script non verranno elencati i processi timer di EngineService in una distribuzione di SharePoint 2013.

```powershell
Get-SPTimerJob | Where {$_.service -Like "*power*" -Or $_.service -Like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default
```

```Output
      Status DisplayName                                                                          LastRunTime          Service                             
------ -----------                                                                          -----------          -------                             
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService
```

##  <a name="health-rules"></a><a name="bkmk_health_rules"></a>Regole di integrità
 Sono presenti meno regole in una distribuzione di SharePoint 2013. Per un elenco completo delle regole per ogni ambiente di SharePoint e una spiegazione di come usare le regole, vedere [regole di integrità di PowerPivot-Configure](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md).

```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                          Enabled Summary
----                          ------- -------         
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.
```

##  <a name="windows-and-uls-logs"></a><a name="bkmk_logs"></a>Log di Windows e ULS
 **Registro eventi di Windows**

 Tramite il comando seguente verrà ricercato il registro eventi di Windows per eventi correlati all'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per informazioni sulla disabilitazione degli eventi o sulla modifica del livello di evento, vedere [configurare e visualizzare i file di log di SharePoint e la registrazione diagnostica &#40;PowerPivot per SharePoint&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).

 **Nome servizio:** MSOLAP$POWERPIVOT

 **Nome visualizzato nei servizi Windows** : SQL Server Analysis Services (POWERPIVOT)

```powershell
Get-EventLog "application" | Where-Object {$_.source -Like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -property * -AutoSize | Out-Default
```

```Output
TimeGenerated           EntryType Source            Message
-------------           --------- ------            -------
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
```

 **Log di Servizio di registrazione unificato di SharePoint, ultime 48 ore**

 Tramite il comando seguente verranno restituiti i messaggi di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dal log di Servizio di registrazione unificato creati nelle ultime 48 ore. Modificare il parametro addhours in base alle esigenze.

```powershell
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid,level, message | Format-Table -Property * -AutoSize | Out-Default
```

 Con la variazione seguente del comando vengono restituiti solo gli eventi del log per la categoria di **aggiornamento dati** .

```powershell
Get-SPLogEvent -starttime(Get-Date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message
```

```Output
Timestamp   : 4/14/2014 7:15:01 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 43
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : The following error occurred when working with the service application, Default PowerPivot Service Application. Skipping the service application..

Timestamp   : 4/14/2014 7:15:02 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 99
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to 
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout. 
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the 
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The 
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at 
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...
```

##  <a name="msolap-provider"></a><a name="bkmk_msolap"></a>Provider MSOLAP
 Verificare che si tratti del provider MSOLAP. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]e [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] richiedono MSOLAP. 5.

```powershell
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default
```

```Output
ProviderId ProviderType Description
---------- ------------ -----------
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services     
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0 
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0
```

 Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) e [Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services](https://technet.microsoft.com/library/hh758436.aspx).

##  <a name="adomdnet-client-library"></a><a name="bkmk_adomd"></a>Libreria client ADOMD.Net

```powershell
Get-WMIObject -Class win32_product | Where-Object {$_.name -Like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | out-default
```

```Output
name                                                  version      vendor
----                                                  -------      ------
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation
```

 Per altre informazioni, vedere [Installare ADOMD.NET in server front-end Web in cui viene eseguita Amministrazione centrale](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).

##  <a name="health-data-collection-rules"></a><a name="bkmk_health_collection"></a>Regole di raccolta dati di integrità
 Verificare che lo **Stato** sia online e **Abilitato** sia True.

```powershell
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -Like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                         Status Enabled TableName                   DaysToKeepDetailedData
----                         ------ ------- ---------                   ----------------------
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14
```

 Per altre informazioni, vedere [PowerPivot Usage Data Collection](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md).

##  <a name="solutions"></a><a name="bkmk_solutions"></a>Soluzioni
 Se gli altri componenti sono online, è possibile ignorare la verifica delle soluzioni. Se tuttavia mancano le regole di integrità, verificare l'esistenza e la visualizzazione delle due soluzioni. Verificare che le due soluzioni PowerPivot siano **Online** e **Distribuita**.

```powershell
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

SharePoint 2013:

```Output
Name                                 Status Deployed        DeploymentState DeployedServers
----                                 ------ --------        --------------- ---------------
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}
```

SharePoint 2010:

```Output
Name                 Status Deployed        DeploymentState DeployedServers 
----                 ------ --------        --------------- --------------- 
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}
```

 Per altre informazioni sulla distribuzione delle soluzioni SharePoint, vedere [Distribuire pacchetti delle soluzioni (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262995\(v=office.14\).aspx).

##  <a name="manual-verification-steps"></a><a name="bkmk_manual"></a>Passaggi di verifica manuali
 In questa sezione vengono descritti i passaggi di verifica che non possono essere completati con i cmdlet di PowerShell.

 **Aggiornamento dati pianificato:** configurare la pianificazione dell'aggiornamento di una cartella di lavoro su **Aggiorna anche appena possibile**.  Per ulteriori informazioni, vedere la sezione "verifica dell'aggiornamento dati" in [pianificare l'aggiornamento dei dati e le origini dati che non supportano l'autenticazione di Windows &#40;PowerPivot per SharePoint&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md).

##  <a name="more-resources"></a><a name="bkmk_more_resources"></a>Altre risorse
 [Web Server (IIS) Administration Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/ee790599.aspx)(Cmdlet di amministrazione di server Web IIS in Windows PowerShell).

 [PowerShell per controllare i servizi, i siti di IIS e il pool di applicazioni in SharePoint](https://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0).

 [Informazioni di riferimento su Windows PowerShell per SharePoint 2013](https://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)

 [Informazioni di riferimento su Windows PowerShell per SharePoint Foundation 2010](https://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)

 [Gestire Excel Services con Windows PowerShell (SharePoint Server 2010)](https://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)

 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)

 [Utilizzare il cmdlet Get-EvenLog](https://technet.microsoft.com/library/ee176846.aspx)

##  <a name="full-powershell-script"></a><a name="bkmk_full_script"></a>Script completo di PowerShell
 Nello script seguente sono contenuti tutti i comandi delle sezioni precedenti. Tramite lo script vengono eseguiti i comandi nello stesso ordine di presentazione in questo argomento. Nello script sono contenute alcune variazioni facoltative dei comandi riportati in questo argomento nel caso sia necessario il filtro aggiuntivo. Le variazioni sono disabilitate con un indicatore di commento (#). Nello script sono inoltre incluse alcune istruzioni per verificare la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Le istruzioni di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] sono disabilitate con un indicatore di commento (#).

```powershell
# This script audits services related to PowerPivot for SharePoint
$starttime = Get-Date
write-host -foregroundcolor DarkGray StartTime $starttime

Write-Host  "Import the SharePoint PowerShell snappin"
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0

Write-Host -ForegroundColor Green "Analysis Services Windows Service"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "PowerPivotEngineService and PowerPivotSystemService"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"

Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel*" -or $_.TypeName -like "*Analysis Services*"} | format-table -property * -autosize | out-default
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance

Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename,  DisplayName, status

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
# the following assumes there is only 1 PowerPivot Service Application, and returns that application's pool name.  if you have more than one, use the 2nd version
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)
Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPServiceApplicationProxy |  Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*Reporting Services*" -or $_.TypeName -like "*excel services*"} | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "DATABASES"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*" -or $_.TypeName -like "*ReportingServices*"}

Write-Host -ForegroundColor Green "features"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like "*powerpivot*" -or $_.displayName -like "*ReportServer*"}  | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPTimerJob | Where {$_.service -like "*power*" -or $_.service -like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "health rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -Property * -autosize | Out-Default
#The following is the same command but with the Inforamtion events filtered out.
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default

#Write-Host ""
Write-Host -ForegroundColor Green "ULS Log data"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message | Format-Table -Property * -AutoSize | Out-Default
#the following example filters for the category 'data refresh'
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "ADOMD.net client library"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-WMIObject -Class win32_product | Where-Object {$_.name -like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Usage Data Rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Solutions"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time
