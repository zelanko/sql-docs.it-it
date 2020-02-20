---
title: Script e PowerShell con Reporting Services | Microsoft Docs
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d1a0c969bf5e1964446ac9ffd3d9abe12bb90b89
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68893400"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Script e PowerShell con Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta un'ampia gamma di scenari di sviluppo e gestione tramite script, tra cui l'utilità della riga di comando rs.exe, i cmdlet PowerShell per server di report in modalità SharePoint, sfruttando il modello a oggetti [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da PowerShell per la modalità nativa e SharePoint.  
  
-   Gli amministratori possono scrivere script in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] per automatizzare le procedure di distribuzione e gestione dell'installazione di un server di report. Gli amministratori possono anche generare ed eseguire script [!INCLUDE[tsql](../../includes/tsql-md.md)] che consentono di creare, configurare e aggiornare un database del server di report. Gli amministratori possono anche usare le funzionalità script di registrazione e riproduzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per automatizzare le attività di manutenzione di routine.  
  
-   Gli sviluppatori possono creare applicazioni personalizzate che includono script. È possibile eseguire uno script che effettua chiamate al servizio Web ReportServer. Nello script è possibile scrivere quasi tutte le operazioni che si possono scrivere in codice gestito.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta lo script .NET [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] come linguaggio di script che può essere elaborato dall'utilità RS.exe, un host di script che viene eseguito nel server di report.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Cmdlet ed esempi di PowerShell in modalità SharePoint di Reporting Services  
 ![Contenuto correlato di PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include i cmdlet [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per l'amministrazione del server di report.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Sono inclusi gli esempi seguenti:  
  
    -   Creare un proxy e un'applicazione di servizio  
  
    -   Rivedere e aggiornare un'estensione per il recapito  
  
    -   Ottenere e impostare le proprietà del database dell'applicazione Reporting Service, ad esempio timeout database  
  
    -   Elencare le estensioni per i dati  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Modello a oggetti di Reporting Services ed esempi di Powershell  
 ![Contenuto correlato di PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
 Le chiamate del modello a oggetti principale di PowerShell valide in generale per la modalità SharePoint e nativa, ad esempio l'attività di migrazione, l'attività di sottoscrizione ed esempi più correlati per le sottoscrizioni, funzionano in SQL15.  
  
-   [Usare PowerShell per modificare ed elencare i proprietari di sottoscrizioni di Reporting Services ed eseguire una sottoscrizione](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Usare PowerShell per creare una VM di Azure con un server di report in modalità nativa](https://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Vedere la sezione "Accedere alle classi WMI utilizzando PowerShell" in [Accedere al provider WMI per Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  

## <a name="rsexe-scripting-samples"></a>Esempi di script RS.exe  
  
-   [Script di esempio rs.exe di Reporting Services per la copia di contenuto tra server di report](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Per altri esempi di script, applicazioni ed estensioni, vedere gli [esempi di prodotti di Reporting Services di SQL Server](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [Utilizzare script per l'esecuzione di attività di distribuzione e di amministrazione](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [Eseguire lo script con l'utilità rs.exe e il servizio Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
