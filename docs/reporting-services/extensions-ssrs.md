---
title: Estensioni
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: f7a64289bd3f1e1bd8fce71d21e5e1604e5bf4b4
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262892"
---
# <a name="extensions-for-sql-server-reporting-services-ssrs"></a>Estensioni di SQL Server Reporting Services (SSRS)

  Il server di report in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa le estensioni per modulare i tipi di input o output accettati per l'autenticazione, l'elaborazione dati, il rendering e il recapito dei report. Questo semplifica l'utilizzo di nuovi standard di software del settore da parte delle installazioni esistenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , quale un nuovo schema di autenticazione o un tipo di origine dati personalizzato. Il server di report supporta estensioni di autenticazione personalizzate, estensioni per l'elaborazione dati, estensioni dell'elaborazione di report, estensioni per il rendering ed estensioni per il recapito e estensioni disponibili per gli utenti sono configurabili nel file di configurazione RSReportServer.config. Ad esempio, è possibile limitare i formati di esportazione che il visualizzatore di report può usare. Un server di report richiede almeno un'estensione di autenticazione, un'estensione per l'elaborazione dati e un'estensione per il rendering. Le estensioni personalizzate di elaborazione dei report e di recapito sono facoltative. Sono tuttavia necessarie se si desidera supportare la distribuzione dei report o i controlli personalizzati.  
  
 In questo argomento vengono descritte le estensioni immediatamente disponibili in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="security-extensions"></a>Estensioni di sicurezza

 Le estensioni di sicurezza sono utilizzate per autenticare e autorizzare utenti e gruppi presso un server di report. L'estensione predefinita di sicurezza si basa sull'autenticazione di Windows. Nel caso in cui il modello di distribuzione richieda un approccio di autenticazione diverso, ad esempio se è richiesta l'autenticazione basata su form per la distribuzione in Internet o in reti Extranet, è inoltre possibile creare un'estensione personalizzata di sicurezza in sostituzione di quella predefinita. In una singola installazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è possibile usare una sola estensione di sicurezza. È possibile sostituire l'estensione predefinita di sicurezza dell'autenticazione di Windows, ma non è possibile utilizzarla insieme a un'estensione personalizzata di sicurezza.  
  
## <a name="data-processing-extensions"></a>Estensioni per l'elaborazione dati

 Le estensioni per l'elaborazione dati vengono utilizzate per eseguire una query su un'origine dati e restituire un set di righe bidimensionale. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa estensioni diverse per interagire con tipi di origini dati diversi. È possibile usare le estensioni incluse in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]oppure svilupparne di personalizzate. Vengono fornite estensioni per l'elaborazione dati per origini dati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)], Hyperion Essbase, Teradata, OLE DB e ODBC. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] può anche usare qualsiasi provider di dati di [!INCLUDE[vstecado](../includes/vstecado-md.md)] . Le estensioni per l'elaborazione dati gestiscono l'elaborazione delle richieste di query provenienti dal componente Elaborazione report tramite l'esecuzione delle attività seguenti:  
  
- Aprire una connessione a un'origine dati.  
  
- Analisi di una query e restituzione di un elenco di nomi di campo.  
  
- Esecuzione di una query sull'origine dei dati e restituzione di un set di righe.  
  
- Passaggio di parametri a una query, se necessario.  
  
- Esecuzione di un'iterazione del set di righe e recupero dei dati.  
  
Alcune estensioni consentono inoltre di eseguire le attività seguenti:  
  
- Analizzare una query e restituire un elenco di nomi di parametri utilizzati nella query.  
  
- Analisi di una query e restituzione di un elenco dei campi utilizzati per il raggruppamento.  
  
- Analisi di una query e restituzione di un elenco dei campi utilizzati per l'ordinamento.  
  
- Specifica di nome utente e password per la connessione all'origine dei dati.  
  
- Passaggio di parametri con più valori a una query.  
  
- Esecuzione di un'iterazione delle righe e recupero dei metadati ausiliari.  
  
## <a name="rendering-extensions"></a>Estensioni per il rendering

 Le estensioni per il rendering consentono di trasformare i dati e le informazioni sul layout generate dall'elaboratore di report in un formato specifico del dispositivo. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] include sette estensioni per il rendering: HTML, Excel, CSV, XML, Image, PDF e [!INCLUDE[msCoName](../includes/msconame-md.md)] Word.  
  
- **Estensioni per il rendering HTML** Quando si richiede un report da un server di report tramite un Web browser, il server di report usa l'estensione per il rendering HTML per eseguire il rendering del report. L'estensione per il rendering HTML genera tutto il codice HTML con la codifica UTF-8. Per altre informazioni, vedere [Rendering in formato HTML &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md) e [Supporto browser per Reporting Services e Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
- **Estensione per il rendering Excel** L'estensione per il rendering Excel viene usata per il rendering dei report in un formato visualizzabile e modificabile in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 o versioni successive. Questa estensione per il rendering crea file in formato BIFF (Binary Interchange File Format). BIFF è il formato file nativo per i dati Excel. I report di cui è stato eseguito il rendering in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] supportano tutte le caratteristiche disponibili per qualsiasi foglio di calcolo. Per altre informazioni, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
- **Estensione per il rendering CSV** L'estensione per il rendering CSV consente di eseguire il rendering dei report in file di testo normale con valori delimitati da virgole, senza alcuna formattazione. Gli utenti possono quindi aprire i file in questo formato con un'applicazione foglio di calcolo, ad esempio [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]o con qualsiasi altro programma che supporti i file di testo. Per altre informazioni, vedere [Esportazione in un file CSV &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
- **Estensione per il rendering XML** L'estensione per il rendering XML esegue il rendering dei report in file XML che possono essere archiviati o letti da altri programmi. È inoltre possibile utilizzare una trasformazione XSLT per trasformare il report in un altro XML Schema utilizzabile da un'altra applicazione. Per il codice XML generato dall'estensione per il rendering XML viene utilizzata la codifica UTF-8. Per altre informazioni, vedere [Esportazione in XML &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md).  
  
- **Estensioni per il rendering delle immagini** L'estensione per il rendering delle immagini esegue il rendering dei report in bitmap o metafile nei formati BMP, EMF, GIF, JPEG, PNG, TIFF e WMF. Per impostazione predefinita, il rendering delle immagini viene eseguito nel formato TIFF supportato dal visualizzatore di immagini predefinito del sistema operativo, ad esempio Visualizzatore immagini e fax per Windows. È quindi possibile inviare l'immagine a una stampante dal visualizzatore. L'utilizzo di questa estensione per il rendering dei report garantisce che l'aspetto del report sia identico in tutti i client. Quando si visualizza un report in formato HTML, l'aspetto del report può variare a seconda della versione e delle impostazioni del browser dell'utente, nonché dei tipi di carattere disponibili. L'estensione per il rendering delle immagini esegue il rendering del report nel server in modo da visualizzare la stessa immagine a tutti gli utenti. Poiché il rendering del report viene eseguito nel server, è necessario che in tale server siano installati tutti i tipi di carattere utilizzati nel report. Per altre informazioni, vedere [Esportazione in un file di immagine &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md).  
  
- **Estensione per il rendering PDF** L'estensione per il rendering PDF consente di eseguire il rendering dei report in file PDF che possono essere aperti e visualizzati con Adobe Acrobat 6.0 o versioni successive. Per altre informazioni, vedere [Esportazione in un file PDF &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md).  
  
- **Estensione per il rendering Word** L'estensione per il rendering [!INCLUDE[msCoName](../includes/msconame-md.md)] Word esegue il rendering di un report come documento di Word compatibile con [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 o versioni successive. Per altre informazioni, vedere [Esportazione in Microsoft Word &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
## <a name="report-processing-extensions"></a>Estensioni per l'elaborazione del report

 È possibile aggiungere estensioni per l'elaborazione del report per consentire l'elaborazione personalizzata degli elementi del report non inclusi in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Per impostazione predefinita, un server di report è in grado di elaborare tabelle, grafici, matrici, elenchi, caselle di testo, immagini e tutti gli altri elementi del report. Per aggiungere funzionalità speciali a un report che richiedono l'elaborazione personalizzata durante l'esecuzione del report, ad esempio per incorporare una mappa di [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint, è possibile creare un'estensione per l'elaborazione del report.  
  
## <a name="delivery-extensions"></a>Estensioni per il recapito
 L'applicazione di elaborazione in background utilizza estensioni per il recapito per recapitare i report in varie destinazioni. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] include due estensioni, una per il recapito tramite posta elettronica e una per il recapito tramite condivisione file. L'estensione per il recapito tramite posta elettronica consente di inviare un messaggio di posta elettronica tramite SMTP (Simple Mail Transport Protocol) che include il report stesso oppure l'URL per accedere al report. È inoltre possibile inviare brevi messaggi a cercapersone, telefoni o altri dispositivi, senza includere l'URL o il report. L'estensione per il recapito tramite condivisione file consente di salvare i report in una cartella condivisa nella rete. Per il file creato è possibile specificare il percorso, il formato di rendering, il nome file e opzioni di sovrascrittura. È possibile utilizzare il metodo di recapito tramite condivisione file per archiviare i report per i quali è stato eseguito il rendering e nell'ambito della strategia per l'utilizzo di report di dimensioni molto grandi. Le estensioni per il recapito interagiscono con le sottoscrizioni. Al momento della creazione di una sottoscrizione, gli utenti hanno la possibilità di scegliere una delle estensioni per il recapito disponibili per impostare il metodo di recapito del report preferito.