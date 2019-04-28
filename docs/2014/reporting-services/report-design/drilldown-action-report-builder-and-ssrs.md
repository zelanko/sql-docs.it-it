---
title: Azione di drill-down (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- sql12.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql12.rtp.rptdesigner.seriesproperties.visibility.f1
- sql12.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10092"
- sql12.rtp.rptdesigner.textboxproperties.visibility.f1
- sql12.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10167"
- sql12.rtp.rptdesigner.rectangleproperties.visibility.f1
- "10174"
- sql12.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10155"
- "10123"
- sql12.rtp.rptdesigner.subreportproperties.visibility.f1
- "10425"
- sql12.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- "10217"
- sql12.rtp.rptdesigner.axisproperties.visibility.f1
- sql12.rtp.rptdesigner.serieslabelproperties.visibility.f1
- "10161"
- sql12.rtp.rptdesigner.chartproperties.visibility.f1
- sql12.rtp.rptdesigner.legendproperties.visibility.f1
- sql12.rtp.rptdesigner.pictureproperties.visibility.f1
- "10215"
- "10258"
- "10144"
- "10062"
- "10053"
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b939882e5021eb08925f974bad71d1720c6eff7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825310"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>Azione di drill-down (Generatore report e SSRS)
  Fornendo più o meno icone in una casella di testo, è possibile consentire agli utenti di nascondere e visualizzare gli elementi in modo interattivo. Questa azione viene chiamata *drill-down* . Per una tabella o una matrice, è possibile visualizzare o nascondere le righe e le colonne statiche o le righe e le colonne associate ai gruppi.  
  
 ![rs_drilldown](../media/rs-drilldown.gif "rs_drilldown")  
  
 In questa illustrazione l'utente fa clic sui segni più (+) nel report per mostrare dati dettaglio.  
  
 È ad esempio possibile nascondere inizialmente tutte le righe, ad eccezione della riga di riepilogo del gruppo esterno di una tabella con gruppi di righe. Per ogni gruppo interno, incluso il gruppo dettagli, aggiungere un'icona per espandere o comprimere alla cella di raggruppamento del gruppo contenitore. Dopo il rendering del report, l'utente può fare clic sulla casella di testo per espandere e comprimere i dati dettaglio. Per altre informazioni, vedere [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md).  
  
 Per consentire agli utenti di espandere o comprimere un elemento, impostare le proprietà di visibilità per tale elemento.  
  
> [!NOTE]  
>  Quando si crea un report con un'azione drill-down, è necessario impostare le informazioni relative alla visibilità sul gruppo, la colonna o la riga da nascondere e non solo su una singola casella di testo nella riga o nella colonna. Inoltre, la casella di testo utilizzata per l'elemento Toggle deve trovarsi in un ambito contenitore che controlla l'elemento da visualizzare o nascondere.  
>   
>  Per nascondere, ad esempio, una riga associata a un gruppo nidificato, la casella di testo deve trovarsi in una riga associata al gruppo padre o a un elemento di livello superiore nella gerarchia di contenimento.  
>   
>  Per informazioni sull'impostazione delle informazioni di visibilità sul gruppo, sulla colonna o sulla riga, vedere [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)  
  
 Per altre informazioni su come nascondere elementi di report, vedere [Nascondere un elemento &#40;Generatore report e SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>Confronto tra report drill-down e drill-through  
 In un report drill-down un utente fa clic su un pulsante più o meno per espandere o comprimere una sezione di un report per mostrare dati dettaglio. I un report drill-through l'utente fa clic su un collegamento relativo a un valore di riepilogo, aprendo in questo modo un report separato, correlato contenente dati dettaglio. I dati dettaglio vengono recuperati solo quando il report dettagli è in esecuzione. I report drill-through richiedono in genere un numero di risorse minore rispetto ai report drill-down. Per altre informazioni, vedere [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>Supporto delle estensioni per il rendering per elementi del report nascosti  
 L'elemento Toggle per visualizzare e nascondere gli elementi del report è supportato solo dalle estensioni per il rendering che supportano funzioni di interattività con gli utenti, ad esempio l'estensione per il rendering HTML utilizzata durante l'esecuzione di un report in Generatore report e in Gestione report. Le altre estensioni per il rendering consentono di visualizzare gli elementi nascosti. Nell'elenco seguente viene descritto il supporto per gli elementi del report con visibilità condizionale:  
  
-   In HTML, se gli elementi sono nascosti, non sono visibili nell'origine HTML.  
  
-   Le estensioni per il rendering XML visualizzano tutti gli elementi del report, anche se nascosti.  
  
-   L'estensione per il rendering Excel visualizza ed espande le righe e le colonne nascoste di una tabella, una matrice o un elenco. Tutte le righe e le colonne sono visibili.  
  
 Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
