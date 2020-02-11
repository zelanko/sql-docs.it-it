---
title: Azione di drill-down (Generatore report e SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- "10092"
- "10167"
- "10174"
- sql13.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10155"
- sql13.rtp.rptdesigner.chartproperties.visibility.f1
- sql13.rtp.rptdesigner.pictureproperties.visibility.f1
- sql13.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10123"
- "10425"
- sql13.rtp.rptdesigner.axisproperties.visibility.f1
- "10217"
- "10161"
- "10215"
- sql13.rtp.rptdesigner.legendproperties.visibility.f1
- "10258"
- "10144"
- sql13.rtp.rptdesigner.subreportproperties.visibility.f1
- sql13.rtp.rptdesigner.textboxproperties.visibility.f1
- "10062"
- sql13.rtp.rptdesigner.serieslabelproperties.visibility.f1
- sql13.rtp.rptdesigner.rectangleproperties.visibility.f1
- sql13.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql13.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10053"
- sql13.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- sql13.rtp.rptdesigner.seriesproperties.visibility.f1
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee55b7c5b6e5fc1d65f5914cc2850e204c0c0c2e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579012"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>Azione di drill-down (Generatore report e SSRS)
Le icone più e meno in una casella di testo consentono agli utenti di nascondere o visualizzare gli elementi in modo interattivo. Questa azione viene chiamata *drill-down* . Per una tabella o una matrice, è possibile visualizzare o nascondere le righe e le colonne statiche o le righe e le colonne associate ai gruppi.  
  
 ![rs_drilldown](../../reporting-services/report-design/media/rs-drilldown.gif "rs_drilldown")  
  
 In questa illustrazione l'utente fa clic sui segni più (+) nel report per mostrare dati dettaglio.  
  
 È ad esempio possibile nascondere inizialmente tutte le righe, ad eccezione della riga di riepilogo del gruppo esterno di una tabella con gruppi di righe. Per ogni gruppo interno, incluso il gruppo dettagli, aggiungere un'icona per espandere o comprimere alla cella di raggruppamento del gruppo contenitore. Dopo il rendering del report, l'utente può fare clic sulla casella di testo per espandere e comprimere i dati dettaglio. Per altre informazioni, vedere [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
 Per consentire agli utenti di espandere o comprimere un elemento, impostare le proprietà di visibilità per tale elemento.  
  
> [!NOTE]  
>  Quando si crea un report con un'azione drill-down, è necessario impostare le informazioni relative alla visibilità sul gruppo, la colonna o la riga da nascondere e non solo su una singola casella di testo nella riga o nella colonna. Inoltre, la casella di testo utilizzata per l'elemento Toggle deve trovarsi in un ambito contenitore che controlla l'elemento da visualizzare o nascondere.  
>   
>  Per nascondere, ad esempio, una riga associata a un gruppo nidificato, la casella di testo deve trovarsi in una riga associata al gruppo padre o a un elemento di livello superiore nella gerarchia di contenimento.  
>   
>  Per informazioni sull'impostazione delle informazioni di visibilità sul gruppo, sulla colonna o sulla riga, vedere [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)  
  
 Per altre informazioni su come nascondere elementi di report, vedere [Nascondere un elemento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>Confronto tra report drill-down e drill-through  
 In un report drill-down un utente fa clic su un pulsante più o meno per espandere o comprimere una sezione di un report per mostrare dati dettaglio. I un report drill-through l'utente fa clic su un collegamento relativo a un valore di riepilogo, aprendo in questo modo un report separato, correlato contenente dati dettaglio. I dati dettaglio vengono recuperati solo quando il report dettagli è in esecuzione. I report drill-through richiedono in genere un numero di risorse minore rispetto ai report drill-down. Per altre informazioni, vedere [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>Supporto delle estensioni per il rendering per elementi del report nascosti  
 L'elemento per visualizzare e nascondere gli elementi del report è supportato solo dalle estensioni per il rendering che supportano l'interattività con gli utenti, ad esempio l'estensione per il rendering HTML usata durante l'esecuzione di un report in Generatore report e nel portale Web. Le altre estensioni per il rendering consentono di visualizzare gli elementi nascosti. Nell'elenco seguente viene descritto il supporto per gli elementi del report con visibilità condizionale:  
  
-   In HTML, se gli elementi sono nascosti, non sono visibili nell'origine HTML.  
  
-   Le estensioni per il rendering XML visualizzano tutti gli elementi del report, anche se nascosti.  
  
-   L'estensione per il rendering Excel visualizza ed espande le righe e le colonne nascoste di una tabella, una matrice o un elenco. Tutte le righe e le colonne sono visibili.  
  
 Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
