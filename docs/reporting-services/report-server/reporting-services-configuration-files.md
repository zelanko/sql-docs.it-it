---
title: File di configurazione di Reporting Services | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506651"
---
# <a name="reporting-services-configuration-files"></a>File di configurazione di Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] le informazioni sui componenti vengono archiviate nel Registro di sistema e in file di configurazione che vengono copiati nel file system durante l'installazione. I file di configurazione contengono una combinazione di valori solo per uso interno e valori definiti dall'utente. I valori definiti dall'utente vengono specificati durante l'installazione, tramite gli strumenti di configurazione e le utilità della riga di comando e mediante la modifica manuale dei file di configurazione.  
  
 La modifica dei file di configurazione è necessaria solo se si aggiungono o si configurano impostazioni avanzate. Le impostazioni di configurazione sono specificate come elementi o attributi XML. Se si conoscono il linguaggio XML e i file di configurazione, è possibile utilizzare un editor di testo o di codice per modificare le impostazioni definibili dall'utente. Per altre informazioni sulla modifica di un file di configurazione o sulla modalità in cui il server di report legge le impostazioni di configurazione nuove e aggiornate, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
> Nelle versioni precedenti Gestione report dispone di un file configurazione denominato RSWebApplication.config. Tale file è diventato obsoleto. Se si esegue l'aggiornamento da un'installazione precedente, il file non verrà eliminato ma il server di report non leggerà alcuna impostazione presente nel file. Se il file esiste nel computer, eliminarlo. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive tutte le impostazioni di configurazione di Gestione report e del portale Web vengono archiviate e lette dal file RSReportServer.config. Per un elenco delle impostazioni eliminate o spostate, vedere [Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 Contenuto dell'articolo:  
  
-   [Riepilogo dei file di configurazione (modalità nativa)](#bkmk_config_file_Summary_native_mode)  
  
-   [Riepilogo dei file di configurazione (modalità SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Riepilogo dei file di configurazione (modalità nativa)  
 Nella tabella seguente viene fornita una descrizione del percorso di archiviazione delle impostazioni di configurazione. La maggior parte delle impostazioni di configurazione vengono archiviate in file di configurazione inclusi in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per impostazione predefinita, la directory di installazione è la seguente:  
  
' ' Installare percorsi  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER (dove xx è il numero di versione MS SQL) o  
C:\Programmi\Microsoft SQL Server Reporting Services\SSRS  
  a seconda della versione SSRS
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|File di archiviazione|Descrizione|Percorso|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Nel file sono archiviate le impostazioni di configurazione per caratteristiche del servizio del server di report, ovvero Gestione report o il portale Web, il servizio Web ReportServer e l'elaborazione in background. Per altre informazioni su ogni impostazione, vedere [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|Web.config per il servizio Web ReportServer|Include solo le impostazioni che sono necessarie per ASP.NET se applicabile per la versione SSRS.|\<Directory installazione> \Reporting Services \ReportServer|  
|Impostazioni del Registro di sistema|Nel Registro di sistema sono archiviati lo stato della configurazione e altre impostazioni utilizzate per disinstallare Reporting Services. Sono inoltre archiviate informazioni su ogni applicazione di servizio di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Non modificare direttamente queste impostazioni poiché questa operazione potrebbe rendere non valida l'installazione.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<IDIstanza\> \Setup<br /><br /> ID istanza di esempio: MSSQL13.MSSQLSERVER<br /><br /> **- e -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|In questo file sono archiviate impostazioni di configurazione per Progettazione report. Per altre informazioni, vedere [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<unità>:\Programmi \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Vedere anche  
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Estensioni di Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Utilità rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [Avviare e arrestare il servizio del server di report](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
