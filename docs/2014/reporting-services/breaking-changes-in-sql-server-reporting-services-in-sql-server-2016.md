---
title: Modifiche di rilievo in SQL Server Reporting Services in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d86c9bb07a52aba0cd93b006fc33edf4d1aa885
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109924"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2014
  In questo argomento vengono descritte le modifiche di rilievo introdotte in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. I problemi potrebbero verificarsi durante un aggiornamento oppure in script o report personalizzati. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
 **Contenuto dell'argomento:**  
  
-   [Modifiche di rilievo di SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
-   [Modifiche di rilievo di SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Modifiche di rilievo di SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Modifiche di rilievo di Reporting Services  
 Nessuna modifica di rilievo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Modifiche di rilievo di Reporting Services  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>Per i riferimenti server della modalità SharePoint è richiesto il sito di SharePoint  
 Non è possibile accedere o fare riferimento direttamente al server di report usando direttamente il nome virtuale nel percorso URL. Ad esempio:   
  
 `http://<Server name>/ReportServer`  
  
 È ora necessario includere il sito di SharePoint nel percorso URL. Ad esempio, se il nome del sito è '`videos`' e usato la '`sites`' prefisso, l'URL sarebbe simile al seguente:  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>Modifiche all'installazione dalla riga di comando della modalità SharePoint  
 L'impostazione di input **/RSINSTALLMODE** viene usata solo con installazioni in modalità nativa e non per quelle in modalità SharePoint. Ad esempio, quanto segue non è supportato [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]: **/RSINSTALLMODE = "DefaultSharePointMode"**. Al posto dell'impostazione di input, usare **/RSSHPINSTALLMODE = "DefaultSharePointMode"**.  
  
 L'istruzione seguente è riportato un esempio di un set di comandi e parametri di installazione completa: **setup /ACTION = install /FEATURES = SQL, RS /InstanceName = InstanceName=denali_inst1... /RSSHPINSTALLMODE = "DefaultSharePointMode"**  
  
 Per altre informazioni sulle installazioni dalla riga di comando, vedere [prompt dei comandi di installazione di Reporting Services SharePoint Mode e modalità nativa](install-windows/install-reporting-services-at-the-command-prompt.md).  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>Il provider WMI per Reporting Services non supporta più la configurazione della modalità SharePoint.  
 La configurazione di SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene completata tramite i cmdlet di PowerShell e Amministrazione centrale SharePoint. Nella nuova architettura della modalità SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene usata l'architettura dei servizi SharePoint. SharePoint non supporta interfacce WMI.  
  
 Queste modifiche si applicano al seguente elenco di componenti e flussi di lavoro:  
  
-   Applicazioni personalizzate in cui viene usato il provider WMI per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
-   Gestione configurazione [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , rskeymgmt.exe e rsconfig.exe. Per la configurazione della modalità SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , usare Amministrazione centrale SharePoint e PowerShell, anziché queste utilità.  
  
-   SQL Server Management Studio: I clienti non possono fare riferimento a un server con sintassi analoga a < machine_name > / < instance_name >. A partire dalla versione [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] , il metodo consigliato consiste nell'usare l'URL del sito di SharePoint. Ad esempio, **http://<SHAREPOINT_SERVER>/<sharePoint_site&gt**. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], l'URL del sito di SharePoint è l'unica sintassi supportata.  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>Progettazione modelli report non è disponibile in SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] non supporta più progetti di modello di report. Progettazione modelli report non è disponibile in [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Non è possibile creare nuovi progetti modello di report, aprire progetti esistenti in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e creare o aggiornare modelli di report. Per aggiornare i modelli di report, è possibile usare [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] o strumenti precedenti. È possibile continuare a usare i modelli di report come origini dati nei report creati negli strumenti di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] , quali Generatore report e Progettazione report. In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è ancora disponibile Progettazione query, cioè lo strumento usato per creare query ed estrarre i dati del report dai relativi modelli.  
  
##  <a name="bkmk_kj"></a> Modifiche di rilievo di SQL Server 2008 R2 Reporting Services  
 Questa sezione descrive le modifiche di rilievo introdotte in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Poiché SQL Server 2008 R2 è un aggiornamento secondario della versione di SQL Server 2008, è consigliabile rivedere anche il contenuto nella sezione relativa a SQL Server 2008.  
  
### <a name="expanded-csv-data-renderer"></a>Renderer dei dati CSV espanso  
 In [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]nel file CSV sono inclusi dati del grafico e del misuratore. Le applicazioni che dipendono da una struttura di file CSV precedente non verranno più usate a causa delle colonne aggiuntive per i grafici e i misuratori.  
  
 Per altre informazioni, vedere [Esportazione in un file CSV &#40;Generatore report e SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche del comportamento di SQL Server Reporting Services in SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Novità &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Funzionalità deprecate in SQL Server Reporting Services in SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funzionalità non più disponibili di SQL Server Reporting Services in SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
