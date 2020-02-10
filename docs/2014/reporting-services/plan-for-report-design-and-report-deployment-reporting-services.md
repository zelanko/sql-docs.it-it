---
title: Pianificare la progettazione e la distribuzione di report (Reporting Services 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6104bfc97d2f66652ffa9b16e9ff0ae8f9b0550
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108045"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>Pianificare la progettazione e la distribuzione di report (Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in sono disponibili diversi approcci per la creazione e la distribuzione dei report. Utilizzare questo argomento per la pianificazione di un ambiente di creazione di report e un server di report che interagiscono. In questo argomento viene fornita una panoramica del supporto delle definizioni di report mediante i componenti [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Una definizione di report è un file XML scritto in linguaggio RDL (Report Definition Language) o RDLC (Report Definition Language for Clients). Ogni definizione di report è conforme a una versione di schema specifica elencata all'inizio del file.  
  
 I file RDL vengono creati in Progettazione report nei progetti di [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e in Generatore report 3.0. I file RDLC vengono creati tramite i controlli ReportViewer inclusi in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 In questo argomento  
  
-   [Versioni dello schema RDL](#bkmk_rdl_schema_versions)  
  
-   [Server di report e supporto dello schema RDL](#bkmk_report_server_rdl_schema_support)  
  
-   [Supporto per la creazione e la distribuzione di report](#bkmk_report_authoring_and_deployment)  
  
-   [Controlli ReportViewer](#bkmk_reportviewer)  
  
##  <a name="bkmk_rdl_schema_versions"></a>Versioni dello schema RDL  
 Nella tabella seguente viene fornito un elenco delle versioni dello schema disponibili e delle relative abbreviazioni utilizzate nella parte restante dell'argomento:  
  
|Abbreviazione|Versione dello schema|  
|------------------|--------------------|  
|2010 RDL|https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition|  
|2008 RDL|https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition|  
|2005 RDL<br /><br /> 2005 RDLC|https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition|  
|2000 RDL|https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition|  
  
 Per ulteriori informazioni su RDL e sugli schemi RDL, vedere quanto riportato di seguito:  
  
-   [Microsoft SQL Server XML Schema](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [Specifiche Report Definition Language](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
 Per altre informazioni sui controlli ReportViewer, vedere [Controlli ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx).  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a>Server di report e supporto dello schema RDL  
 In un server di report di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] è possibile distribuire un file di definizione del report nei modi seguenti:  
  
-   **Progettazione report:** Distribuire un report da Progettazione report in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)].  
  
-   **Generatore report:** Salvare un report nel server di report da Generatore report.  
  
-   **Gestione report:** Caricare un report in un server di report in modalità nativa da Gestione report.  
  
-   **SharePoint:** Caricare un report in un sito di SharePoint configurato con un server di report in modalità SharePoint.  
  
-   **A livello di codice:** Pubblicare un report a livello di codice utilizzando le interfacce API SOAP in un server di report. Per ulteriori informazioni, vedere [Report Server Web Service](report-server-web-service/report-server-web-service.md).  
  
 Nella tabella seguente viene elencata la versione supportata dello schema rdl in base alla versione del server di report.  
  
|Versione del server di report|Versione dello schema RDL|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> Oppure<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> Oppure<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|2005 RDL<br /><br /> 2000 RDL|  
  
 Quando si carica una definizione di report nel server di report o si aggiorna un server di report che contiene report esistenti, il server di report mantiene il formato originale della definizione del report. Al **primo utilizzo**, il server di report aggiorna il report nel database del server di report a un formato binario mantenuto per le visualizzazioni successive. La definizione del report (con estensione RDL) non viene aggiornata.  
  
 È possibile estrarre dal server di report una copia di sola lettura del file di definizione del report (con estensione RDL). In un server di report in modalità nativa, passare a Gestione report, selezionare il report e fare clic su **Download**. In una distribuzione in modalità SharePoint, passare alla raccolta documenti, selezionare il report e fare clic su **Scarica una copia**.  
  
 Per aggiornare la definizione del report, è necessario aprire il report in un ambiente di creazione di report e salvarlo.  
  
 Per altre informazioni sugli aggiornamenti del report e sulle versioni dello schema supportate, vedere [Aggiornare i report](install-windows/upgrade-reports.md).  
  
##  <a name="bkmk_report_authoring_and_deployment"></a>Supporto per la creazione e la distribuzione di report  
 Gli ambienti di creazione di report sono Progettazione report nei progetti di [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] e Generatore report. Gli ambienti di creazione di report forniscono supporto per l'aggiornamento e la progettazione di report, la visualizzazione in anteprima dei report in locale o sul server di report e la distribuzione dei report.  
  
 Nella tabella seguente viene riepilogato il supporto per la creazione e la distribuzione di definizioni di report per le diverse versioni dello schema:  
  
|Ambiente di creazione|Versione di RDL creata|Distribuzione versione RDL|Distribuzione alle versioni del server di report|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|Progettazione report in SQL Server 2014 Data Tools - Business Intelligence per Microsoft Visual Studio 2012, nell'Area download Microsoft.<br /><br /> Oppure<br /><br /> Progettazione report in SQL Server 2012 Data Tools - Business Intelligence per Microsoft Visual Studio 2012, nell'Area download Microsoft.<br /><br /> Oppure<br /><br /> Progettazione report in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools, incluso in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].|Autori 2010 RDL. All'apertura di RDL esistente:<br /><br /> 2000 RDL, aggiornamenti a 2010 RDL<br /><br /> 2005 RDL, aggiornamenti a 2010 RDL<br /><br /> 2008 RDL, aggiornamenti a 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Progettazione report in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio|Autori 2010 RDL. All'apertura di RDL esistente:<br /><br /> 2000 RDL, aggiornamenti a 2010 RDL<br /><br /> 2005 RDL, aggiornamenti a 2010 RDL<br /><br /> 2008 RDL, aggiornamenti a 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Progettazione report in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio|Autori 2008 RDL. All'apertura di RDL esistente:<br /><br /> 2000 RDL, aggiornamenti a 2008 RDL<br /><br /> 2005 RDL, aggiornamenti a 2008 RDL|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Generatore report|Autori 2010 RDL. All'apertura di RDL esistente:<br /><br /> 2000 RDL, aggiornamenti a 2010 RDL<br /><br /> 2005 RDL, aggiornamenti a 2010 RDL<br /><br /> 2008 RDL, aggiornamenti a 2010 RDL|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Progettazione report di Visual Studio RDLC Progettazione report|2005 RDLC|N/D|N/D|  
  
 Per ulteriori informazioni su [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)], vedere quanto segue:  
  
-   [Distribuzione e supporto della versione in SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Microsoft SQL Server Data Tools-Business Intelligence per Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).  
  
##  <a name="bkmk_reportviewer"></a>Controlli ReportViewer  
 Un controllo ReportViewer di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] può visualizzare un report con estensione RDLC in modalità di anteprima locale o in modalità remota, il controllo può visualizzare un file con estensione RDL ospitato in un server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Nella tabella seguente è riportato l'elenco delle versioni di RDL supportate dai controlli ReportViewer per l'elaborazione locale (con estensione RDLC). Il supporto RDL lato server è riepilogato nella sezione [Server di report e supporto dello schema RDL](#bkmk_report_server_rdl_schema_support).  
  
|Controllo ReportViewer nel prodotto|Versione di RDL per l'anteprima locale|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]2013<br /><br /> Oppure<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]2012<br /><br /> Oppure<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> Oppure<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Conversione di file RDLC in file RDL](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [Controlli ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [Aggiunta e configurazione dei controlli ReportViewer](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Report, parti del report e definizioni dei report &#40;Generatore report e SSRS&#41;](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Strumenti di Reporting Services](tools/reporting-services-tools.md)   
 [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
  
