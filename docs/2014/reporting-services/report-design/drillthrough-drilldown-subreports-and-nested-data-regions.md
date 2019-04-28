---
title: Drill-through, drill-down, sottoreport e aree dati nidificate (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4791a157-b028-4698-905d-f1dd0887aa0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 13383c305b9e2e8f1c1ece754c55e5d0f0bd6955
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825028"
---
# <a name="drillthrough-drilldown-subreports-and-nested-data-regions-report-builder-and-ssrs"></a>Drill-through, drill-down, sottoreport e aree dati nidificate (Generatore report e SSRS)
  È possibile organizzare i dati in vari modi per mostrare la relazione da generale a dettagliata.  È possibile inserire tutti i dati nel report, ma impostarli in modo che rimangano nascosti finché un utente non farà clic per rivelare i dettagli. Questa è un'azione di tipo *drill-down* . È possibile visualizzare i dati in un'area dati, ad esempio una tabella o un grafico, *annidata* in un'altra area dati, ad esempio una tabella o una matrice. È possibile visualizzare i dati in un *sottoreport* completamente contenuto in un report principale. In alternativa, è possibile inserire i dati di dettaglio in report *drill-through* , ovvero report separati che vengono visualizzati quando un utente fa clic su un collegamento.  
  
 ![rs_DrillThruDrilldownEtc](../media/rs-drillthrudrilldownetc.gif "rs_DrillThruDrilldownEtc")  
  
 A. Report drill-through  
  
 B. sottoreport  
  
 C. Aree dati nidificate  
  
 D. Azione di drill-down  
  
 Tutti questi elementi presentano similitudini, ma hanno scopi diversi e dispongono di caratteristiche diverse. Due di essi, report drill-through e sottoreport, sono in effetti report separati. La nidificazione è un modo per inserire un'area dati in un'altra area dati. Il drill-down è un'azione che può essere applicata a qualsiasi elemento del report per nascondere e visualizzare altri elementi del report. Tutti questi elementi consentono di organizzare e visualizzare dati in modo da rendere più semplice l'interpretazione del report da parte degli utenti.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SummaryCharacteristics"></a> Riepilogo delle caratteristiche  
 Nella tabella seguente sono riepilogate le diverse caratteristiche. I dettagli sono descritti in apposite sezioni più avanti in questo argomento. Il drill-down non è incluso in questi confronti poiché la relativa azione per mostrare e nascondere può essere applicata a qualsiasi report.  
  
|Caratteristica|Sottoreport|drill-through|annidata|  
|-----------|---------------|------------------|------------|  
|Utilizzo del set di dati del report principale|Uguale o diverso|Uguale o diverso|Uguale|  
|Recupero di dati|I dati vengono recuperati contemporaneamente al report principale|I dati vengono recuperati un report drill-through alla volta|I dati vengono tutti recuperati contemporaneamente al report principale|  
|Elaborazione ed esecuzione del rendering|Con il report principale|Quando si fa clic sul collegamento|Con il report principale|  
|Modalità di esecuzione|Più lenta (ma recupera tutti i dati con il report principale)|Più veloce (ma non recupera tutti i dati con il report principale)|Più veloce (e recupera tutti i dati con il report principale)|  
|Utilizzo di parametri|Yes|Yes|No|  
|Possibilità di riutilizzo|Come report o come sottoreport o report drill-through in altri report|Come report o come sottoreport o report drill-through in altri report|No|  
|Posizione|Esterna al report principale, uguale o diversa dal server di report|Esterna al report principale, uguale al server di report|Interna al report principale|  
|Visualizzazione|Nel report principale|In un report diverso|Nel report principale|  
  

  
##  <a name="Details"></a> Dettagli delle caratteristiche  
  
###  <a name="Datasets"></a> Set di dati utilizzati  
 Sottoreport e report drill-through possono utilizzare lo stesso set di dati del report principale o possono utilizzarne uno diverso. Le aree dati nidificate utilizzano lo stesso set di dati.  
  
###  <a name="RetrieveData"></a> Recupero di dati  
 Sottoreport e aree dati nidificate recuperano dati contemporaneamente al report principale, al contrario dei report drill-through. Ogni report drill-through recupera dati quando un utente fa clic su ogni collegamento. Questo aspetto è importante se è necessario recuperare contemporaneamente i dati del report principale e del report subordinato.  
  
###  <a name="ProcessRender"></a> Elaborazione e rendering  
 Un sottoreport viene elaborato come parte del report principale. Se un sottoreport in cui sono visualizzate informazioni dettagliate su un ordine viene aggiunto, ad esempio, a una cella della tabella nella riga di dettaglio, tale sottoreport verrà elaborato una volta per ogni riga della tabella e ne verrà eseguito il rendering come parte del report principale. L'elaborazione e il rendering di un report drill-through vengono eseguiti solo quando l'utente fa clic sul collegamento drill-through nel report di riepilogo principale.  
  
###  <a name="Performance"></a> restazioni  
 Prima di decidere quale report utilizzare, considerare la possibilità di utilizzare un'area dati anziché un sottoreport, specialmente se il sottoreport non viene utilizzato da più report. Poiché infatti ogni istanza di un sottoreport viene elaborata dal server di report come report distinto, le prestazioni possono risultare rallentate. Le aree dati offrono invece un livello di funzionalità e flessibilità analogo a quello dei sottoreport, ma con prestazioni migliori. Anche i report drill-through offrono prestazioni migliori rispetto ai sottoreport perché non recuperano contemporaneamente tutti i dati insieme al report principale.  
  
###  <a name="Parameters"></a> Utilizzo di parametri  
 I report drill-through e i sottoreport includono in genere parametri di report che specificano i dati del report da visualizzare. Quando ad esempio si fa clic sul numero di un ordine di vendita in un report principale, viene visualizzato un report drill-through che accetta il numero dell'ordine di vendita come parametro e che quindi visualizza tutti i dati per tale ordine di vendita. Quando si crea il collegamento nel report principale, specificare i valori da passare come parametri al report drill-through.  
  
 Per creare un report drill-through o un sottoreport, è necessario progettare innanzitutto il report drill-through di destinazione o il sottoreport e quindi creare un'azione drill-through o aggiungere il riferimento al report principale.  
  
###  <a name="Reusability"></a> Riusabilità  
 Sottoreport e report drill-through sono tipi di report separati. Possono quindi essere utilizzati in numerosi report o visualizzati come report autonomi. Le aree dati nidificate non sono riutilizzabili. Non è possibile salvarli come parti del report perché sono nidificati in un'area dati. È possibile salvare l'area dati che li contiene come parte di un report, ma non l'area dati nidificata.  
  
###  <a name="Location"></a> Percorso  
 Sottoreport e report drill-through sono entrambi report separati, pertanto vengono archiviati all'esterno del report principale. I sottoreport possono trovarsi nello stesso server di report o in uno diverso, mentre i report drill-through devono essere presenti nello stesso server di report. Le aree dati nidificate fanno parte del report principale.  
  
###  <a name="Display"></a> Visualizzazione  
 Sottoreport e aree dati nidificate vengono visualizzati nel report principale. I report drill-through vengono visualizzati separatamente.  
  

  
##  <a name="InThisSection"></a> Contenuto della sezione  
 [Report drill-through &#40;Generatore report e SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md)  
 Sono illustrati i report che vengono visualizzati quando un utente fa clic su un collegamento in un report principale.  
  
 [Sottoreport &#40;Generatore report e SSRS&#41;](subreports-report-builder-and-ssrs.md)  
 Vengono descritti i report visualizzati nel corpo del report principale.  
  
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)  
 Viene descritto come nidificare un'area dati all'interno di un'altra, ad esempio un grafico all'interno di una matrice.  
  
 [Azione di drill-down &#40;Generatore report e SSRS &#41;](drilldown-action-report-builder-and-ssrs.md)  
 Viene spiegato l'utilizzo dell'azione drill-down per nascondere e mostrare elementi del report.  
  
 [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)  
 Viene spiegato come fare riferimento a elementi esterni al file di definizione del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md)  
  
  
