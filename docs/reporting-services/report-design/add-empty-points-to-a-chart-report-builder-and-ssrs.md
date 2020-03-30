---
title: Aggiungere punti vuoti a un grafico (Generatore Report) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65b97d3f50eec05574a9f7463678ca7da09e2492
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081652"
---
# <a name="add-empty-points-to-a-chart-report-builder-and-ssrs"></a>Aggiunta di punti vuoti a un grafico (Generatore Report e SSRS)
Nel grafico i valori Null vengono visualizzati come spazi o intervalli vuoti tra punti dati in una serie. Nei report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i punti vuoti sono punti dati che possono essere inseriti nello spazio vuoto creato dai valori Null.  
  
 Per impostazione predefinita i punti vuoti vengono calcolati considerando la media tra il punto dati precedente e quello successivo che contiene un valore. È possibile modificare questa situazione in modo che tutti i punti vuoti vengano inseriti nella posizione zero.  
  
 Per altre informazioni, vedere [Punti dati vuoti e Null nei grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-empty-points-on-a-chart"></a>Per specificare punti vuoti in un grafico  
  
1.  Aprire il riquadro Proprietà.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sulla serie che contiene valori Null. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
3.  Espandere il nodo **EmptyPoint** .  
  
4.  Selezionare un valore del colore per la proprietà Color.  
  
5.  Nel nodo **EmptyPoint** espandere il nodo Marker.  
  
6.  Selezionare un tipo di marcatore per la proprietà MarkerType.  
  
    > [!NOTE]  
    >  È necessario selezionare un tipo di marcatore per aggiungere punti vuoti a una barra, a una colonna oppure a un grafico a dispersione. Per i grafici ad area, a linee e radar, tuttavia, la selezione di un tipo di marcatore è facoltativa poiché nel grafico lo spazio vuoto o l'intervallo viene riempito senza che sia necessario specificare un marcatore.  
  
7.  Impostare il valore del punto vuoto.  
  
    1.  Nel riquadro Proprietà espandere il nodo **CustomAttributes** .  
  
    2.  Impostare la proprietà EmptyPointValue. Per inserire punti vuoti in una posizione relativa alla media dei punti dati precedente e successivo, selezionare **Media**. Per inserire punti vuoti nella posizione zero, selezionare **Zero**.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Aggiungere cambi di scala a un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
