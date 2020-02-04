---
title: Funzionalità interattiva per estensioni diverse per il rendering di report | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1038958e969a04531cf790a9254816b24d3b5646
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580710"
---
# <a name="interactive-functionality---different-report-rendering-extensions"></a>Funzionalità interattiva per estensioni diverse per il rendering di report
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce funzionalità per l'interazione con un report impaginato in fase di esecuzione. Solo alcuni formati di rendering dei report supportano l'intera gamma di caratteristiche interattive. Usare la tabella seguente per comprendere la modalità di utilizzo delle diverse caratteristiche interattive in formati specifici.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="interactive-features-in-different-output-formats"></a>Caratteristiche interattive nei diversi formati di output  
 I report impaginati di cui viene eseguito il rendering nei formati XML, CSV o Immagine non supportano caratteristiche interattive.  
  
 Viene invece eseguito il rendering in HTML dei report visualizzati nel portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , web part di SharePoint o in un browser. HTML e Windows Form sono gli unici formati di output dei report a supportare l'intera gamma di caratteristiche interattive. I formati HTML alternativi, come MHTML, supportano molte caratteristiche interattive. Le eccezioni per MHTML sono riportate nella tabella seguente.  
  
### <a name="document-maps"></a>Mappe documento  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|La mappa documento interattiva è un riquadro di navigazione contenente collegamenti gerarchici utilizzabili per spostarsi tra le diverse sezioni di un report.|  
|PDF|Con l'estensione per il rendering PDF, una mappa documento viene visualizzata come riquadro Segnalibri. Tutti gli elementi nella mappa documento vengono elencati uno dopo l'altro nel riquadro. Include una gerarchia di collegamenti. Se si specifica un intervallo di pagine, la gerarchia comprenderà solo i segnalibri di cui è stato eseguito il rendering.|  
|Excel|In Excel il rendering di una mappa documento viene eseguito come primo foglio della cartella di lavoro. Include una gerarchia di collegamenti. Quando si fa clic sul collegamento nella mappa documento, viene aperta la cella di destinazione appropriata nel rispettivo foglio di lavoro.|  
|Word|In Word il rendering della mappa documento viene eseguito come etichette di sommario.|  
|Altro (ad esempio, TIFF, XML e CSV)|Non disponibili in MHTML, XML, CSV o Immagine.|  
  
### <a name="drillthrough-links-to-other-reports"></a>Collegamenti drill-through ad altri report  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Gli utenti fanno clic sui valori dei dati nel report per visualizzare i dati correlati in un altro report.|  
|PDF|I collegamenti drill-through non sono disponibili nel formato PDF. Utilizzare collegamenti ipertestuali per i report in formato PDF con collegamenti ad altre pagine.|  
|Excel|Il rendering dei collegamenti drill-through viene eseguito in Excel.<br /><br /> Il collegamento diventa un collegamento ipertestuale che punta al report cui fa riferimento il collegamento drill-through. Se si fa clic sul collegamento, viene visualizzato un report in una finestra del browser.|  
|Word|I collegamenti drill-through vengono visualizzati in Word.<br /><br /> Il collegamento diventa un collegamento ipertestuale che punta al report cui fa riferimento il collegamento drill-through. Se si fa clic sul collegamento, viene visualizzato un report in una finestra del browser.|  
|Altri|Non disponibili in XML, CSV o Immagine.|  
  
### <a name="toggle-items-within-a-report"></a>Attivazione/disattivazione di elementi all'interno di un report  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Gli utenti fanno clic sulle icone di espansione o compressione per visualizzare le sezioni di un report.|  
|PDF|Il server di report esporta lo stato di visualizzazione corrente del report in formato PDF. L'attivazione o la disattivazione interattiva non è supportata.|  
|Excel|Il rendering di elementi e collegamenti drill-down che è possibile attivare/disattivare viene eseguito come strutture comprimibili in Excel. In Excel è possibile espandere e comprimere le sezioni del report. Per altre informazioni sulle limitazioni imposte da Excel, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).|  
|Word|Il server di report esporta lo stato di visualizzazione corrente del report in formato PDF. L'attivazione o la disattivazione interattiva non è supportata.|  
|Altri|Non disponibili in MHTML, XML o CSV. In caso di esportazione in un formato immagine, il server di report esporta lo stato di visualizzazione corrente del report in formato PDF. L'attivazione o la disattivazione interattiva non è supportata.|  
  
### <a name="interactive-sorting"></a>Ordinamento interattivo  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Nei report tabella gli utenti fanno clic sulle frecce di ordinamento presenti sulle colonne per modificare il criterio di ordinamento dei dati.|  
|PDF|Non disponibile in PDF.|  
|Excel|Non disponibile in Excel.|  
|Word|Non disponibile in Word.|  
|Altri|Non disponibili in MHTML, XML, CSV o Immagine.|  
  
### <a name="hyperlinks-to-external-web-content-or-images"></a>Collegamenti ipertestuali a immagini o contenuto Web esterni  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Gli utenti fanno clic sui collegamenti per aprire pagine Web esterne in una nuova finestra del browser.|  
|PDF|L'estensione per il rendering PDF esegue il rendering dei collegamenti ipertestuali. Quando un utente fa clic su un collegamento ipertestuale, le pagine collegate vengono aperte nel browser.|  
|Excel|I collegamenti ipertestuali vengono visualizzati in Excel.|  
|Word|I collegamenti ipertestuali vengono visualizzati in Word.|  
|Altri|I collegamenti ipertestuali non sono disponibili in MHTML, XML, CSV o Immagine.<br /><br /> In MHTML e Immagine le immagini esterne vengono visualizzate come immagini statiche.|  
  
### <a name="bookmark-or-anchor"></a>Segnalibro o ancoraggio  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Gli utenti fanno clic sui collegamenti per passare a un'altra sezione dello stesso report.|  
|PDF|Non disponibile in PDF.|  
|Excel|I segnalibri vengono visualizzati in Excel.<br /><br /> Il segnalibro diventa un collegamento ipertestuale che punta al nome dell'elemento del report.|  
|Word|Il rendering dei segnalibri viene eseguito in Word.<br /><br /> Il segnalibro diventa un collegamento ipertestuale che punta all'elemento del report con il segnalibro. Quando si esporta il report vengono convertiti solo 40 caratteri del nome di un segnalibro o di un ancoraggio, pertanto è possibile che vengano creati nomi di segnalibro o ancoraggio duplicati. Gli spazi vengono convertiti in caratteri di sottolineatura (_).|  
|Altri|Non disponibili in XML, CSV o Immagine.|  
  
### <a name="prompted-parameters-obtained-at-run-time"></a>Parametri richiesti ottenuti in fase di esecuzione  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|Viene visualizzata un'area di input dei parametri nella parte superiore del report. Quest'area fa parte del Visualizzatore HTML utilizzato per visualizzare i report in un browser.|  
|PDF|Il server di report esporta il report in PDF utilizzando i valori dei parametri attualmente in uso per il report.|  
|Excel|Il server di report esporta il report in Excel utilizzando i valori dei parametri attualmente in uso per il report.|  
|Word|Il server di report esporta il report in Word utilizzando i valori dei parametri attualmente in uso per il report.|  
|Altri|Il server di report esporta il report in altri formati utilizzando i valori dei parametri attualmente in uso per il report.|  
  
### <a name="filters-applied-at-run-time"></a>Filtri applicati in fase di esecuzione  
  
|Opzione di esportazione|Informazioni relative al supporto|  
|-------------------|-------------------------|  
|Anteprima/Visualizzatore report, HTML|I dati filtrati vengono visualizzati all'utente in fase di esecuzione.|  
|PDF|Il server di report esporta il report in PDF utilizzando i dati filtrati nel report corrente.|  
|Excel|Il server di report esporta il report in Excel utilizzando i dati filtrati nel report corrente.|  
|Word|Il server di report esporta il report in Word utilizzando i dati filtrati nel report corrente.|  
|Altri|Il server di report esporta il report in altri formati utilizzando i dati filtrati nel report corrente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
    
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
