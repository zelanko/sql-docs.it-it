---
title: Pianificazione per Reporting Services e supporto Browser per Power View (Reporting Services 2014) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- scripts [Reporting Services], requirements
- viewing reports
- browsers [Reporting Services]
- Web browsers [Reporting Services], about browser support
- browsing reports [Reporting Services]
- components [Reporting Services], browsers
- Web browsers [Reporting Services]
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c1f1b4d74d7ad7f34254a5c56c6dafc5fd2fb829
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350498"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>Pianificazione per il supporto browser per Reporting Services e Power View (Reporting Services 2014)
  In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] viene usato un Web browser per visualizzare i report ed eseguire Gestione report. Solo alcuni browser supportano tutte le funzionalità report. In questo argomento viene descritto il supporto e i requisiti per le funzionalità di gestione di Gestione report, per la visualizzazione dei report e i comandi del visualizzatore di report in Visual Studio. Viene inoltre riepilogata la disponibilità delle funzionalità per i browser supportati, i requisiti di autenticazione e i requisiti di script.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** Modalità SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] | Modalità nativa di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
 **Contenuto dell'argomento**  
  
-   [Scenari del Browser Power View](#bkmk_powerview)  
  
-   [Requisiti del Browser tramite Gestione report (modalità nativa)](#bkmk_reportmanager)  
  
-   [Requisiti del browser per visualizzare i report](#bkmk_reportviewer)  
  
-   [Requisiti di autenticazione](#bkmk_authentication)  
  
-   [Supporto browser per controlli Server Web ReportViewer in Visual Studio](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a> Scenari del Browser Power View  
 L'elenco di browser supportati e di versioni di browser supportate da [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] dipende dal tipo di documento aperto. Le cartelle di lavoro di Excel 2013 e "**rdlx**" file di utilizzano i diversi componenti.  
  
|Tipo di documento|Ambiente|Supporto browser|  
|-------------------|-----------------|---------------------|  
|Report Power View (RDLX)|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] in modalità integrata SharePoint per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e l'applicazione Web Power View.|Vedere [Power View in SharePoint Server e modalità integrata SharePoint per Reporting Services](#bkmk_powerview_on_SSRS).|  
|Cartella di lavoro di Excel 2013 con fogli di lavoro di Power View|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] in Excel Services.<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] nell'applicazione Web di Excel.|Vedere [Power View in Excel Services o Excel Web App in SharePoint Online](#bkmk_powerview_on_ExcelServices).|  
  
###  <a name="bkmk_powerview_on_SSRS"></a> Power View in SharePoint Server e modalità integrata SharePoint di Reporting Services  
 Nella tabella seguente sono riepilogate le versioni di browser supportate per [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] quando un utente apre il report Power View (RDLX) in una farm di SharePoint con un'applicazione di servizio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per SharePoint installato e configurato.  
  
-   La tabella è valida per SharePoint 2010 e SharePoint 2013.  
  
-   Per altre informazioni sul supporto browser per SharePoint 2013, vedere [pianificare il supporto browser in SharePoint 2013](https://technet.microsoft.com//library/cc263526\(office.15\).aspx) (https://technet.microsoft.com/library/cc263526(office.15).aspx).  
  
-   Per altre informazioni sul supporto browser per SharePoint 2010, vedere [pianificare il supporto browser (SharePoint Server 2010)](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) (https://technet.microsoft.com/library/cc263526(office.14).aspx).  
  
|**Browser**|**Windows 8 e 8.1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 10 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 9**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|  
|**Internet Explorer 8**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|  
|**Mozilla Firefox (ultima versione pubblicamente rilasciata)**|32 bit|32 bit|32 bit|32 bit|32 bit|Non supportato|  
|**Apple Safari (ultima versione pubblicamente rilasciata)**|Non supportato|Non supportato|Non supportato|Non supportato|Non supportato|32 bit, 64 bit|  
  
> [!NOTE]  
>  "32 bit" si riferisce al browser, non al sistema operativo. È possibile, ad esempio, utilizzare Internet Explorer 9 a 32 bit in Windows 7 a 64 bit.  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Funzionalità InPrivate Browsing in Internet Explorer  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] non supporta la funzionalità InPrivate Browsing in [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 e Internet Explorer 9. Per altre informazioni su InPrivate Browsing, vedere l'articolo che [spiega cos'è InPrivate Browsing](http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (http://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a> Power View in Excel Services o Excel Web App in SharePoint Online  
 Nella tabella seguente sono riepilogate le versioni di browser supportate per [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] quando un utente apre una cartella di lavoro di Excel 2013 con fogli di Power View in SharePoint Server in cui è in esecuzione Excel Services:  
  
-   Per altre informazioni sul supporto browser per SharePoint 2013, vedere [pianificare il supporto browser in SharePoint 2013](https://technet.microsoft.com/library/cc263526\(office.15\).aspx) (https://technet.microsoft.com/library/cc263526(office.15).aspx).  
  
|**Browser**|**Windows 8 e 8.1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 10 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 9**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|  
|**Internet Explorer 8**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|  
|**Mozilla Firefox (ultima versione pubblicamente rilasciata)**|32 bit|32 bit|32 bit|32 bit|32 bit|32 bit, 64 bit|  
|**Apple Safari (ultima versione pubblicamente rilasciata)**|Non supportato|Non supportato|Non supportato|Non supportato|Non supportato|32 bit, 64 bit|  
|**Google Chrome (ultima versione pubblicamente rilasciata)**|32 bit **(\*)** per periodo di tempo limitato|32 bit **(\*)** per periodo di tempo limitato|32 bit **(\*)** per periodo di tempo limitato|32 bit **(\*)** per periodo di tempo limitato|32 bit **(\*)** per periodo di tempo limitato|Non supportato|  
  
 **(\*)** Chrome interromperà il supporto di Netscape plug-in di API (NPAPI) usato da Silverlight. Power View dipende da Silverlight.  Per altre informazioni, vedere [The Final Countdown for NPAPI](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html).  
  
##  <a name="bkmk_reportmanager"></a> Requisiti del Browser tramite Gestione report (modalità nativa)  
 Di seguito è riportato l'elenco corrente dei browser supportati che è possibile utilizzare per eseguire Gestione report in modalità nativa di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per gestire i report e il server di report.  
  
|Browser|  
|-------------|  
|Internet Explorer 7 o versioni successive, con l'opzione per l'esecuzione di script abilitata.|  
|Mozilla FireFox (ultima versione pubblicamente rilasciata)|  
|Apple Safari (ultima versione pubblicamente rilasciata)|  
|Google Chrome (ultima versione pubblicamente rilasciata)|  
  
##  <a name="bkmk_reportviewer"></a> Requisiti del browser per visualizzare i report  
 Di seguito è riportato l'elenco corrente delle funzionalità e dei browser supportati con il visualizzatore di report. Il visualizzatore di report supporta la visualizzazione dei report da Gestione report e dalle raccolte di SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|**Browser**|**Windows 8 e 8.1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|**iOS 6-7 per iPad**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|Non supportato|Non supportato|  
|**Internet Explorer 10 (per il desktop)**|32 bit, 64 bit|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|Non supportato|Non supportato|  
|**Internet Explorer 9**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 8**|Non supportato|32 bit, 64 bit|Non supportato|32 bit, 64 bit|32 bit, 64 bit|Non supportato|Non supportato|  
|**Internet Explorer 7**|Non supportato|Non supportato|Non supportato|Non supportato|32 bit, 64 bit|Non supportato|Non supportato|  
|**Mozilla Firefox (ultima versione pubblicamente rilasciata)**|32 bit|32 bit|32 bit|32 bit|32 bit|Non supportato|Non supportato|  
|**Apple Safari (ultima versione pubblicamente rilasciata)**|Non supportato|Non supportato|Non supportato|Non supportato|Non supportato|32 bit, 64 bit|Supportato con funzionalità limitate <sup>(1)</sup>|  
|**Google Chrome (ultima versione pubblicamente rilasciata)**|32 bit|32 bit|32 bit|32 bit|32 bit|Non supportato|Non supportato|  
  
 **<sup>(1)</sup>**  Sono supportate le funzionalità seguenti:  
  
-   Esportazione in formato PDF e TIFF.  
  
-   Visualizzare in modo interattivo i report in Apple Safari nei dispositivi di iOS. Tra le funzionalità supportate sono incluse l'espansione e la compressione, il riquadro dei parametri e l'ordinamento interattivo.  
  
-   Per altre informazioni, vedere [visualizzazione report di Reporting Services su dispositivi Microsoft Surface e Apple iOS](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md).  
  
 **Nota** Se si accede a un server di report da un computer Macintosh, è consigliabile utilizzare Safari. Se si utilizza un prodotto SharePoint integrato con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Pianificare il supporto browser (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkId=183583).  
  
### <a name="url-access-for-viewing-reports"></a>Accesso con URL per la visualizzazione di report  
 Per visualizzare direttamente i report, anziché tramite Gestione report, è possibile utilizzare l'accesso con URL per creare un collegamento al report e al visualizzatore di report. L'accesso con URL supporta un'ampia gamma di browser.  
  
 Per ulteriori informazioni sull'accesso con URL, vedere l'argomento seguente:  
  
-   [Riferimento ai parametri di accesso con URL](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a> Requisiti di autenticazione  
 I browser supportano schemi di autenticazione specifici che devono essere gestiti dal server di report affinché la richiesta del client abbia esito positivo. Nella tabella seguente sono indicati i tipi di autenticazione predefiniti supportati da ogni browser eseguito in un sistema operativo Windows.  
  
|**Tipo di browser**|**Supporti**|**Impostazione predefinita del browser**|**Impostazione predefinita del server**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|Negoziata, Kerberos, NTLM o di base|Negotiate|Sì. Le impostazioni di autenticazione predefinite funzionano con Internet Explorer.|  
|**Firefox**|NTLM, Basic|NTLM|Sì. Le impostazioni di autenticazione predefinite funzionano con Firefox.|  
|**Safari**|Basic|Basic|Sì. Le impostazioni di autenticazione predefinite funzionano con Safari.|  
|**Chrome**|Negoziata, NTLM o di base|Negoziata|Sì. Le impostazioni di autenticazione predefinite funzionano con Chrome.|  
  
### <a name="script-requirements"></a>Requisiti di script  
 Per utilizzare il visualizzatore di report, configurare il browser per l'esecuzione di script.  
  
 Se lo scripting non è abilitato, all'apertura di un report verrà visualizzato un messaggio di errore simile al seguente:  
  
-   **Il browser in uso non supporta gli script oppure è stato configurato in modo da non consentire l'esecuzione di script. Fare clic qui per visualizzare il report senza script**.  
  
 Se si sceglie di visualizzare il report senza il supporto per gli script, il report verrà sottoposto a rendering in HTML senza le funzionalità del visualizzatore di report, quali la barra degli strumenti per report e la mappa documento.  
  
> [!NOTE]  
>  La barra degli strumenti report fa parte del componente Visualizzatore HTML. Per impostazione predefinita la barra degli strumenti viene visualizzata nella parte superiore di ogni report di cui viene eseguito il rendering in una finestra del browser. Nel visualizzatore di report sono disponibili funzionalità tramite cui è possibile eseguire ricerche di informazioni nel report, scorrere fino a una pagina specifica e adattare le dimensioni della pagina per la visualizzazione. Per ulteriori informazioni sulla barra degli strumenti per report o sul Visualizzatore HTML, vedere [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md).  
  
##  <a name="bkmk_controls"></a> Supporto browser per controlli Server Web ReportViewer in Visual Studio  
 Il controllo server Web ReportViewer è utilizzato per incorporare la funzionalità del report in un'applicazione Web ASP.NET. I controlli sono inclusi con Visual Studio e supportano browser diversi e versioni di browser differenti rispetto agli altri componenti descritti in questo argomento. Il tipo di browser utilizzato per visualizzare l'applicazione determina il tipo di funzionalità di ReportViewer che è possibile fornire nell'applicazione. Utilizzare la tabella fornita in questo argomento per determinare quali browser supportati sono soggetti a restrizioni di funzionalità e quali piattaforme sono supportate.  
  
 A causa delle differenze nei motori di rendering dei browser supportati, è possibile che alcune funzionalità avanzate del report siano visualizzate in modo diverso nei vari browser.  Ad esempio, la rotazione del testo.  
  
### <a name="scripting-requirements"></a>Requisiti di script  
 Utilizzare un browser in cui il supporto per gli script è abilitato. Se il browser non può eseguire script, non è possibile visualizzare il report.  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>Requisiti del browser per la visualizzazione dei report con i controlli server Web ReportViewer  
 Il supporto delle funzionalità del report interattive varia in base al tipo di browser. La matrice del supporto seguente mostra quali tipi di browser sono supportati e le relative piattaforme, I tipi soggetti a vincoli sono indicati nella colonna Note.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**Browser**|**Windows 8** e **Windows 8.1**|**Windows 7**|**Windows Server 2012** e **2012 R2**|**Windows Server 2008** e **2008 R2**|**Windows Server 2003**|**Mac OS X 10.6-10.9**|**Note**|  
|**Internet Explorer 11 (per il desktop**|Yes|Yes|Yes|Non supportato|Non supportato|Non supportato|Internet Explorer supporta il set completo di funzionalità ReportViewer.|  
|**Internet Explorer 10 (per il desktop)**|Yes|Yes|Yes|Non supportato|Non supportato|Non supportato|Internet Explorer supporta il set completo di funzionalità ReportViewer.|  
|**Internet Explorer 9**|Non supportato|Yes|Non supportato|Yes|Yes|Yes|Internet Explorer supporta il set completo di funzionalità ReportViewer.|  
|**Internet Explorer 8.0**|Non supportato|Yes|Non supportato|Yes|Sì<sup>1</sup>|Non supportato|Internet Explorer supporta il set completo di funzionalità ReportViewer. <sup>1</sup>|  
|**Internet Explorer 7.0**|Non supportato|Yes|Non supportato|Yes|Sì<sup>1</sup>|Non supportato|Internet Explorer supporta il set completo di funzionalità ReportViewer. <sup>1</sup>|  
|**Firefox (ultima versione pubblicamente rilasciata)**|Yes|Yes|Yes|Yes|Yes|Non supportato|La stampa e lo zoom non sono supportati.|  
|**Safari (ultima versione pubblicamente rilasciata)**|Non supportato|Non supportato|Non supportato|Non supportato|Non supportato|Yes|La stampa e lo zoom non sono supportati.<br /><br /> Il controllo di calendario utilizzato per selezionare date in un report con parametri è disabilitato in questo browser. È necessario che gli utenti digitino manualmente le date desiderate nell'area di richiesta parametri.|  
|**Chrome (ultima versione pubblicamente rilasciata)**|Yes|Yes|Yes|Yes|Yes|Non supportato|La stampa e lo zoom non sono supportati.|  
  
 <sup>1</sup>nella modalità degli standard, Internet Explorer 7.0 e 8.0 non vengono visualizzate le righe inclinate nei report. Se si utilizzano righe inclinate nei report, impostare la pagina ASP.NET per essere eseguita in modalità non standard in Internet Explorer. A tale scopo, trovare il \<! Tipo di documento > tag nella pagina ASP.NET. In alternativa, se si utilizza una pagina master, è possibile trovare il tag nel file con estensione master. Il tag è simile al seguente:  
  
```  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```  
  
 Sostituire il \<! Tipo di documento > tag con il seguente tag:  
  
```  
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```  
  
 Per altre informazioni sulle modalità di compatibilità in Internet Explorer, vedere [definizione della compatibilità del documento](https://go.microsoft.com/fwlink/?LinkId=180380) (https://go.microsoft.com/fwlink/?LinkId=180380).  
  
 Per altre informazioni sull'uso dei controlli ReportViewer, vedere [distribuzione di controlli Reports e ReportViewer](https://msdn.microsoft.com/library/ms251723.aspx) (https://msdn.microsoft.com/library/ms251723.aspx).  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di Reporting Services](tools/reporting-services-tools.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visualizzatore HTML e barra degli strumenti Report](html-viewer-and-the-report-toolbar.md)   
 [Riferimento ai parametri di accesso con URL](url-access-parameter-reference.md)  
  
  
