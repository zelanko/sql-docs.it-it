---
title: Istogrammi (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0a71b4311dacf9ea08f12daff8b7610d8f6c49b5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964157"
---
# <a name="column-charts-report-builder-and-ssrs"></a>Column Charts (Report Builder and SSRS)
  In un istogramma le serie vengono visualizzate come set di barre verticali raggruppate per categoria. Gli istogrammi sono utili per mostrare le modifiche ai dati in un periodo di tempo o per illustrare confronti tra elementi. L'istogramma semplice è strettamente correlato al grafico a barre, in cui le serie vengono visualizzate come set di barre orizzontali, e all'istogramma a intervalli, in cui le serie vengono visualizzate come set di barre verticali con punti iniziali e finali variabili. Per altre informazioni, vedere [Grafici a barre &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md) e [Grafici a intervalli &#40;Generatore report e SSRS&#41;](range-charts-report-builder-and-ssrs.md).  
  
 L'istogramma è particolarmente adatto per questi dati, perché tutte e tre le serie condividono lo stesso periodo di tempo, consentendo di eseguire confronti validi.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>Variazioni di un istogramma  
  
-   **In pila**. Istogramma con più serie impilate in verticale. Se il grafico contiene una sola serie, l'istogramma in pila verrà visualizzato come istogramma.  
  
-   **In pila 100%**. Istogramma con più serie impilate in verticale per occupare il 100% dell'area del grafico. Se il grafico contiene una sola serie, tutte le colonne si adatteranno al 100% dell'area del grafico.  
  
-   **Cluster 3D**. Istogramma con le singole serie visualizzate in righe distinte in un grafico 3D.  
  
-   **Cilindro 3D**. Istogramma con le barre a forma di cilindro in un grafico 3D.  
  
-   `Histogram` (Indici per tabelle con ottimizzazione per la memoria). Istogramma calcolato in modo tale che le barre siano disposte in una distribuzione normale.  
  
-   `Pareto` (Indici per tabelle con ottimizzazione per la memoria). Istogramma con le barre disposte dal valore massimo al minimo.  
  
## <a name="data-considerations-for-a-column-chart"></a>Considerazioni sui dati per un istogramma  
  
-   Gli istogrammi e i grafici a barre vengono utilizzati principalmente per indicare i confronti tra gruppi. Se in un grafico sono presenti più di tre serie, è consigliabile utilizzare un grafico a barre o un istogramma in pila. È anche possibile raccogliere i grafici a barre o gli istogrammi in pila in più gruppi, se il grafico contiene diverse serie. Per altre informazioni, vedere [i grafici a barre &#40;Generatore Report e SSRS&#41; ](charts-report-builder-and-ssrs.md) e *istogrammi*.  
  
-   In un istogramma è disponibile meno spazio per la visualizzazione in orizzontale delle etichette dell'asse delle categorie. Se tali etichette sono lunghe, è consigliabile utilizzare un grafico a barre o cambiare l'angolo di rotazione dell'etichetta.  
  
-   È possibile aggiungere stili di disegno speciali alle singole barre di un istogramma per aumentarne l'impatto visivo. Gli stili di disegno includono spicchio, rilievo, cilindro e chiaroscuro. Tali effetti sono progettati per migliorare l'aspetto del grafico 2D. Se si utilizza un grafico 3D, gli stili di disegno vengono comunque applicati, ma non producono lo stesso effetto. Per altre informazioni su come aggiungere uno stile di disegno a un grafico a barre, vedere [Aggiungere stili smussato, rilievo e trama a un grafico &#40;Generatore report e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
-   La caratteristica univoca degli istogrammi è la possibilità di visualizzare il grafico come istogramma classico o grafico di Pareto. A tale scopo, impostare la proprietà ShowColumnAs `Histogram` oppure `Pareto` nella finestra proprietà per `true`.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Grafici a barre &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Grafici a intervalli &#40;Generatore report e SSRS&#41;](range-charts-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un grafico a barre al report &#40;Generatore report&#41;](../tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [Punti dati vuoti e Null nei grafici &#40;Generatore report e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
