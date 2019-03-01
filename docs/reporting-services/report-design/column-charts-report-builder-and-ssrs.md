---
title: Istogrammi (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0ddc125d91802441f0788f4beaca0369d40b5c01
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285959"
---
# <a name="column-charts-report-builder-and-ssrs"></a>Column Charts (Report Builder and SSRS)
  In un istogramma le serie vengono visualizzate come set di barre verticali raggruppate per categoria. Gli istogrammi sono utili per mostrare le modifiche ai dati in un periodo di tempo o per illustrare confronti tra elementi. L'istogramma semplice è strettamente correlato al grafico a barre, in cui le serie vengono visualizzate come set di barre orizzontali, e all'istogramma a intervalli, in cui le serie vengono visualizzate come set di barre verticali con punti iniziali e finali variabili. Per altre informazioni, vedere [Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md) e [Grafici a intervalli &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md).  
  
 L'istogramma è particolarmente adatto per questi dati, perché tutte e tre le serie condividono lo stesso periodo di tempo, consentendo di eseguire confronti validi.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>Variazioni di un istogramma  
  
-   **In pila**. Istogramma con più serie impilate in verticale. Se il grafico contiene una sola serie, l'istogramma in pila verrà visualizzato come istogramma.  
  
-   **In pila 100%**. Istogramma con più serie impilate in verticale per occupare il 100% dell'area del grafico. Se il grafico contiene una sola serie, tutte le colonne si adatteranno al 100% dell'area del grafico.  
  
-   **Cluster 3D**. Istogramma con le singole serie visualizzate in righe distinte in un grafico 3D.  
  
-   **Cilindro 3D**. Istogramma con le barre a forma di cilindro in un grafico 3D.  
  
-   **Istogramma classico**. Istogramma calcolato in modo tale che le barre siano disposte in una distribuzione normale.  
  
-   **Pareto**. Istogramma con le barre disposte dal valore massimo al minimo.  
  
## <a name="data-considerations-for-a-column-chart"></a>Considerazioni sui dati per un istogramma  
  
-   Gli istogrammi e i grafici a barre vengono utilizzati principalmente per indicare i confronti tra gruppi. Se in un grafico sono presenti più di tre serie, è consigliabile utilizzare un grafico a barre o un istogramma in pila. È anche possibile raccogliere i grafici a barre o gli istogrammi in pila in più gruppi, se il grafico contiene diverse serie. Per altre informazioni, vedere [Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
-   In un istogramma è disponibile meno spazio per la visualizzazione in orizzontale delle etichette dell'asse delle categorie. Se tali etichette sono lunghe, è consigliabile utilizzare un grafico a barre o cambiare l'angolo di rotazione dell'etichetta.  
  
-   È possibile aggiungere stili di disegno speciali alle singole barre di un istogramma per aumentarne l'impatto visivo. Gli stili di disegno includono spicchio, rilievo, cilindro e chiaroscuro. Tali effetti sono progettati per migliorare l'aspetto del grafico 2D. Se si utilizza un grafico 3D, gli stili di disegno vengono comunque applicati, ma non producono lo stesso effetto. Per altre informazioni su come aggiungere uno stile di disegno a un grafico a barre, vedere [Aggiungere stili smussato, rilievo e trama a un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
-   La caratteristica univoca degli istogrammi è la possibilità di visualizzare il grafico come istogramma classico o grafico di Pareto. A tale scopo, nella finestra Proprietà impostare la proprietà ShowColumnAs - **Istogramma** o **Pareto** su **true**.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Grafici a intervalli &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un grafico a barre al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [Punti dati vuoti e Null nei grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
