---
title: Distribuzione e supporto della versione in SQL Server Data Tools (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c488316c1eaed822685577356e9df6f0cad9d174
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100359"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssrs"></a>Deployment and Version Support in SQL Server Data Tools (SSRS)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] supporta gli scenari seguenti:  
  
-   Apertura delle definizioni dei report (*.rdl) e dei progetti server di report (\*.rptproj).  
  
-   Compilazione delle definizioni di report.  
  
-   Visualizzazione in anteprima dei report in Progettazione report.  
  
-   Distribuzione dei report nei server di report.  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> Proprietà di configurazione e distribuzione  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] supporta le configurazioni di progetto. Una configurazione di progetto è costituita da un set di proprietà che consentono di specificare percorsi e comportamenti quando un progetto viene compilato come passaggio nella visualizzazione in anteprima o nella distribuzione dei report. Per ulteriori informazioni sulle configurazioni di progetto, vedere la documentazione di Visual Studio.  
  
 Utilizzare le configurazioni di progetto per controllare l'aggiornamento delle definizioni di report alle versioni dello schema compatibili con i server di report di destinazione. Le proprietà controllate dalle configurazioni di progetto includono il server di report di destinazione, la cartella in cui il processo di compilazione consente di archiviare temporaneamente le definizioni di report per l'anteprima e la distribuzione, nonché i livelli di errore.  
  
 I report vengono compilati prima di essere sottoposti a rendering come anteprime in Progettazione report o di essere distribuiti nel server di report.  
  
 È possibile impostare le proprietà di configurazione nella finestra di dialogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **di** .  
  
 Nelle proprietà di compilazione e distribuzione è incluso quanto segue:  
  
-   OutputPath è una proprietà di compilazione che identifica il percorso delle cartelle per archiviare la definizione del report usata nella verifica della compilazione, nella distribuzione e nell'anteprima dei report.  
  
-   ErrorLevel è una proprietà di compilazione che identifica la gravità dei problemi di compilazione segnalati come errori. I problemi con livelli di gravità minori o uguali al valore di ErrorLevel vengono segnalati come errori; in caso contrario, vengono segnalati come avvisi. Per altre informazioni, vedere la sezione "Convalida del report e livelli di errore" di [Progettare report con Progettazione report &#40;SSRS&#41;](design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
-   TargetServerVersion è una proprietà di distribuzione che consente di identificare la versione prevista di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installata nel server di report di destinazione specificato nella proprietà TargetServerURL.  
  
 Quando si specifica la versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella finestra di dialogo **Proprietà progetto** , non vengono ripristinati automaticamente i report di questa versione. Di conseguenza, un progetto server di report può contenere report delle due diverse versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando il progetto server di report viene distribuito, tutti i report presenti nel progetto vengono convertiti nella versione specificata in TargetServerVersion.  
  
 È possibile aggiungere più di una configurazione di progetto a un progetto; ognuna viene utilizzata per uno scenario differente, ad esempio la distribuzione in versioni diverse di server di report. Per altre informazioni, vedere [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md) e [Finestra di dialogo Pagine delle proprietà del progetto](project-property-pages-dialog-box.md).  
  
##  <a name="bkmk_SupportedVersions"></a> Versioni supportate  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], l'ambiente di sviluppo a 32 bit per progetti server di report, non è progettato per l'esecuzione in computer basati su [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]e non può essere installato nei server basati su [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]. Tuttavia, è possibile usare [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] in computer con processore x64.  
  
 Nella tabella seguente sono descritte le versioni supportate per la creazione e la pubblicazione di report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Lo schema non è stato cambiato fin da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
|Tipo di progetto o file|Version|Creazione di report|Pubblicazione di report|Note|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|Progetto server di report<br /><br /> o Gestione configurazione<br /><br /> Progetto Creazione guidata report|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Schema RDL 2014|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Progetto server di report<br /><br /> oppure<br /><br /> Progetto Creazione guidata report|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Schema RDL 2012|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Progetto server di report<br /><br /> o Gestione configurazione<br /><br /> Progetto Creazione guidata report|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Schema RDL 2008 R2|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Progetto server di report<br /><br /> oppure<br /><br /> Progetto Creazione guidata report|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Schema RDL 2008|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] solo server di report|Aggiornamenti dello schema da RDL 2003 e RDL 2005 a RDL 2008 in locale.|  
|Progetto server di report<br /><br /> o Gestione configurazione<br /><br /> Progetto Creazione guidata report|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Schema RDL 2005|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oppure [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server di report||  
|Progetto server di report|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|Schema RDL 2003|Non supportato||  
|Progettazione report RDLC [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|Schema RDL 2005|Non supportato|Lo schema RDL 2008 non è supportato.|  
|Controlli dei visualizzatori di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|RDL 2008 non supportato in modalità locale|N/D|Consente di visualizzare i report RDL 2008 nel server di report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità server.|  
  
 Per altre informazioni sull'apertura di report in una versione precedente dello schema di definizione del report, vedere [Aggiornare i report](../install-windows/upgrade-reports.md). Per ulteriori informazioni su schemi di definizione dei report specifici, vedere la pagina relativa alla [specifica del linguaggio RDL](https://go.microsoft.com/fwlink/?linkid=116865).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di origini dati e report](../reports/publishing-data-sources-and-reports.md)  
  
  
