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
ms.openlocfilehash: b0bd7ad95fcda039c6fd5a9299f4339d35b8a619
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564127"
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
  
```
Install Paths  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER  (where xx is the MS SQL version number)
  or  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  depending on the SSRS version
```  
  
|File di archiviazione|Descrizione|Percorso|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Nel file sono archiviate le impostazioni di configurazione per caratteristiche del servizio del server di report, ovvero Gestione report o il portale Web, il servizio Web ReportServer e l'elaborazione in background. Per altre informazioni su ogni impostazione, vedere [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per il portale Web. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportManager|  
|Web.config per il servizio Web ReportServer|Nel file sono incluse solo le impostazioni necessarie per ASP.NET.|\<Directory installazione> \Reporting Services \ReportServer|  
|Web.config per Gestione report|Include solo le impostazioni che sono necessarie per ASP.NET se applicabile per la versione SSRS.|\<Directory installazione> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Nel file sono archiviate le impostazioni di configurazione che specificano i livello di traccia e le opzioni di registrazione per il servizio del server di report. Per ulteriori informazioni sugli elementi di questo file, vedere [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer \Bin|  
|Impostazioni del Registro di sistema|Nel Registro di sistema sono archiviati lo stato della configurazione e altre impostazioni utilizzate per disinstallare Reporting Services. Durante la risoluzione di problemi di installazione o di configurazione, è possibile visualizzare queste impostazioni per ottenere informazioni sulla configurazione del server di report.<br /><br /> Non modificare direttamente queste impostazioni poiché questa operazione potrebbe rendere non valida l'installazione.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<IDIstanza\> \Setup<br /><br /> **- e -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|In questo file sono archiviate impostazioni di configurazione per Progettazione report. Per altre informazioni, vedere [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<unità>:\Programmi \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server utilizzate durante l'anteprima del report. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Programmi\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Riepilogo dei file di configurazione (modalità SharePoint)  
 Nella tabella seguente viene fornita una descrizione dei file di configurazione utilizzati per un server di report in modalità SharePoint. La maggior parte delle impostazioni di configurazione viene archiviata nei database dell'applicazione di servizio di SharePoint. Per altre informazioni, vedere [Servizio SharePoint di Reporting Services e applicazioni di servizio](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 Per impostazione predefinita, la directory di installazione per la modalità SharePoint è la seguente:  
  
```
Install path
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
  
  
