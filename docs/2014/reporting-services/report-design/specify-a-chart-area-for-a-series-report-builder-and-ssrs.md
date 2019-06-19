---
title: Specificare un'area del grafico per una serie (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10157"
- sql12.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 14fc5556e430cf364b004cd02ebd0278da650867
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104966"
---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>Specificare un'area del grafico per una serie (Generatore report e SSRS)
  Il grafico è il contenitore di livello superiore che include il bordo esterno, il titolo del grafico e la legenda. Per impostazione predefinita, il grafico contiene una sola area predefinita. L'area del grafico non è visibile sulla superficie del grafico, ma è possibile considerarla come un contenitore che include solo le etichette e il titolo degli assi, nonché l'area tracciato di una o più serie. Nell'illustrazione seguente viene mostrato il concetto di aree del grafico all'interno di un singolo grafico.  
  
 ![Visualizza un'area del grafico](../media/chartareasdiagram.gif "Visualizza un'area del grafico")  
  
 Per impostazione predefinita, tutte le serie vengono aggiunte all'area del grafico predefinita. Quando si utilizzano grafici ad area, a dispersione, a linee e istogrammi, qualsiasi combinazione di queste serie può essere visualizzata nella stessa area del grafico. Se nella stessa area del grafico sono contenute diverse serie, la leggibilità del grafico risulterà ridotta. Potrebbe essere necessario separare i tipi di grafico in più aree del grafico allo scopo di migliorare la leggibilità e semplificare il confronto. I grafici azionari relativi a prezzi e volumi, ad esempio, includono spesso intervalli di valori differenti. È tuttavia possibile confrontare dati che si riferiscono allo stesso periodo di tempo.  
  
 Le serie a barra, polare o con forme possono essere combinate solo con serie degli stessi tipi di grafico nella stessa area del grafico. Se si utilizza un grafico polare o con forme, è consigliabile utilizzare un'area dati del grafico separata per ogni campo da visualizzare.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-series-with-a-new-chart-area"></a>Per associare una serie a una nuova area del grafico  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi del grafico e scegliere **Aggiungi nuova area grafico**. Sul grafico verrà visualizzata una nuova area vuota.  
  
2.  Fare clic con il pulsante destro del mouse sulla serie nel grafico o su un campo serie o dati nell'area appropriata del riquadro Dati grafico, quindi fare clic su **Proprietà serie**.  
  
3.  In **Assi e area grafico**selezionare l'area del grafico in cui si desidera visualizzare la serie.  
  
4.  (Facoltativo) Allineare le aree del grafico in senso verticale. A questo scopo, fare clic con il pulsante destro del mouse sul grafico e scegliere **Proprietà area grafico**. In **Allineamento**selezionare un'altra area del grafico con la quale si desidera allineare l'area del grafico selezionata.  
  
## <a name="see-also"></a>Vedere anche  
 [Più serie in un grafico &#40;Generatore report e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Definire i colori in un grafico mediante la tavolozza &#40;Generatore report e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Grafici polari &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Grafici con forme &#40;Generatore report e SSRS&#41;](shape-charts-report-builder-and-ssrs.md)   
 [Grafici a torta &#40;Generatore report e SSRS&#41;](pie-charts-report-builder-and-ssrs.md)  
  
  
