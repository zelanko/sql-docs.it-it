---
title: Grafici a linee (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 194e6679-890d-4a3e-a756-130d32ef7e29
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 20e9e6626bbd08eebfe69a04f63ed882979b34d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580154"
---
# <a name="line-charts-report-builder-and-ssrs"></a>Grafici a linee (Generatore report e SSRS)
  In un grafico a linee le serie vengono visualizzate come set di punti collegati da una singola linea. I grafici a linee vengono utilizzati per rappresentare grandi quantità di dati che si verificano nell'arco di un periodo di tempo continuo. Per altre informazioni sull'aggiunta di dati a un grafico a linee, vedere [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 Nella figura seguente è illustrato un grafico a linee contenente tre serie.  
  
 ![Grafico a linee](../../reporting-services/report-design/media/rs-linechart.gif "Grafico a linee")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variazioni  
  
-   **Linee smussate**. Grafico a linee in cui viene utilizzata una linea curva anziché regolare.  
  
-   **Linee con rientri**. Grafico a linee in cui viene utilizzata una linea con rientri anziché regolare. I punti vengono collegati tramite una linea in modo simile ai gradini di una scala.  
  
-   **Grafici sparkline**. Le variazioni del grafico a linee in cui viene visualizzata solo la serie di linee nella cella di una tabella o matrice. Per altre informazioni, vedere [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="data-considerations-for-line-charts"></a>Considerazioni sui dati per i grafici a linee  
  
-   Per migliorare l'impatto visivo del grafico a linee predefinito, impostare lo spessore del bordo della serie su 3 e aggiungere un offset dell'ombreggiatura pari a 1. In questo modo verrà creato un grafico a linee più spesse. Se si sceglie un altro tipo di grafico, sarà necessario ripristinare i valori originali di queste proprietà.  
  
-   Se il set di dati include valori vuoti, nel grafico a linee verranno aggiunti punti vuoti sotto forma di linee segnalibro per mantenere la continuità nel grafico. Se non si desidera visualizzare tali linee, utilizzare un tipo di grafico non contiguo per rappresentare il set di dati, ad esempio un grafico a barre o un istogramma.  
  
-   Un grafico a linee richiede almeno due punti per disegnare una linea.  Se il set di dati contiene un unico punto dati, il grafico a linee verrà visualizzato come marcatore di un singolo punto dati.  
  
-   Una serie disegnata come linea non occupa molto spazio all'interno di un'area del grafico.  Per questo motivo, i grafici a linee vengono spesso combinati con altri tipi di grafico, ad esempio istogrammi. Tuttavia, non è possibile combinare un grafico a linee con i tipo di grafico a barre, polare, a torta o con forme.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Istogrammi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Grafici ad aree &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)   
 [Punti dati vuoti e Null nei grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
