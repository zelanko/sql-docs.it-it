---
title: Add Bevel, Emboss, and Texture Styles to a Chart (Aggiungere gli stili smussato, rilievo e trama a un grafico (Generatore report e SSRS)) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b25d12646a2662cb5c6ab8f2a9b510aa02d7c49b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106275"
---
# <a name="add-bevel-emboss-and-texture-styles-to-a-chart-report-builder-and-ssrs"></a>Aggiungere stili smussato, rilievo e trama a un grafico (Generatore report e SSRS)
  Quando si utilizzano determinati tipi di grafico, è possibile specificare un effetto di disegno per aumentarne l'effetto visivo. Tali effetti vengono applicati solo alle serie, mentre non influiscono su altri elementi del grafico.  
  
 Quando si utilizza una variante di un grafico a torta o ad anello, è possibile specificare uno stile di disegno con contorni sfumati o concavo, simile agli effetti smussato o rilievo applicabili a un'immagine.  
  
 Quando si utilizza una variante di un grafico a barre o di un istogramma, è possibile applicare stili di trama, ad esempio cilindro, spicchio e chiaroscuro, alle singole barre o colonne.  
  
 Oltre a questi stili di disegno, è possibile aggiungere bordi e ombreggiature a molti elementi del grafico per conferire un effetto ottico di profondità. Per altre informazioni su altri modi per formattare il grafico, vedere [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>Per aggiungere gli stili smussato o rilievo a un grafico a torta o ad anello  
  
1.  Nella scheda **Visualizza** selezionare **Proprietà** per aprire il riquadro Proprietà.  
  
2.  Selezionare il grafico a torta o ad anello che si desidera ottimizzare. Selezionare un campo di dati nel grafico, non tutto il grafico.  
  
3.  Nel riquadro Proprietà espandere il nodo **CustomAttributes** .  
  
4.  Per PieDrawingStyle selezionare uno stile dall'elenco a discesa.  
  
> [!NOTE]  
>  Non è possibile disporre di stili 3D e smussato o rilievo nello stesso grafico. Una volta abilitato lo stile 3D per il grafico, la proprietà PieDrawingStyle non verrà visualizzata.  
  
 ![Grafico a torta con stile di disegno concavo](../media/rs-piedrawingeffects-concave.gif "Grafico a torta con stile di disegno concavo")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>Per aggiungere gli stili di trama a un grafico a barre o a un istogramma  
  
1.  Selezionare il grafico a barre o l'istogramma che si desidera ottimizzare. Selezionare un campo di dati nel grafico, non tutto il grafico.  
  
2.  Aprire il riquadro Proprietà.  
  
3.  Espandere il nodo **CustomAttributes** .  
  
4.  Per DrawingStyle selezionare uno stile dall'elenco a discesa.  
  
> [!NOTE]  
>  Non è possibile disporre di stili 3D e smussato o rilievo nello stesso grafico. Una volta abilitato lo stile 3D per il grafico, la proprietà PieDrawingStyle non verrà visualizzata.  
  
 ![Grafico a barre con effetto di disegno LightToDark](../media/rs-bardrawingeffects-lighttodark.gif "Grafico a barre con effetto di disegno LightToDark")  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a barre &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Istogrammi &#40;Generatore report e SSRS&#41;](column-charts-report-builder-and-ssrs.md)   
 [Grafici a torta &#40;Generatore report e SSRS&#41;](pie-charts-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
