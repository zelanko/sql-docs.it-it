---
title: Report drill-through (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 938a6450-67c1-4eef-80b4-8fdaefeed584
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63119bf6d8ba4e9d907b9c6cdfb6bfe0b7765941
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105939"
---
# <a name="drillthrough-reports-report-builder-and-ssrs"></a>Report drill-through (Generatore report e SSRS)
  Un report drill-through è un report aperto da un utente facendo clic su un collegamento in un altro report. Nei report drill-through sono solitamente disponibili dettagli relativi a un elemento contenuto in un report di riepilogo originale. In questa illustrazione, ad esempio, il report di riepilogo delle vendite include gli ordini di vendita e i totali. Quando un utente fa clic su un numero di ordine nell'elenco di riepilogo, viene aperto un altro report contenente i dettagli relativi a tale ordine.  
  
 ![rs_DrillThru](../media/rs-drillthru.gif "rs_DrillThru")  
  
 I dati del report drill-through non vengono recuperati fino a quando l'utente non fa clic sul collegamento nel report principale che determina l'apertura del report drill-through. Se è necessario recuperare contemporaneamente i dati del report principale e il report drill-through, utilizzare un sottoreport. Per altre informazioni, vedere [Sottoreport &#40;Generatore report e SSRS&#41;](subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Quando si utilizza Generatore report, per visualizzare il report drill-through che viene aperto quando si fa clic sul collegamento drill-through nel report principale, è necessario essere connessi a un server di report.  
  
 Per una rapida introduzione ai report drill-through, vedere [Esercitazione: Creazione di report drill-through e report principali &#40;Generatore report&#41;](../tutorial-creating-drillthrough-and-main-reports-report-builder.md). Report drill-through è disponibile anche in due soluzioni di business intelligence, [BI Reporting: Scenari di report e sottoscrizioni](https://technet.microsoft.com/bi/ff769487.aspx) e [nei dashboard aziendali: Soluzione di vendita](https://technet.microsoft.com/bi/ff643005.aspx)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="parameters-in-drillthrough-reports"></a>Parametri nei report drill-through  
 In un report drill-through sono contenuti in genere i parametri passati a tale report dal report di riepilogo. Nel report di riepilogo di esempio relativo alle vendite è contenuto il campo [OrderNumber] in una casella di testo di una cella della tabella. Nel report drill-through è contenuto un parametro che accetta il numero di ordine come valore. Quando si imposta il collegamento al report drill-through nella casella di testo per [OrderNumber], è necessario impostare il parametro per il report di destinazione su [OrderNumber]. Quando l'utente fa clic sul numero di ordine nel report di riepilogo, verrà aperto un report dettagliato di destinazione in cui vengono visualizzate le informazioni relative al numero di ordine. Per visualizzare istruzioni sulla personalizzazione di report drill-through basati sui valori dei parametri, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md) e [Funzione InScope &#40;Generatore report e SSRS&#41;](report-builder-functions-inscope-function.md).  
  
## <a name="designing-the-drillthrough-report"></a>Progettazione del report drill-through  
 Per creare un report drill-through, è necessario progettare il report prima di creare un'azione drill-through nel report principale.  
  
 Un report drill-through può essere qualsiasi report. Tale report accetta in genere uno o più parametri per specificare i dati da visualizzare, a seconda del collegamento corrispondente nel report principale. Se ad esempio il collegamento del report principale è stato definito per un ordine di vendita, al report drill-through verrà passato il numero dell'ordine di vendita.  
  
## <a name="creating-a-drillthrough-action-in-the-main-report"></a>Creazione di un'azione drill-through nel report principale  
 È possibile aggiungere collegamenti drill-through a caselle di testo (incluso il testo nelle celle di una tabella o matrice), immagini, grafici, misuratori e qualsiasi altro elemento del report che dispone di una pagina delle proprietà Azione. Per altre informazioni, vedere [Aggiungere un'azione drill-through a un report &#40;Generatore report e SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
 È possibile creare l'azione drill-through nel report principale come azione del report o azione URL. Per un'azione del report, il report drill-through deve essere presente nello stesso server di report del report principale. Per un'azione URL, il report deve essere presente nel percorso URL completo. Il modo in cui si specifica un report potrebbe essere diverso per un server di report o un sito di SharePoint integrato con un server di report. Se il server di report viene configurato in modalità integrata SharePoint, solo le azioni URL sono supportate.  
  
 Per altre informazioni, vedere [Aggiungere un'azione drill-through a un report &#40;Generatore report e SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) e [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
## <a name="viewing-a-drillthrough-report"></a>Visualizzazione di un report drill-through  
 Per visualizzare un report di riepilogo con i collegamenti drill-through dopo la pubblicazione, è necessario verificare che i report drill-through si trovino nello stesso server di report del report di riepilogo. In tutti i casi, all'utente devono essere concesse le autorizzazioni necessarie per visualizzare il report drill-through.  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through, drill-down, sottoreport e aree dati annidate &#40;Generatore report e SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
