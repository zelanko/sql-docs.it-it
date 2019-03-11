---
title: Novità di Reporting Services (SSRS) | Microsoft Docs
author: markingmyname
ms.author: maghan
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 02/28/2019
ms.openlocfilehash: c2635c764871bb8ff5d97c4c300d5585520db976
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018027"
---
# <a name="whats-new-in-sql-server-reporting-services-ssrs"></a>Novità di SQL Server Reporting Services (SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)]

Informazioni sulle novità di SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Questo argomento illustra le principali aree funzionali e viene aggiornato man mano che vengono rilasciati nuovi elementi.

Per le note sulla versione corrente, vedere [Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md). 

Per informazioni su Server di report di Power BI, vedere [Che cos'è Server di report di Power BI?](https://docs.microsoft.com/power-bi/report-server/get-started).

**Scarica** ![download](../analysis-services/media/download.png "download")

Per scaricare SQL Server 2017 Reporting Services, accedere all'**[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=55252)**.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-preview-reporting-services"></a>Anteprima di SQL Server 2019 Reporting Services

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Reporting Services non è disponibile per CTP 2.3. Installare la versione corrente, [SQL Server 2017 Reporting Services](install-windows/install-reporting-services.md).
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="ssrs-2017"></a>SSRS 2017

### <a name="comments-on-reports"></a>Commenti nei report

I commenti sono ora disponibili per i report per una maggior prospettiva e collaborazione con altri utenti. È anche possibile includere allegati nei commenti.

![Commenti all'interno di un server di report](media/what-s-new-in-sql-server-reporting-services-ssrs/report-server-comments.png)

Per altre informazioni, vedere [Add comments to a report in a report server](https://powerbi.microsoft.com/documentation/reportserver-add-comments/) (Aggiungere commenti a un report in un server di report).

### <a name="dax-queries-in-reporting-tools"></a>Query DAX negli strumenti di report

Nelle versioni più recenti di Generatore Report e SQL Server Data Tools è possibile creare query DAX native nei modelli di dati tabulari di SQL Server Analysis Services supportati trascinando i campi desiderati nelle finestre di progettazione delle query. Vedere il [blog di Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

### <a name="rest-api-support"></a>Supporto delle API REST

Per consentire lo sviluppo di applicazioni e personalizzazioni moderne, SQL Server Reporting Services ora supporta completamente un'API RESTful conforme a OpenAPI. La documentazione e le specifiche complete dell'API sono ora disponibili in [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0).

### <a name="query-designer-support-for-dax-now-in-report-builder-and-sql-server-data-tools"></a>Supporto della progettazione query per DAX in Generatore Report ed SQL Server Data Tools

In Generatore Report e SQL Server Data Tools è ora possibile creare query DAX native nei modelli di dati tabulari di SQL Server Analysis Services supportati. È possibile usare la progettazione query in entrambi gli strumenti per trascinare i campi voluti e generare la query DAX automaticamente anziché scriverla manualmente.  
 
Altre informazioni nel [blog di Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

* Scaricare [Generatore report di Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=734968).
* Scaricare [SQL Server Data Tools (versione finale candidata)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate).

> **Nota**: è possibile usare la progettazione query per DAX solo con le origini dati tabulari SSAS incorporate in SQL Server 2016 e versioni successive.
::: moniker-end
 
## <a name="ssrs-2016"></a>SSRS 2016
  
### <a name="reporting-services-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  
 È disponibile un nuovo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] is available. Si tratta di un portale aggiornato e moderno, che include gli indicatori KPI, i report per dispositivi mobili, i report impaginati e i file di Excel e Power BI Desktop. Il [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] sostituisce Gestione Report delle versioni precedenti. È anche possibile scaricare Mobile Report Publisher e Generatore Report dal [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] senza bisogno della tecnologia ClickOnce.
 
 Per creare report per dispositivi mobili, sarà necessario usare [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short.md)].  
  
 Per altre informazioni sul [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)], vedere [Portale Web (modalità nativa SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).  
  
 ![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  
 
 #### <a name="custom-branding-for-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Personalizzazione del [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 
  È possibile personalizzare il [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] con il logo e i colori dell'organizzazione mediante un pacchetto di personalizzazione.  
  
  Per altre informazioni sulla personalizzazione, vedere [Personalizzazione del portale Web](https://msdn.microsoft.com/6dac97f7-02a6-4711-81a3-e850a6b40bf1)
 
 #### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Indicatori di prestazioni chiave (KPI) nel [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 

È possibile creare indicatori KPI direttamente nel [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] , contestuali alla cartella corrente. Durante la creazione di indicatori KPI, è possibile scegliere i campi del set di dati e riepilogare tali valori. È anche possibile selezionare il contenuto correlato per eseguire il drill-through a ulteriori dettagli.
  
 ![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)
 
 Per altre informazioni, vedere [Utilizzo degli indicatori KPI nel portale Web](https://msdn.microsoft.com/a28cf500-6d47-4268-a248-04837e7a09eb)
  
 
 ### <a name="mobile-reports"></a>Report per dispositivi mobili
 
I report per dispositivi mobili di Reporting Services sono report dedicati, ottimizzati per una vasta gamma di fattori di forma, e forniscono un'esperienza ottimale agli utenti che accedono ai report dai dispositivi mobili. Offrono un'ampia serie di visualizzazioni, ad esempio grafici temporali, di categorie e di confronto, mappe ad albero e mappe personalizzate. È possibile connettere i report per dispositivi mobili a una gamma di origini dati, tra cui dati locali tabulari e multidimensionali di SQL Server Analysis Services. I report per dispositivi mobili possono essere disposti in un'area di progettazione con righe e colonne della griglia regolabili ed elementi flessibili che si adattano in modo ottimale agli schermi di qualsiasi dimensione. È quindi possibile salvare i report per dispositivi mobili in un server di Reporting Services, visualizzarli e interagire con essi in un browser o nell'app Power BI per dispositivi mobili su iPad, iPhone, telefoni Android e dispositivi Windows 10.
  
#### <a name="mobile-report-publisher"></a>Mobile Report Publisher  
 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]consente di creare e pubblicare report per dispositivi mobili di SQL Server nel [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)].  
  
 ![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  
  
 Per altre informazioni, vedere [Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).  
  
#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Report per dispositivi mobili di SQL Server ospitati in Reporting Services disponibili nell'app per dispositivi mobili di Power BI  
 L'app Power BI per dispositivi mobili per iOS su iPad e iPhone può ora visualizzare i report per dispositivi mobili di SQL Server ospitati nel server di report locale.  
  
 ![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  
  
 Non è possibile connettersi per impostazione predefinita senza modificare la configurazione. Per altre informazioni su come consentire all'app per dispositivi mobili di Power BI di connettersi al server di report, vedere [Abilitare un server di report per l'accesso a Power BI per dispositivi mobili](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md).
  
### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>Supporto per la modalità SharePoint e SharePoint 2016  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta l'integrazione con SharePoint 2013 e SharePoint 2016.
 
Per altre informazioni, vedere:  
  
-   [Combinazioni supportate di SharePoint, server Reporting Services e componente aggiuntivo &#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
-   [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Installare la modalità SharePoint di Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Supporto per Microsoft .NET Framework 4  
 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] supporta le versioni correnti di Microsoft .NET Framework 4. incluse le versioni 4.0 e 4.5.1. Se non è installata alcuna versione di .NET Framework 4.x, il programma di installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installa .NET 4.0 durante il passaggio di installazione delle funzionalità.  

### <a name="report-improvements"></a>Miglioramenti dei report

**Motore di rendering HTML5:** è disponibile un nuovo motore di rendering HTML5 ottimale per la modalità con standard "completi" per il Web e i browser moderni.  Il nuovo motore di rendering non si basa più su modalità particolari usate da alcuni browser meno recenti.
  
 Per altre informazioni sul supporto dei browser, vedere [Supporto browser per Reporting Services e Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  

**Report moderni impaginati:** è possibile progettare report impaginati moderni accattivanti con nuovi stili attuali per grafici, misuratori, mappe e altre visualizzazioni dei dati.
  
**Mappa ad albero e grafici radiali:** è possibile ottimizzare i report con la mappa ad albero ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") e i grafici radiali ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon"), strumenti eccezionali per la visualizzazione dei dati gerarchici. Per altre informazioni, vedere [Tree Map and Sunburst Charts in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md).  

**Incorporamento di report:** è ora possibile incorporare report per dispositivi mobili e report impaginati in altre pagine Web e applicazioni usando un iframe e i parametri URL.  

**Aggiungere elementi di un report a un dashboard di Power BI:** quando si visualizza un report nel [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], è possibile selezionare elementi del report e aggiungerli a un dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].   Gli elementi che è possibile aggiungere sono i grafici, i pannelli dei misuratori, le mappe e le immagini. È possibile **(1)** selezionare il gruppo contenente il dashboard in cui si intende aggiungere l’elemento, **(2)** selezionare il dashboard a cui si intende aggiungere l’elemento e **(3)** selezionare la frequenza con cui si desidera che il riquadro venga aggiornato nel dashboard.   ![nota](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") L'aggiornamento è gestito dalle sottoscrizioni di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e, dopo l'aggiunta dell'elemento, è possibile modificare la sottoscrizione e configurare un'altra pianificazione dell'aggiornamento.  
  
 ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 
  
 Per altre informazioni, vedere [Integrazione del server di report di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) e [Aggiungere elementi di Reporting Services ai dashboard di Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).  
 
 **Rendering ed esportazione in PowerPoint:** il formato Microsoft PowerPoint (PPTX) è una nuova estensione per il rendering di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. È possibile esportare report in formato PPTX dalle applicazioni consuete, ovvero Generatore report, Progettazione report (in SSDT) e dal [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Ad esempio, la figura seguente mostra il menu di esportazione dal [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. 
  
 ![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 
  
 È anche possibile selezionare il formato PPTX per l'output della sottoscrizione e usare l'accesso URL del server di report per eseguire il rendering e l'esportazione di un report. Ad esempio, il comando URL seguente nel browser esporta un report da un'istanza denominata del server di report.  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Per altre informazioni, vedere [Export a Report Using URL Access](../reporting-services/export-a-report-using-url-access.md).  
 
 **PDF sostituisce ActiveX per la stampa remota:** l'esperienza di stampa ActiveX tramite la barra degli strumenti del visualizzatore di report è stata sostituita da un'esperienza moderna basata su PDF idonea a tutti i browser supportati, incluso Microsoft Edge. Non è più necessario scaricare controlli ActiveX. In base al browser usato e alle applicazioni e ai servizi di visualizzazione di file PDF installati, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] aprirà una finestra di dialogo di stampa per stampare il report o richiederà di scaricare un file PDF del report.  In qualità di amministratore, si può comunque disabilitare la stampa lato client da [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Per altre informazioni, vedere [Abilitare e disabilitare la stampa sul lato client per Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).

![ssrs-pdf-printing](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>Miglioramenti alle sottoscrizioni  
 
|Funzionalità|Modalità server supportata|  
|-------------|---------------------------|  
|**Abilitare e disabilitare le sottoscrizioni**. Sono disponibili nuove opzioni dell'interfaccia utente per disabilitare e abilitare rapidamente le sottoscrizioni. Le sottoscrizioni disabilitate mantengono le rispettive proprietà di configurazione, ad esempio la pianificazione, e possono essere abilitate con facilità.<br /><br /> ![ssrs-enable-disable-subscriptions](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> Per altre informazioni, vedere [Disable or Pause Report and Subscription Processing](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).|Modalità nativa|  
|**Descrizione della sottoscrizione**. Quando si crea una nuova sottoscrizione, è ora possibile includere una descrizione del report come parte delle proprietà della sottoscrizione. La descrizione viene inclusa nella pagina di riepilogo della sottoscrizione.|Modalità SharePoint e nativa|  
|**Cambiare il proprietario della sottoscrizione**. L'interfaccia utente migliorata consente di cambiare rapidamente il proprietario di una sottoscrizione. Le versioni precedenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] consentono agli amministratori di cambiare i proprietari di una sottoscrizione usando uno script. A partire dalla versione [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , è possibile cambiare i proprietari della sottoscrizione usando l'interfaccia utente o uno script. Il cambiamento del proprietario della sottoscrizione è un'attività amministrativa comune quando gli utenti lasciano l'organizzazione o cambiano ruolo all'interno di essa.|Modalità SharePoint e nativa|  
|**Credenziali condivise per sottoscrizioni con condivisioni file**. Sono ora disponibili due flussi di lavoro con le sottoscrizioni con condivisioni file di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :<br /><br /> A partire da questa versione, l'amministratore di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] può configurare un singolo account di condivisione file, usato per una o più sottoscrizioni. L'account di condivisione file viene configurato in modalità nativa di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] mediante **Specificare un account di condivisione file**in Gestione configurazione e quindi gli utenti selezionano **Usa l'account di condivisione file**nella pagina di configurazione della sottoscrizione.<br /><br /> È possibile configurare singole sottoscrizioni con credenziali specifiche per la condivisione file di destinazione.<br /><br /> È anche possibile combinare i due approcci e fare in modo che alcune sottoscrizioni con condivisioni file usino l'account di condivisione file centrale, mentre altre sottoscrizione usano credenziali specifiche.|Modalità nativa|  

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
 La nuova versione di SSDT include i modelli di progetto per [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]: Creazione guidata progetto server di report e Progetto server di report. Per informazioni sul download di SSDT, vedere [SQL Server Data Tools per Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=827542).  

### <a name="report-builder-improvements"></a>Miglioramenti di Generatore report

**Nuova interfaccia utente di Generatore report:** l'interfaccia utente di base di [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] ha ora un aspetto moderno grazie a elementi semplificati per l'interfaccia utente.  
  
|||  
|-|-|  
|Nuovo|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**Personalizzazione del riquadro Parametri:** è ora possibile personalizzare il riquadro Parametri. Usando l'area di progettazione in Generatore report, è possibile trascinare un parametro in una colonna e in una riga specifiche del riquadro Parametri. È possibile aggiungere e rimuovere colonne per modificare il layout del riquadro.   Per altre informazioni, vedere [Personalizzare il riquadro dei parametri in un report &#40;Generatore report&#41;](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
 ![Elenco di parametri nel riquadro dei dati del report e nel riquadro dei parametri](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "Elenco di parametri nel riquadro dei dati del report e nel riquadro dei parametri")  

  
**Supporto per valori DPI alti:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] supporta il ridimensionamento e i dispositivi con valori DPI alti.  Per altre informazioni sui valori DPI alti, vedere le pagine seguenti:  
  
-   [Windows 8.1 DPI Scaling Enhancements](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  
  
-   [Valori DPI alti e Windows 8.1](https://technet.microsoft.com/library/dn528848.aspx)  

## <a name="next-steps"></a>Passaggi successivi

[Novità di Analysis Services](https://msdn.microsoft.com/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
[Compatibilità con le versioni precedenti](reporting-services-backward-compatibility.md)   
[Funzionalità di Reporting Services supportate dalle edizioni di SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)   
[Eseguire l'aggiornamento e la migrazione di Reporting Services](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
