---
title: Tipi di grafico (Generatore report e SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9c041a300e9d64e5446f43a68f675f2290dd8963
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581651"
---
# <a name="chart-types-report-builder-and-ssrs"></a>Tipi di grafico (Generatore report e SSRS)

È importante scegliere un tipo di grafico appropriato per il tipo di dati da visualizzare. Tale scelta risulta infatti fondamentale per una corretta interpretazione dei dati visualizzati nel grafico. Se ad esempio il set di dati contiene un numero di punti dati particolarmente elevato rispetto alla dimensioni del grafico, è opportuno rappresentarlo in un grafico ad area, a linee o a dispersione. Per informazioni dettagliate sulla preparazione dei dati in base al tipo di grafico selezionato, vedere [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>Scelta del tipo di grafico  
 A ogni tipo di grafico sono associate caratteristiche univoche per agevolare la visualizzazione del set di dati. Per visualizzare i dati, è possibile usare qualsiasi tipo di grafico, tuttavia la lettura dei dati risulterà facilitata se si sceglie un tipo di grafico adatto ai dati, basato su quanto si intende visualizzare nel report. Nella tabella seguente sono riepilogate le caratteristiche dei grafici che rendono un grafico più o meno appropriato a seconda di un determinato set di dati.  
  
 È possibile modificare il tipo di grafico dopo averlo creato. Per altre informazioni, vedere [Modificare un tipo di grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md).  
  
 Molti esempi di questi tipi di grafici sono disponibili come report di esempio. Per altre informazioni sul download di report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
|Tipo di grafico|Visualizzazione di dati proporzionali|Visualizzazione di dati azionari|Visualizzazione di dati lineari|Visualizzazione di dati multivalore|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[Grafici ad aree &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Barre dei dati](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Istogrammi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Grafici a linee &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Grafici a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||||  
|[Grafici polari &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||||  
|[Grafici a intervalli &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|  
|[Grafici a dispersione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||  
|[Grafici con forme &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||||  
|[Grafici sparkline](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|  
|[Grafici azionari &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "Disponibile")|  

## <a name="next-steps"></a>Passaggi successivi

[Grafici](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Punti dati vuoti e Null nei grafici](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[Aggiungere un grafico a un report](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
