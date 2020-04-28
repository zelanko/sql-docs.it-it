---
title: Report di Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f9697d5a53b2aac0d951445206adc4c4f30e5385
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177083"
---
# <a name="reporting-services-reports-ssrs"></a>Report di Reporting Services (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] i report sono definizioni di report basate su XML che includono i dati del report e gli elementi di layout del report. Su un file system client, i file di definizione di report hanno estensione .rdl. Dopo la pubblicazione, il report si converte in un elemento di report archiviato nel server di report o nel sito di SharePoint. I report sono una parte della piattaforma di report basata su server fornita da [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].

 Se non si ha familiarità con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], assicurarsi di consultare le informazioni in [Concetti relativi a Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).

## <a name="benefits-of-reporting-services-reports"></a>Vantaggi dei report di Reporting Services
 È possibile utilizzare la soluzione di report di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] per:

-   Utilizzare un set di origini dati che fornisce una sola versione degli eventi. Basare i report su tali origini dati per offrire una vista unificata dei dati che aiuti a prendere decisioni aziendali.

-   Visualizzare i dati in diverse modalità interconnesse utilizzando le aree dati. Visualizzare i dati organizzati in tabelle, matrici o schede-oblique ed espandere/comprimere gruppi, grafici, misuratori, indicatori o indicatori KPI e mappe, con la possibilità di annidare i grafici nelle tabelle.

-   Visualizzare report per utilizzo personale oppure pubblicarli su un server di report o un sito di SharePoint per condividerli con il team o l'organizzazione.

-   Definire un report una volta e visualizzarlo in diversi modi. È possibile esportare il report in più formati di file oppure inviarlo ai sottoscrittori come posta elettronica o in un file condiviso. È possibile creare vari report collegati in cui si applicano diversi set di parametri alla stessa definizione di report.

-   Utilizzare parti del report, origini dati condivise, query condivise e sottoreport per definire modalità di visualizzazione dei dati utilizzabili più volte.

-   Gestire le origini dati del report separatamente dalla definizione del report. Ad esempio, è possibile convertire un'origine dati di prova in un'origine dati di produzione senza modificare il report.

-   Progettare report in un layout in formato libero Il layout del report non è limitato per settori di informazioni. È possibile organizzare la visualizzazione dei dati sulla pagina in modo da favorire comprensione, analisi e azione.

-   Abilitare azioni di drill-through e di espansione/compressione di elementi Toggle, pulsanti di ordinamento, descrizioni comando e parametri di report per consentire al lettore di report di interagire con il report. Utilizzare parametri di report combinati con espressioni personalizzate per consentire ai lettori di report di controllare il modo in cui i dati vengono filtrati, raggruppati e ordinati.

-   Definire espressioni che offrono la possibilità di personalizzare il modo in cui i dati del report vengono filtrati, raggruppati e ordinati.

 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")

##  <a name="stages-of-report-processing"></a><a name="bkmk_StagesSummary"></a> Fasi dell'elaborazione del report
 Quando si crea un report, si definisce un file di definizione del report (con estensione rdl) in formato XML. Questo file contiene tutte le informazioni necessarie per permettere all'elaboratore di report di combinare i dati e il layout del report. Quando si visualizza un report, il processo percorre le fasi seguenti:

-   **Compilazione.** Si valutano le espressioni nella definizione del report e il formato intermedio compilato viene archiviato internamente sul server di report.

-   **Processo.** Vengono eseguite le query del set di dati e si combina il formato intermedio con dati e layout.

-   **Rendering.** Il report elaborato viene inviato a un'estensione per il rendering per determinare la quantità di informazioni che si adatta a ogni pagina e creare il report impaginato.

-   **Esportazione (opzionale).** Il report viene esportato in un formato di file diverso.

 Per altre informazioni, vedere [Fasi dello sviluppo di report](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports) in [Concetti relativi a Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).

## <a name="create-reports"></a>Creare report
 Per creare un report:

-   **Determinare lo scopo del report.** Identificare lo scopo del report in base al gruppo di destinatari che lo utilizza. Un report ben progettato fornisce ai lettori le informazioni necessarie per analisi e azione. Le decisioni relative alla progettazione effettuate durante questo passaggio influiscono sulla scelta dei parametri, la progettazione del layout e la modalità di visualizzazione del report. Per altre informazioni, vedere [Pianificazione di un report &#40;Generatore report&#41;](../report-design/planning-a-report-report-builder.md) e [Suggerimenti relativi alla progettazione di report &#40;Generatore report e SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.

-   **Scegliere il tipo di query.** Determinare se usare una query del set di dati generalizzata e condivisa o una query del set di dati specifica del proprio set di report. Un set di dati condiviso con una query generalizzata è facile da gestire per l'utilizzo in più report, ma ogni persona che progetta il report deve filtrare i dati per il set specifico di report in base alle necessità. Per altre informazioni, vedere [Dati del report&#40;SSRS&#41;](../report-data/report-data-ssrs.md).

-   **Pianificare viste di dati correlati.** Pianificare la modalità di visualizzazione dei lettori del report. L'uso di report di riepilogo con la possibilità di eseguire il drill-down all'interno dei dati dettagliati rappresenta un approccio utile per la gestione di grandi quantità di dati. Per altre informazioni, vedere [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).

-   **Configurare i permessi.** Pianificare la strategia per concedere il corretto livello di autorizzazioni. Una strategia comune consiste nel creare una struttura di cartelle nel server di report e concedere l'accesso ai report e agli elementi correlati sulla base dei ruoli e la sicurezza della cartella. Per altre informazioni, vedere [Proteggere i report](#bkmk_SecureReportsSummary).

-   **Scegliere un ambiente di creazione.** Il supporto delle funzionalità varia secondo gli strumenti di creazione. Per altre informazioni, vedere [Strumenti di Reporting Services](../tools/reporting-services-tools.md).

-   Per ogni report:

    -   **Identificare le origini dei dati.** Definire le origini dati del report, una per ogni origine di dati. Per altre informazioni, vedere [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).

    -   **Scegliere quali dati utilizzare da ogni origine.** Per ogni origine dati, definire il set di dati del report. In ogni set di dati viene inclusa una query per specificare quali dati utilizzare. Se si dispone di parametri di report, definire un set di dati per popolare l'elenco dei valori disponibile per ogni parametro. Per altre informazioni, vedere [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](../report-data/report-datasets-ssrs.md) e [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).

    -   **Scegliere una visualizzazione dati.** Per ogni set di dati, specificare quale area dati usare per visualizzare i dati. Effettuare la scelta da un elenco di tabelle, grafici, misuratori e mappe. Per altre informazioni, vedere gli argomenti seguenti:

        -   [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)

        -   [Grafici &#40;Generatore report e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)

        -   [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)

        -   [Indicatori &#40;Generatore report e SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)

        -   [Mappe &#40;Generatore report e SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)

        -   [Misuratori &#40;Generatore report e SSRS&#41;](../report-design/gauges-report-builder-and-ssrs.md)

    -   **Personalizzare i dati e il layout.** Progettare il layout del report. Una definizione di un report è formata da un corpo del report, origini dati, set di dati, aree dati, caselle di testo, righe e immagini. I rettangoli vengono utilizzati come contenitori per il layout e come elementi visivi. Personalizzare ogni area dati creando espressioni per il controllo di filtri, gruppi, ordinamento, formato e visualizzazione i dati. Aggiungere i nomi dei report, i percorsi e le altre informazioni di identificazione che semplifichino la gestione di decine o centinaia di report. Aggiungere elementi e contenitori visivi per organizzare gli elementi di layout sulla pagina. Per altre informazioni, vedere gli argomenti seguenti:

        -   [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)

        -   [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)

        -   [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)

        -   [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)

        -   [Immagini, caselle di testo, rettangoli e linee &#40;Generatore report e SSRS&#41;](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)

        -   [Layout e rendering della pagina &#40;Generatore report e SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)

    -   **Configurare le funzionalità relative all'interattività.** Aggiungere funzionalità interattive utilizzabili dai lettori del report. Ad esempio, aggiungere pulsanti di ordinamento o elementi Toggle per la visualizzazione delle query. Per altre informazioni, vedere [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).

    -   **Rivedere ed eseguire l'iterazione sulla progettazione.** Visualizzare l'anteprima del report. Pubblicare una versione preliminare per ottenere un feedback dai lettori del report. Eseguire l'iterazione sulla progettazione.

-   **Rivedere la soluzione di report.** Verificare che il set di report interagisca correttamente.

-   **Considerare quali componenti possono essere utilizzati nuovamente.**  Determinare se un'origine dati o una query del set di dati può essere condivisa e utilizzata nuovamente. In questo caso, creare origini dati e set di dati condivisi nel server di report o nel sito di SharePoint. Determinare se le aree dati sono adatte per essere utilizzate nuovamente come parti del report. Per altre informazioni, vedere [Parti del report in Progettazione report &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).

## <a name="preview-reports"></a>Anteprima dei report
 Ogni strumento per la creazione di report supporta la visualizzazione in anteprima dei report. Per altre informazioni, vedere [Anteprima](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview), [Generatore Report &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) e [Anteprima di report in Generatore Report](../report-builder/previewing-reports-in-report-builder.md) nella [documentazione di Generatore Report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.

## <a name="save-or-publish-reports"></a>Salvare o pubblicare report
 Ogni strumento di creazione supporta il salvataggio locale o la pubblicazione dei report in un server di report o un sito di SharePoint. Per altre informazioni, vedere [Salvare e distribuire](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy), [Generatore Report &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) e [Salvataggio di report &#40;Generatore Report&#41;](../report-builder/saving-reports-report-builder.md) nella [documentazione di Generatore Report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.

## <a name="view-reports"></a>Visualizzare i report
 Oltre alla visualizzazione in anteprima di un report salvato in locale o pubblicato in un server di report, è possibile fornire ai lettori del report un'ampia gamma di opzioni di visualizzazione. Per visualizzare un report:

-   **Browser.**  Utilizzare il servizio Web ReportServer o il sito di SharePoint per visualizzare report pubblicati. Su un sito di SharePoint, è possibile anche configurare un Web part per la visualizzazione dei report pubblicati. Per altre informazioni, vedere [Pianificazione per il supporto browser per Reporting Services e Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md), [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md) e [Accesso con URL &#41;SSRS&#40;](../url-access-ssrs.md).

-   **Consegna.**  Configurare una sottoscrizione per recapitare i report ai lettori tramite posta elettronica o in una cartella di file condivisa.  Per altre informazioni, vedere [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).

-   **Esportazione.**  Dalla barra degli strumenti del visualizzatore di report, un lettore di report può esportare un report in un formato di file diverso. I formati del file di esportazione possono essere configurati dall'amministratore del server di report. Per altre informazioni, vedere [Esportazione di report &#40;Generatore report e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)

-   **Stampa.**  Un lettore di report può stampare un report o alcune delle relative pagine, a seconda della modalità di visualizzazione. Per altre informazioni, vedere [Stampa di report &#40;Generatore report e SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md).

-   **Applicazione Web o Windows Form.**  Utilizzare Visual Studio per sviluppare un'applicazione AJAX ASP.NET o un applicazione di Windows Form che ospiti il controllo del Visualizzatore report. Il controllo può puntare ai report pubblicati su un server di report. Per altre informazioni, vedere [Rapporti Microsoft](https://go.microsoft.com/fwlink/?LinkID=205399).

## <a name="manage-reports"></a>Gestire i report
 Per gestire un report pubblicato:

-   **Origini dati.** Le origini dati condivise e quelle incorporate vengono gestite in modo indipendente dalla definizione del report.

-   **Set.**  I set di dati condivisi vengono gestiti in modo indipendente dalla definizione del report.

-   **Parametri.**  I parametri vengono gestiti in modo indipendente dalla definizione del report. Dopo che i parametri vengono modificati sul server di report, i client della creazione report non possono sovrascrivere le modifiche apportate nel server.

-   **Risorse.**  Immagini e dati spaziali nei file di forma ESRI sono risorse che possono essere pubblicate e gestite in modo indipendente dalla definizione del report.

-   **Report memorizzati nella cache.**  La pianificazione dell'esecuzione di report di grandi dimensioni negli orari di minore attività consente di ridurre l'impatto dell'elaborazione sul server di report durante l'orario di lavoro principale.

-   **Istantanee.**  Utilizzare snapshot del report quando si desidera offrire risultati coerenti per più utenti che devono utilizzare gli stessi set di dati. Con dati volatili, un report su richiesta può generare risultati diversi anche a differenza di pochi minuti. Uno snapshot del report, invece, consente di eseguire confronti validi con altri report o strumenti analitici contenenti dati riferiti allo stesso momento nel tempo.

-   **Cronologia del report.** Tramite la creazione di una serie di snapshot del report, è possibile compilare una cronologia che mostri le modifiche dei dati del report nel tempo.

 Per altre informazioni sulle prestazioni, vedere [Prestazioni, snapshot, memorizzazione nella cache &#40;Reporting Services&#41;](../report-server/performance-snapshots-caching-reporting-services.md).

##  <a name="secure-reports"></a><a name="bkmk_SecureReportsSummary"></a> Proteggere i report
 Per proteggere un report:

-   Dall'amministratore del server di report, identificare l'autorizzazione e il sistema di autenticazione utilizzati per l'installazione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Per impostazione predefinita, in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] si usano autenticazione di Windows, sicurezza integrata e assegnazione di ruolo per consentire di controllare l'accesso ai report pubblicati. Per altre informazioni, vedere [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md) e [Sicurezza e protezione di Reporting Services](../security/reporting-services-security-and-protection.md).

## <a name="create-notifications-based-on-report-data"></a>Creare notifiche basate su dati dei report
 È possibile creare avvisi relativi ai dati dei report pubblicati in un sito di SharePoint. Gli avvisi relativi ai dati sono basati su feed di dati dalle aree dati nel report. Per impostazione predefinita, le aree dati vengono denominate automaticamente. Gli autori del report possono agevolare la creazione di avvisi relativi ai dati nei loro report denominando le aree dati in base agli scopi aziendali. Quando si crea un avviso relativo ai dati, si riceve una notifica mediante posta elettronica nel momento in cui i dati soddisfano le condizioni specificate. Per altre informazioni, vedere [Generazione di feed di dati dai report &#40;Generatore report e SSRS&#41;](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md), [Creare un avviso dati nella finestra di progettazione Avviso dati](../create-a-data-alert-in-data-alert-designer.md) e [Avvisi dati di Reporting Services](../reporting-services-data-alerts.md).

## <a name="upgrade-reports"></a>Upgrade Reports
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] supporta varie versioni di definizioni dei report, server di report e siti di SharePoint. Per aggiornare un report:

-   Aggiornare un'installazione del server di report I report compilati archiviati nel server di report vengono aggiornati automaticamente al primo utilizzo. La definizione del report (.rdl) non viene modificata. Per altre informazioni, vedere [Upgrade and migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md).

-   Aprire un report in un ambiente di creazione di report. La definizione del report viene aggiornata nella maggior parte delle circostanze. Per altre informazioni, vedere [Aggiornare i report](../install-windows/upgrade-reports.md) e [Distribuzione e supporto della versione di SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).

## <a name="troubleshoot-reports"></a>Risolvere problemi relativi ai report
 Per risolvere problemi relativi a un report:

-   **Determinare dove si sta verificando il problema.** Rivedere le informazioni fornite in [Fasi di un report](#bkmk_StagesSummary).

-   **Determinare dove è possibile trovare ulteriori informazioni.** Ad esempio, nel caso di strutture di report che includono espressioni, lo strumento Progettazione report fornisce maggiori informazioni sui problemi di valutazione delle espressioni rispetto allo strumento Generatore report. Per gli errori dell'elaborazione di report, i file di log contengono informazioni dettagliate.

## <a name="tasks"></a>Attività
 Per collegamenti agli argomenti dettagliati, vedere la sezione Attività negli articoli delle funzionalità menzionati nelle sezioni precedenti di questo argomento.

## <a name="see-also"></a>Vedere anche
 Estensioni [degli strumenti di Reporting Services](../tools/reporting-services-tools.md) [&#40;SSRS&#41;](../extensions-ssrs.md) [Reporting Services server di report](../reporting-services-report-server.md)


