---
title: Portale Web (modalità nativa SSRS) | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c5f8405a36595b7a5ddaade9aa00952642625c65
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711222"
---
# <a name="web-portal-ssrs-native-mode"></a>Portale Web (modalità nativa SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Il portale Web di Reporting Services è un'esperienza basata su Web che consente di visualizzare report, inclusi quelli per dispositivi mobili, e indicatori KPI e di spostarsi tra gli elementi presenti nell'istanza del server di report. Il portale Web consente anche di amministrare una singola istanza del server di report.

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>Informazioni sul portale Web

È possibile usare il portale Web per eseguire le attività seguenti:

- Visualizzare, cercare, stampare e sottoscrivere report.

- Creare, proteggere e gestire la gerarchia di cartelle per organizzare gli elementi presenti nel server.

- Configurare la sicurezza basata sui ruoli dalla quale dipende l'accesso a elementi e operazioni.

- Configurare le proprietà di esecuzione, la cronologia e i parametri dei report.

- Creare pianificazioni condivise e origini dei dati condivise per migliorare la gestione delle pianificazioni e delle connessioni alle origini dei dati.

- Creare sottoscrizioni guidate dai dati che consentono di distribuire i report a un elenco di destinatari di grandi dimensioni.

- Creare report collegati per riutilizzare e ridefinire gli scopi di un report esistente in modi diversi.

- Scaricare strumenti comuni come Generatore report e Mobile Report Publisher.

- [Creare indicatori KPI](../reporting-services/working-with-kpis-in-reporting-services.md).

- Inviare commenti e suggerimenti o richieste di funzionalità.

È possibile usare portale Web per esplorare le cartelle del server di report o cercare report specifici. È possibile visualizzare un report, le sue proprietà generali e vecchie copie del report acquisite nella cronologia del report. A seconda delle autorizzazioni di cui si dispone, potrebbe inoltre essere possibile sottoscrivere report per il recapito in una casella di posta elettronica o in una cartella condivisa nel file system.

> [!NOTE]
> Per informazioni sulle versioni e i browser supportati, vedere [Pianificazione per il supporto browser di Reporting Services](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

Il portale Web viene usato solo per un server di report in esecuzione in modalità nativa. Non è supportato per un server di report configurato per la modalità integrata SharePoint.

Alcune funzionalità del portale Web sono disponibili solo in determinate edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Funzionalità di Reporting Services supportate dalle edizioni di SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

In una nuova installazione solo gli amministratori locali dispongono di autorizzazioni sufficienti per utilizzare il contenuto e le impostazioni. Per concedere le autorizzazioni agli altri utenti, un amministratore locale deve creare le assegnazioni di ruolo appropriate per gestire l'accesso al server di report. Le pagine dell'applicazione e le operazioni che saranno in seguito disponibili per un utente dipendono dalle assegnazioni di ruolo di tale utente. Per altre informazioni, vedere [Concedere l'accesso utente a un server di report](security/grant-user-access-to-a-report-server-report-manager.md)

> [!NOTE]
> Se si sta esplorando il portale Web nel computer locale su cui è in esecuzione il server, è possibile visualizzare un messaggio che indica che non è consentito visualizzare questa cartella. Ciò è dovuto a Controllo dell'account utente e al fatto che non si esegue il browser come amministratore. Non è possibile eseguire Edge come amministratore. È necessario usare Internet Explorer. È possibile esplorare il server in modalità remota oppure avviare Internet Explorer come amministratore e usarlo per esplorare il portale Web. Per usare il portale Web in modalità remota, sarà necessario concedere all'account i diritti di gestione contenuto per la cartella.  

## <a name="start-and-use-the-web-portal"></a>Avviare e usare il portale Web

Il portale Web è un'applicazione Web che si apre digitando l'URL del [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] nella barra degli indirizzi della finestra del browser. Quando si avvia il [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], le pagine, le opzioni e i collegamenti visualizzati variano in base alle autorizzazioni disponibili per il server di report. Per eseguire un'attività, è necessario essere assegnato a un ruolo che include l'attività.  Gli utenti assegnati a un ruolo con autorizzazioni complete hanno accesso a tutti i menu e le pagine disponibili per la gestione di un server di report. Un utente assegnato a un ruolo autorizzato a visualizzare ed eseguire i report, invece, potrà visualizzare solo le pagine e i menu correlati a queste attività specifiche. Per ogni utente è possibile impostare assegnazioni di ruolo diverse per server di report diversi o anche per le varie cartelle e i vari report archiviati in un singolo server di report.

Per altre informazioni sui ruoli, vedere [Concessione di autorizzazioni in un server di report in modalità nativa](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).

### <a name="start-the-web-portal"></a>Avviare il portale Web

Per avviare il portale Web da un browser, eseguire le operazioni seguenti:

1. Aprire il Web browser. Per un elenco dei Web browser supportati, vedere [Pianificazione per il supporto browser di Reporting Services](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

2. Nella barra degli indirizzi del Web browser digitare l'URL del portale Web.

    L'URL predefinito è *https://[NomeComputer]/reports*.

    Il server di report potrebbe essere configurato per l'utilizzo di una porta specifica. Ad esempio, *https://[NomeComputer]:80/reports* o *https://[NomeComputer]:8080/reports*.

## <a name="grouping-by-categories"></a>Raggruppamento per categorie

Il portale Web raggruppa gli elementi in diverse categorie. Le categorie disponibili sono le seguenti.

- KPI
- Report per dispositivi mobili
- Report impaginati
- Report di Power BI Desktop
- Cartelle di lavoro di Excel
- Set di dati
- Origini dati
- Risorse

È possibile controllare gli elementi visualizzati selezionando **Visualizza** in alto a destra. Se si seleziona Mostra nascosti, questi elementi verranno visualizzati in un colore più chiaro.

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Report di Power BI Desktop e cartelle di lavoro di Excel

È possibile caricare, organizzare e gestire le autorizzazioni per i report di Power BI Desktop e le cartelle di lavoro di Excel. Verranno raggruppati all'interno del portale Web.

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

I file vengono archiviati in Reporting Services, in modo analogo ad altri file di risorse. È possibile selezionare uno di questi elementi per scaricarlo in locale nel desktop. Le modifiche apportate possono essere salvate caricandole di nuovo nel server di report.

## <a name="search-for-items"></a>Cercare elementi

È possibile immettere un termine di ricerca per visualizzare tutto gli elementi accessibili. I risultati sono suddivise in categorie, ovvero indicatori KPI, report, set di dati e altri elementi. È quindi possibile interagire con i risultati e aggiungerli ai preferiti.

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>Attività del portale Web

[Personalizzazione del portale Web](../reporting-services/branding-the-web-portal.md)

[Utilizzo degli indicatori KPI](../reporting-services/working-with-kpis-in-reporting-services.md)

[Utilizzo dei set di dati condivisi](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>Vedere anche

[Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[Configurare un URL (Gestione configurazione SSRS)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Strumenti di Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
[Pianificazione per il supporto browser di Reporting Services](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Funzionalità di Reporting Services supportate dalle edizioni di SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
