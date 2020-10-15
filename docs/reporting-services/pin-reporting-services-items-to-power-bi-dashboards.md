---
title: Aggiungere elementi del report impaginato ai dashboard di Power BI - Reporting Services | Microsoft Docs
ms.date: 01/14/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: È possibile aggiungere elementi del report impaginato di Reporting Services in locale a un dashboard nel servizio Power BI come nuovo riquadro.
ms.topic: conceptual
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6fbf2020d22994fdf214c7e869368c20b7b40cf7
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891841"
---
# <a name="pin-reporting-services-paginated-report-items-to-dashboards-in-power-bi"></a>Aggiungere elementi del report impaginato di Reporting Services ai dashboard in Power BI

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

È possibile aggiungere l'elemento di un report impaginato di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in locale a un dashboard nel servizio [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] come nuovo riquadro.   Per aggiungere elementi, l'amministratore deve innanzitutto integrare il server di report con Azure Active Directory e [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
##  <a name="requirements-to-pin"></a><a name="bkmk_requirements_to_pin"></a> Requisiti per l'aggiunta  
  
-   Il server di report è configurato per l'integrazione di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] . Per altre informazioni, vedere [Integrazione del server di report e di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md). Se il server di report non è stato configurato, il pulsante **Aggiungi al dashboard di Power BI** non verrà visualizzato nella barra degli strumenti del Visualizzatore report.  
  
     ![barra degli strumenti del Visualizzatore report](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   Aggiungere elementi dal Visualizzatore report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nel [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], ad esempio, `https://myserver/Reports`.  Non è possibile aggiungere elementi da [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], da Progettazione report in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o da un URL del server di report.  Ad esempio, `https://myserver/ReportServer`.  
  
-   È necessario configurare il browser per consentire i popup dal sito del server di report.  
  
-   Se si vuole aggiornare l'elemento aggiunto, è necessario configurare i report per le credenziali archiviate.  Quando si aggiunge un elemento, viene creata automaticamente una sottoscrizione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per gestire l'aggiornamento dei dati dell'elemento nel dashboard.  Se il report non usa le credenziali archiviate, quando viene eseguita la sottoscrizione verrà visualizzato un messaggio simile al seguente nella pagina **Sottoscrizioni personali**.  
  
    "Errore di recapito di Power BI: dashboard: Esempio di analisi della spesa IT, oggetto visivo: Chart2, errore: Impossibile completare l'azione corrente. Le credenziali per l'origine dati utente non soddisfano i requisiti per eseguire il report o il set di dati condiviso. Le credenziali per l'origine dati utente..."
 
    Vedere la sezione "Configurare le credenziali archiviate per un'origine dati specifica del report (modalità nativa)" di [Archiviare le credenziali in un'origine dati di Reporting Services](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).  
  
##  <a name="items-you-can-pin"></a><a name="bkmk_supported_items"></a> Elementi che è possibile aggiungere  
 I seguenti elementi del report possono essere aggiunti a un dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  Non è possibile aggiungere elementi annidati all'interno di un'area dati. Ad esempio, non è possibile aggiungere un elemento annidato all'interno di una tabella o un elenco di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Grafici  
-   Pannelli dei misuratori  
-   Mappe  
-   Immagini  
-   Gli elementi devono far parte del corpo del report.  Non è possibile aggiungere elementi presenti nell'intestazione o nel piè di pagina.  
-   È possibile aggiungere singoli elementi presenti all'interno di un rettangolo di livello superiore, ma non come unico gruppo.  
  
##  <a name="to-pin-a-report-item"></a><a name="bkmk_to_pin"></a> Per aggiungere un elemento del report  
  
1. Verificare di aver eseguito l'accesso a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] selezionare la voce di menu **Impostazioni personali** ed eseguire l'accesso. Per altre informazioni, vedere [Impostazioni personali per Integrazione di Power BI &#40;portale Web&#41;](my-settings-for-power-bi-integration-web-portal.md).

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. Passare alla cartella [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] che contiene il report e quindi visualizzare il report.  
  
3. Durante la visualizzazione del report, fare clic sul pulsante **Aggiungi a Power BI** nella barra degli strumenti.  Se non è già stato eseguito l'accesso, verrà richiesto di farlo.  Se il pulsante di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] non è visibile, il server di report non è stato integrato con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Per altre informazioni, vedere [Integrazione del server di report e di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. Selezionare l'elemento del report che si vuole aggiungere a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. È possibile aggiungere un solo elemento per volta.  Il Visualizzatore report presenta una visualizzazione ombreggiata del report. Gli elementi del report che è possibile aggiungere sono evidenziati, mentre quelli che non è possibile aggiungere sono ombreggiati con un colore scuro.  
  
    **(1)** selezionare il gruppo contenente il dashboard in cui si vuole aggiungere l'elemento, **(2)** selezionare il dashboard a cui si vuole aggiungere l'elemento e **(3)** selezionare la frequenza di aggiornamento del riquadro nel dashboard.   ![nota](/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") L'aggiornamento è gestito dalle sottoscrizioni di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e, dopo l'aggiunta dell'elemento, è possibile modificare la sottoscrizione e configurare un'altra pianificazione dell'aggiornamento.  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. Selezionare **Aggiungi**.  
  
    Nella finestra **Elemento aggiunto correttamente** è possibile selezionare il collegamento **Visualizzalo in Power BI** per passare al dashboard e visualizzare l'elemento appena aggiunto.  
  
6. Fare clic su **Chiudi** per tornare alla visualizzazione normale del report.  
  
##  <a name="in-the-dashboard"></a><a name="bkmk_in_the_dashboard"></a> Nel dashboard

Dopo l'aggiunta dell'elemento del report nel dashboard, l'aspetto del riquadro è simile a quello di altri riquadri del dashboard e non è presente alcuna indicazione visibile riguardo la sua provenienza da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. L'elenco seguente riepiloga in che modo le proprietà del riquadro vengono popolate dall'elemento del report.  
  
Nel dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] l'elemento del report aggiunto si comporta come gli altri riquadri:

**(1)** È possibile aggiungere il riquadro ad altri dashboard.

**(2)** In **Dettagli riquadro** si noterà che il titolo del report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene usato come titolo predefinito del riquadro.

**(3)** Il sottotitolo del riquadro è basato sulla data e sull'ora di aggiunta del riquadro o dell'ultimo aggiornamento dei dati da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La pianificazione dell'aggiornamento è gestita dalla sottoscrizione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] creata automaticamente quando l'elemento del report è stato aggiunto.

**(5)** Se si fa clic sul riquadro stesso, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] usa il **collegamento personalizzato (4)** per passare alla pagina del [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] del server di report registrato. Il link è stato impostato quando l'elemento è stato aggiunto da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Se non si dispone di connettività a Internet per il server di report, verrà visualizzato un errore nel browser.  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="troubleshoot-issues"></a><a name="bkmk-troubleshoot"></a> Risolvere eventuali problemi  
  
-   **Nessun pulsante di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] nella barra degli strumenti del Visualizzatore report:**  questo messaggio indica che il server di report non è stato integrato con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Per altre informazioni, vedere [Integrazione del server di report e di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
- **Impossibile eseguire l'aggiunta**: se si tenta di aggiungere un elemento, viene visualizzato il messaggio di errore seguente: Vedere la sezione [Elementi che è possibile aggiungere](#bkmk_supported_items).  
  
    "Impossibile eseguire l'aggiunta: in questa pagina non sono presenti elementi del report da poter aggiungere a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]".  
  
-   **Gli elementi aggiunti mostrano dati non aggiornati** in un dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , che non è stato aggiornato per un periodo di tempo.  Il token delle credenziali utente è scaduto ed è necessario eseguire nuovamente l'accesso.  La registrazione delle credenziali utente con Azure e [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] è valida per 90 giorni. Nel [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] fare clic su **Impostazioni personali**. Per altre informazioni, vedere [Impostazioni personali per Integrazione di Power BI &#40;portale Web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
-   **Gli elementi aggiunti mostrano dati non aggiornati** in un dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , che non è stato mai aggiornato.  Il problema è che il report non è configurato per usare le credenziali archiviate. Un report deve usare le credenziali archiviate perché l'azione di aggiunta di un elemento del report crea una sottoscrizione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per gestire la pianificazione dell'aggiornamento dei riquadri. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] richiedono credenziali archiviate. Se si esamina la pagina **Sottoscrizioni personali**, viene visualizzato un messaggio di errore simile al seguente:  
  
    "Errore di recapito di Power BI: dashboard: Elementi SSRS, oggetto visivo: Image3, errore: Impossibile completare l'azione corrente. Le credenziali per l'origine dati utente non soddisfano i requisiti per eseguire il report o il set di dati condiviso. Le credenziali per l'origine dati utente non sono archiviate nel database del server di report oppure l'origine dati utente è configurata per non richiedere credenziali, ma l'account di esecuzione automatica non è specificato. (rsInvalidDataSourceCredentialSetting)"
  
-   **Credenziali di Power BI scadute:**  se si tenta di aggiungere un elemento, viene visualizzato il messaggio di errore seguente. In [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]fare clic su **Impostazioni personali** e, nella pagina Impostazioni personali, fare clic su **Accedi**. Per altre informazioni, vedere [Impostazioni personali per Integrazione di Power BI &#40;portale Web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
    "Impossibile eseguire l'aggiunta: Errore server imprevisto: Le credenziali di Power BI mancano, non sono valide o sono scadute".  
  
-   **Impossibile eseguire l'aggiunta**: se si tenta di aggiungere un elemento a un dashboard in uno stato di sola lettura, verrà visualizzato un messaggio di errore simile al seguente:  
  
    "Errore del server: impossibile trovare l'elemento "Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0". (rsItemNotFound)"  

-   **I riquadri nelle app Power BI mostrano dati non aggiornati:** Se si aggiunge un elemento del report di Reporting Services a un dashboard e quindi si distribuisce il dashboard in un'app, l'elemento del report aggiunto in tale dashboard non verrà aggiornato. 

##  <a name="subscription-management"></a><a name="bkmk_subscription_management"></a> Gestione delle sottoscrizioni  
 Oltre ai problemi relativi alle sottoscrizioni descritti nella sezione sulla risoluzione dei problemi, le informazioni seguenti aiuteranno a mantenere le sottoscrizioni relative a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].
  
-   **Nome dell'elemento modificato:** se un elemento del report aggiunto viene rinominato o eliminato, il riquadro di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] non verrà più aggiornato e verrà visualizzato un messaggio di errore simile al seguente.  Se si ripristina il nome originale dell'elemento, la sottoscrizione inizierà a funzionare di nuovo e il riquadro verrà aggiornato nella pianificazione delle sottoscrizioni.  
  
    "Errore di recapito di Power BI: dashboard: Elementi SSRS, oggetto visivo: Image1, errore: Errore: impossibile trovare l'elemento del report "Image1"".  
  
    È inoltre possibile modificare le proprietà della sottoscrizione e cambiare il **nome dell'elemento visivo del report** con il nome dell'elemento del report appropriato. ![modificare l'oggetto visivo usato per l'aggiornamento di Power BI](../reporting-services/media/ssrs-powerbi-subscription-visual.png "modificare l'oggetto visivo usato per l'aggiornamento di Power BI")  
  
-   **Eliminare un riquadro**. Se si elimina un riquadro in [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], la sottoscrizione associata non viene eliminata in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e nella pagina **Sottoscrizioni personali** viene visualizzato un errore simile al seguente. È possibile eliminare la sottoscrizione.  
  
    "Errore di recapito di Power BI: dashboard: Elementi SSRS, oggetto visivo: Image3, errore: Impossibile trovare l'elemento "Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f"".  

## <a name="video"></a>Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>Vedere anche  
 [Integrazione del server di report e di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Impostazioni personali per Integrazione di Power BI &#40;portale Web&#41;](my-settings-for-power-bi-integration-web-portal.md)  
 [Dashboard in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]