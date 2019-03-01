---
title: Che cos'è SQL Server Reporting Services (SSRS) | Microsoft Docs
description: Informazioni sugli strumenti e i servizi per i report di Reporting Services impaginati e per dispositivi mobili in locale.
ms.date: 05/25/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 08a71374d72a70e9bba6863eb9f6b5ac548d28f7
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297399"
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>Che cos'è SQL Server Reporting Services (SSRS)?

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

Per informazioni sul server di report di Power BI, vedere [Che cos'è Server di report di Power BI?](https://docs.microsoft.com/power-bi/report-server/get-started)

Creare, distribuire e gestire report impaginati e per dispositivi mobili di Reporting Services in locale, con la gamma di strumenti e servizi pronti all'uso offerti da SQL Server Reporting Services (SSRS).

![SQL Server Reporting Services su tutti i dispositivi](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services su tutti i dispositivi")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>Creare, distribuire e gestire report impaginati e per dispositivi mobili

SQL Server Reporting Services è una soluzione che i clienti distribuiscono nella propria sede per la creazione, la pubblicazione e la gestione di report, in modo da inviarli agli utenti giusti in diversi modi, tramite visualizzazione su Web browser, su un dispositivo mobile o come messaggio di posta elettronica nella casella di posta in arrivo.

SQL Server Reporting Services offre una famiglia di prodotti aggiornata:

* **Report impaginati "tradizionali"** aggiornati, in modo da poter creare report dall'aspetto moderno, con strumenti aggiornati e nuove funzionalità per crearli.
* **Nuovi report per dispositivi mobili** con un layout reattivo, in grado di adattarsi a diversi dispositivi e a diverse modalità di orientamento.
* **Un portale Web moderno** visualizzabile in qualsiasi browser moderno. Nel nuovo portale è possibile organizzare e visualizzare report impaginati e per dispositivi mobili e indicatori KPI di Reporting Services. È anche possibile archiviare cartelle di lavoro di Excel nel portale.

Nelle sezioni che seguono sono disponibili informazioni più dettagliate.

### <a name="whats-new-in-reporting-services"></a>Novità di Reporting Services

Queste fonti consentono di rimanere aggiornati sulle nuove funzionalità di SQL Server Reporting Services.

* [Novità di Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [Blog del team di SQL Server Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* Il [video di Guy in a Cube sul canale YouTube](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>Report impaginati

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services è associato ai report in formato impaginato "tradizionale", in cui le righe delle tabelle e le pagine del report aumentano proporzionalmente alla quantità di dati. Questo tipo di impaginazione è molto utile per la generazione di documenti con layout fisso ad alta definizione ottimizzati per la stampa, ad esempio file PDF e file di Word.

Questo carico di lavoro BI di base esiste tuttora e pertanto è stato modernizzato. Ora è possibile creare report dall'aspetto moderno con nuove funzionalità usando [Generatore report](../reporting-services/report-builder/report-builder-in-sql-server-2016.md) o Progettazione report in [SQL Server Data Tools (SSDT)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).

* Tutti gli stili e le tavolozze dei colori predefiniti sono stati aggiornati in modo da poter creare report con un nuovo stile moderno minimalista.
* Il riquadro dei parametri è stato aggiornato ed è ora possibile disporre i parametri nell'ordine desiderato.
* I report possono essere esportati in nuovi formati, ad esempio PowerPoint. Le visualizzazioni di Reporting Services in PowerPoint sono attive e modificabili, non sono semplici screenshot.
* È possibile creare un'esperienza ibrida di Power BI/Reporting Services.  Anziché ricreare i report di Reporting Services locali in Power BI, è possibile aggiungere elementi visivi dai report ai dashboard di Power BI. in modo da monitorare tutto da un'unica posizione nel proprio dashboard di Power BI.

## <a name="mobile-reports"></a>Report per dispositivi mobili

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

Con il mobile computing, i dispositivi necessari per lavorare sono cambiati e pertanto le persone hanno esigenze diverse per quanto riguarda la generazione di report. I report con layout fisso non sono adatti per tablet e smartphone. Un elemento progettato per uno schermo ampio di PC non viene visualizzato in modo ottimale sul display di uno smartphone che, oltre ad avere dimensioni più piccole, consente l'orientamento orizzontale o verticale.

Con questi formati di schermo notevolmente diversi, non è necessario un layout fisso, ma un layout reattivo, in grado di adattarsi a diversi dispositivi e a diverse modalità di orientamento. È stato quindi aggiunto un nuovo tipo di report, per dispositivi mobili, che è basato sulla tecnologia Datazen, acquisita da Microsoft circa un anno fa e integrata nel prodotto. È possibile eseguire la migrazione dei report Datazen esistenti in Reporting Services con [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128). 

I report per dispositivi mobili vengono creati con la nuova app [Mobile Report Publisher](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) . Di conseguenza, usando le [app Power BI per dispositivi mobili](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) native per Windows 10, iOS, Android e HTML5, è possibile accedere ai dati presenti nel cloud di Power BI e ai dati locali di SQL Server Reporting Services. Mentre si creano le visualizzazioni, Mobile Report Publisher genera automaticamente dati di esempio per ciascuna, permettendo così di visualizzare in anteprima l'aspetto dei dati e di scegliere il tipo di dati adatto a ogni visualizzazione.

## <a name="web-portal"></a>Portale Web

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

Per gli utenti finali di Reporting Services in modalità nativa, la porta d'ingresso è un portale Web moderno che è possibile visualizzare in qualsiasi browser moderno. È possibile accedere a tutti i report impaginati e per dispositivi mobili e gli indicatori KPI di Reporting Services.

Nel portale Web è possibile applicare una grafica personalizzata e anche creare indicatori KPI, in modo da visualizzare le principali metriche aziendali immediatamente nel browser, senza dover aprire un report. 

Il nuovo portale Web è una riscrittura completa di Report Manager. È ora diventato un'app HTML5 a pagina singola, basata su standard, per cui sono ottimizzati i browser moderni: Edge, Internet Explorer 10 e 11, Chrome, Firefox, Safari e tutti i browser più diffusi.

Il contenuto del portale Web è organizzato in base al tipo: report impaginati e per dispositivi mobili e indicatori di prestazioni chiave di Reporting Services, cartelle di lavoro di Excel, set di dati condivisi e origini dati condivise da usare come blocchi predefiniti per i report. È possibile archiviare e gestire questi elementi in modo sicuro nel portale con la gerarchia di cartelle classica. È possibile contrassegnare i preferiti e gestire il contenuto, se si dispone del ruolo appropriato.

Nel nuovo portale Web è ancora possibile pianificare l'elaborazione dei report, accedere ai report su richiesta e sottoscrivere report pubblicati.

Altre informazioni sul [portale Web (modalità nativa SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>Reporting Services in modalità integrata SharePoint

I report vengono pubblicati in Reporting Services in modalità integrata SharePoint. È possibile pianificare l'elaborazione dei report, accedere ai report su richiesta, sottoscrivere report pubblicati ed esportare report in altre applicazioni, ad esempio Microsoft Excel. È possibile creare avvisi dati nei report pubblicati in un sito di SharePoint e ricevere messaggi di posta elettronica quando i dati del report cambiano.  

Per altre informazioni, vedere [Server di report di Reporting Services in modalità SharePoint integrata](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md).

## <a name="includessrsnoversionincludesssrsnoversion-mdmd-programming-features"></a>Funzionalità di programmazione di[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 

È possibile sfruttare le funzionalità di programmazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per poter estendere e personalizzare la funzionalità di reporting con API per integrare o estendere l'elaborazione di dati e report in applicazioni personalizzate.

Per altre informazioni, vedere [Guida per gli sviluppatori (Reporting Services)](../reporting-services/reporting-services-developer-documentation.md). 

## <a name="next-steps"></a>Passaggi successivi

* [Installare Reporting Services](../reporting-services/install-windows/install-reporting-services.md)  
* [Installare Generatore report](../reporting-services/install-windows/install-report-builder.md)   
* [Scaricare SQL Server Data Tools (SSDT)](https://go.microsoft.com/fwlink/?LinkID=616714)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
