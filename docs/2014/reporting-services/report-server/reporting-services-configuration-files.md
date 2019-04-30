---
title: File di configurazione di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63d2dff214ed1125450ec319dff4ad7f7dc36990
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190900"
---
# <a name="reporting-services-configuration-files"></a>File di configurazione di Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] le informazioni sui componenti vengono archiviate nel Registro di sistema e in file di configurazione che vengono copiati nel file system durante l'installazione. I file di configurazione contengono una combinazione di valori solo per uso interno e valori definiti dall'utente. I valori definiti dall'utente vengono specificati durante l'installazione, tramite gli strumenti di configurazione e le utilità della riga di comando e mediante la modifica manuale dei file di configurazione.  
  
 La modifica dei file di configurazione è necessaria solo se si aggiungono o si configurano impostazioni avanzate. Le impostazioni di configurazione sono specificate come elementi o attributi XML. Se si conoscono il linguaggio XML e i file di configurazione, è possibile utilizzare un editor di testo o di codice per modificare le impostazioni definibili dall'utente. Per altre informazioni sulla modifica di un file di configurazione o sulla modalità in cui il server di report legge le impostazioni di configurazione nuove e aggiornate, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
>  Nelle versioni precedenti Gestione report dispone di un file configurazione denominato RSWebApplication.config. Tale file è diventato obsoleto. Se si esegue l'aggiornamento da un'installazione precedente, il file non verrà eliminato ma il server di report non leggerà alcuna impostazione presente nel file. Se il file esiste nel computer, eliminarlo. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive tutte le impostazioni di configurazione di Gestione report vengono archiviate e lette dal file RSReportServer.config. Per esaminare un elenco dei quali impostazioni eliminate o spostate, vedere [modifiche di rilievo di SQL Server Reporting Services in SQL Server 2014](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 Contenuto dell'argomento:  
  
-   [Riepilogo dei file di configurazione (modalità nativa)](#bkmk_config_file_Summary_native_mode)  
  
-   [Riepilogo dei file di configurazione (modalità SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Riepilogo dei file di configurazione (modalità nativa)  
 Nella tabella seguente viene fornita una descrizione del percorso di archiviazione delle impostazioni di configurazione. La maggior parte delle impostazioni di configurazione vengono archiviate in file di configurazione inclusi in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per impostazione predefinita, la directory di installazione è la seguente:  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|File di archiviazione|Descrizione|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Archivia le impostazioni di configurazione delle aree di funzionalità del servizio Server di Report: Gestione report, il servizio Web ReportServer e l'elaborazione in background. Per ulteriori informazioni su ogni impostazione, vedere [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le Gestione report. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportManager|  
|Web.config per il servizio Web ReportServer|Nel file sono incluse solo le impostazioni necessarie per ASP.NET.|\<Directory installazione> \Reporting Services \ReportServer|  
|Web.config per Gestione report|Nel file sono incluse solo le impostazioni necessarie per ASP.NET.|\<Directory installazione> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Nel file sono archiviate le impostazioni di configurazione che specificano i livello di traccia e le opzioni di registrazione per il servizio del server di report. Per ulteriori informazioni sugli elementi di questo file, vedere [ReportingServicesService Configuration File](reportingservicesservice-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer \Bin|  
|Impostazioni del Registro di sistema|Nel Registro di sistema sono archiviati lo stato della configurazione e altre impostazioni utilizzate per disinstallare Reporting Services. Durante la risoluzione di problemi di installazione o di configurazione, è possibile visualizzare queste impostazioni per ottenere informazioni sulla configurazione del server di report.<br /><br /> Non modificare direttamente queste impostazioni poiché questa operazione potrebbe rendere non valida l'installazione.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<IDIstanza\> \Setup<br /><br /> **- e -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|In questo file sono archiviate impostazioni di configurazione per Progettazione report. Per altre informazioni, vedere [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md).|\<unità>:\Programmi \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server utilizzate durante l'anteprima del report. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Programmi\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Riepilogo dei file di configurazione (modalità SharePoint)  
 Nella tabella seguente viene fornita una descrizione dei file di configurazione utilizzati per un server di report in modalità SharePoint. La maggior parte delle impostazioni di configurazione viene archiviata nei database dell'applicazione di servizio di SharePoint. Per altre informazioni, vedere [Servizio SharePoint di Reporting Services e applicazioni di servizio](../reporting-services-sharepoint-service-and-service-applications.md).  
  
 Per impostazione predefinita, la directory di installazione per la modalità SharePoint è la seguente:  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|File di archiviazione|Descrizione|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Archivia le impostazioni di configurazione delle aree di funzionalità del servizio Server di Report: Gestione report, il servizio Web ReportServer e l'elaborazione in background. Per ulteriori informazioni su ogni impostazione, vedere [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Nel file sono archiviati i criteri di sicurezza dall'accesso di codice per le estensioni del server. Per ulteriori informazioni su questo file, vedere [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directory installazione> \Reporting Services \ReportServer|  
|Web.config per il servizio Web ReportServer|Nel file sono incluse solo le impostazioni necessarie per ASP.NET.|\<Directory installazione> \Reporting Services \ReportServer|  
|Impostazioni del Registro di sistema|Nel Registro di sistema sono archiviati lo stato della configurazione e altre impostazioni utilizzate per disinstallare Reporting Services. Sono inoltre archiviate informazioni su ogni applicazione di servizio di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Non modificare direttamente queste impostazioni poiché questa operazione potrebbe rendere non valida l'installazione.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<IDIstanza\> \Setup<br /><br /> ID istanza di esempio: MSSQL12.MSSQLSERVER<br /><br /> **- e -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|In questo file sono archiviate impostazioni di configurazione per Progettazione report. Per altre informazioni, vedere [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md).|\<unità>:\Programmi \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Vedere anche  
 [Server di report di Reporting Services &#40;modalità nativa&#41;](reporting-services-report-server-native-mode.md)   
 [Estensioni di Reporting Services](../extensions/reporting-services-extensions.md)   
 [Utilità rsconfig &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [Avviare e arrestare il servizio del server di report](start-and-stop-the-report-server-service.md)  
  
  
