---
title: Posizionamento di etichette in un grafico (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc04d47058c1ef1bc3929d941a6680eb013fcc53
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105434"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>Posizionamento di etichette in un grafico (Generatore report e SSRS)
  Poiché ogni tipo di grafico è caratterizzato da una forma diversa, le etichette dei punti dati vengono collocate in una posizione ottimale in modo da non interferire con il grafico. La posizione predefinita delle etichette varia a seconda del tipo di grafico:  
  
-   Sui grafici in pila le etichette possono essere posizionate solo all'interno della serie.  
  
-   Sui grafici a imbuto o a piramide le etichette vengono posizionate all'esterno di una colonna.  
  
-   Sui grafici a torta le etichette vengono posizionate all'interno delle singole sezioni.  
  
-   Sui grafici a barre le etichette vengono posizionate all'esterno delle barre che rappresentano i punti dati.  
  
-   Sui grafici polari le etichette vengono posizionate all'esterno dell'area circolare che rappresenta i punti dati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>Per modificare la posizione delle etichette dei punti dati in un grafico a torta  
  
1.  Creare un grafico a torta.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico, quindi scegliere **Mostra etichette dati**.  
  
3.  Aprire il riquadro Proprietà. Nella scheda **Visualizza** fare clic su **Proprietà**.  
  
4.  Nell'area di progettazione fare clic sul grafico. Le proprietà del grafico verranno visualizzate nel riquadro Proprietà.  
  
5.  Nella sezione **Generale** espandere il nodo **CustomAttributes** . Verrà visualizzato un elenco di attributi per il grafico a torta.  
  
6.  Selezionare un valore per la proprietà PieLabelStyle.  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>Per modificare la posizione delle etichette dei punti in un grafico a imbuto o a piramide  
  
1.  Creare un grafico a imbuto o a piramide.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico, quindi scegliere **Mostra etichette dati**.  
  
3.  Aprire il riquadro Proprietà. Nella scheda **Visualizza** fare clic su **Proprietà**.  
  
4.  Nell'area di progettazione fare clic sul grafico. Le proprietà del grafico verranno visualizzate nel riquadro Proprietà.  
  
5.  Nella sezione **Generale** espandere il nodo **CustomAttributes** . Verrà visualizzato un elenco di attributi per il grafico a imbuto.  
  
6.  Per un grafico a imbuto, selezionare un valore per la proprietà FunnelLabelStyle. Per un grafico a piramide, selezionare un valore per la proprietà PyramidLabelStyle.  
  
    > [!NOTE]  
    >  Quando questa proprietà è impostata su un valore `OutsideInColumn`, le etichette vengono disegnate in una colonna verticale. La posizione della colonna non può essere modificata in alcun modo.  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>Per modificare la posizione delle etichette dei punti dati in un grafico a barre  
  
1.  Creare un grafico a barre.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico, quindi scegliere **Mostra etichette dati**.  
  
3.  Aprire il riquadro Proprietà. Nella scheda **Visualizza** fare clic su **Proprietà**.  
  
4.  Nell'area di progettazione fare clic sul grafico. Le proprietà del grafico verranno visualizzate nel riquadro Proprietà.  
  
5.  Nella sezione **Generale** espandere il nodo **CustomAttributes** . Verrà visualizzato un elenco di attributi per il grafico a barre.  
  
6.  Selezionare un valore per la proprietà BarLabelStyle.  
  
 Quando lo stile delle etichette del grafico a barre è impostato su `Outside`, le etichette vengono posizionate all'esterno della barra, a condizione che la posizione rientri nell'area del grafico. Se l'etichetta non può essere posizionata all'esterno della barra ma all'interno dell'area del grafico, verrà inserita nella posizione più vicina all'estremità della barra.  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>Per modificare la posizione delle etichette dei punti dati in un grafico ad area, a linee, a dispersione o in un istogramma  
  
1.  Creare un grafico ad area, a linee, a dispersione o un istogramma.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico, quindi scegliere **Mostra etichette dati**.  
  
3.  Aprire il riquadro Proprietà. Nella scheda **Visualizza** fare clic su **Proprietà**.  
  
4.  Nell'area di progettazione fare clic sulla serie. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
5.  Nella sezione **Dati** espandere il nodo **DataPoint** e quindi il nodo **Label**.  
  
6.  Selezionare un valore per la proprietà Position.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a torta &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Grafici a barre &#40;Generatore report e SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
