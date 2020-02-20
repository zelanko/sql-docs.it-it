---
title: Generatore report in SQL Server | Microsoft Docs
ms.date: 05/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c10e37d7c1231a3ed4db2d7412ea223cccc6922d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67688519"
---
# <a name="report-builder-in-sql-server"></a>Generatore report in SQL Server

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] è uno strumento per la creazione di report impaginati, per gli utenti aziendali che preferiscono lavorare in un ambiente autonomo invece di usare Progettazione report in Visual Studio/SSDT.  Quando si progetta un report impaginato, si crea una definizione del report che specifica quali dati recuperare, dove recuperarli e come visualizzarli. Quando si esegue il report, l'elaboratore di report usa la definizione del report specificata, recupera i dati e li combina con il layout per generare il report. È possibile visualizzare il report in anteprima in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Pubblicare quindi il report in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa o in modalità integrata SharePoint (2016 e versioni precedenti). 

È anche possibile pubblicare un report impaginato nel servizio Power BI. Sono disponibili altre informazioni sui [report impaginati in Power BI Premium](https://docs.microsoft.com/power-bi/paginated-reports-report-builder-power-bi) (anteprima).
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 Questo report impaginato include una matrice con gruppi di righe e colonne, grafici sparkline, indicatori e un grafico a torta riepilogativo nella cella d'angolo, accompagnata da una mappa con due set di dati geografici rappresentati dal colore e dalle dimensioni del cerchio.  
  
##  <a name="JumpStartReptCreation"></a> Avvio della creazione del report  
  
-   **Iniziare con un set di dati condiviso**. I set di dati condivisi sono query basate su un'origine dati condivisa che vengono salvate in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa o in modalità integrata SharePoint.  
  
-   **Avviare la procedura guidata di tabella, matrice o grafico**. Scegliere una connessione all'origine dati, trascinare campi per creare una query del set dei dati, selezionare un layout e uno stile e personalizzare il report.  
  
-   **Avviare la creazione guidata della mappa** per creare report di visualizzazione dei dati aggregati su uno sfondo geografico o geometrico. I dati di una mappa possono essere dati spaziali di una query [!INCLUDE[tsql](../../includes/tsql-md.md)] o di un file di forma ESRI (Environmental Systems Research Institute, Inc.). È inoltre possibile aggiungere un sfondo a tessera mappa di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing.  
  
-   **Iniziare il report con le parti del report**. Le parti di report sono elementi di report che sono stati pubblicati separatamente in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa o in modalità integrata SharePoint e possono essere riusati in altri report. È possibile pubblicare elementi di report quali tabelle, matrici, grafici e immagini come parti di report.  
  
##  <a name="DesignRept"></a> Progettazione del report  
  
-   **Creare report impaginati con tabelle, matrici, grafici e layout in formato libero.** Creare report tabella per dati distribuiti in colonne, report matrice (ad esempio report a campi incrociati o di tabelle pivot) per dati di riepilogo, report grafici per dati grafici e report in formato libero per qualsiasi altra esigenza. Nei report è possibile incorporare altri report e grafici, nonché elenchi, grafica e controlli per le applicazioni Web dinamiche.  
  
-   **Report da diverse origini dati.** È possibile compilare report usando dati da qualsiasi tipo di origine dati per cui sia disponibile un provider di dati gestito da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], un provider OLE DB oppure un'origine dati ODBC. È possibile creare report che utilizzano dati relazionali e multidimensionali da database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion e così via. È inoltre possibile utilizzare un'estensione per l'elaborazione dei dati XML per recuperare dati da qualsiasi origine dei dati XML. Per progettare origini dati personalizzate, è possibile utilizzare funzioni con valori di tabella.  
  
-   **Modificare report esistenti.** Con [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]è possibile personalizzare e aggiornare report creati in Progettazione report di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   **Modificare i dati** filtrandoli, raggruppandoli e ordinandoli o aggiungendo formule o espressioni.  
-   **Aggiungere grafici, misuratori, grafici sparkline e indicatori** per riepilogare i dati in un formato visivo e presentare in modo immediato volumi elevati di informazioni aggregate.  
  
-   **Aggiungere funzionalità interattive** quali mappe documento, pulsanti Mostra/Nascondi e collegamenti drill-through a sottoreport e report drill-through. È possibile utilizzare parametri e filtri per filtrare i dati per le viste personalizzate.  
  
-   **Incorporare o fare riferimento a immagini** e altre risorse, ad esempio contenuto esterno.  
  
##  <a name="ManageRpt"></a> Gestione del report  
  
-   **Salvare la definizione del report** nel computer o nel server di report per poter gestire e condividere il report con altri utenti.  
  
-   **Scegliere un formato di presentazione** all'apertura del report o dopo averlo aperto. È possibile scegliere tra formati per il Web, per la pagina e per applicazioni desktop. I formati disponibili includono HTML, MHTML, PDF, XML, CSV, TIFF, Word ed Excel.  
  
-   **Impostare sottoscrizioni.** Dopo aver pubblicato il report nel server di report o in un server di report in modalità integrata SharePoint, è possibile configurare il report in modo che venga eseguito a un'ora specifica, creare una cronologia del report e impostare sottoscrizioni per il recapito tramite posta elettronica.  
  
-   **Generare feed di dati** dal report tramite l'estensione per il rendering Atom di Reporting Services.  
  
> [!NOTE]  
>  I report pubblicati sono gestiti in un server di report o in server di report in modalità integrata SharePoint da un amministratore del server di report. Gli amministratori del server di report possono definire la sicurezza, impostare le proprietà e pianificare le operazioni, ad esempio la cronologia dei report e il recapito dei report tramite posta elettronica. Possono inoltre creare pianificazioni e origini dei dati condivise per renderle disponibili per l'utilizzo da parte di tutti gli utenti. Gli amministratori gestiscono inoltre tutte le cartelle del server di report. La capacità di eseguire le operazioni di gestione dipende dalle autorizzazioni dell'utente.  
  
## <a name="see-also"></a>Vedere anche  
  [Avviare Generatore report](../../reporting-services/report-builder/start-report-builder.md)  
  
  [Installare Generatore report](../../reporting-services/install-windows/install-report-builder.md)

  [Novità di SQL Server Reporting Services e Generatore report](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  Descrive le nuove funzionalità disponibili in questa versione di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].   
  [Esercitazione: Creazione di un report grafico rapido offline](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Presenta [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e le procedure guidate disponibili per la creazione di report. Viene inoltre fornito un set di dati iniziale da utilizzare per evitare di connettersi a un'origine dati.  
  
 [Pianificazione di un report &#40;Generatore report&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 Vengono fornite informazioni sugli aspetti che è necessario considerare prima di iniziare a compilare il report.  
  
 [Concetti relativi a Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md)  
 Definisce i concetti chiave usati in tutta la documentazione relativa a [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] .  
  
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 Vengono illustrati i diversi riquadri e le diverse aree della visualizzazione di progettazione report.  
  
 [Visualizzazione di progettazione set di dati condivisi &#40;Generatore report&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 Vengono illustrati i diversi riquadri e le diverse aree della visualizzazione di progettazione del set di dati condiviso.  
  
 [Tasti di scelta rapida &#40;Generatore report&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 Descrive le scelte rapida da tastiera disponibili per la navigazione e la progettazione di report in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  

