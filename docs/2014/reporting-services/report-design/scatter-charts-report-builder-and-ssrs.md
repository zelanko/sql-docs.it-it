---
title: Grafici a dispersione (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e0efa1bd8516dc066b3b3c57b716a3ff90d1158d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294179"
---
# <a name="scatter-charts-report-builder-and-ssrs"></a>Grafici a dispersione (Generatore report e SSRS)
  In un grafico a dispersione le serie vengono visualizzate come set di punti. I valori sono rappresentati dalla posizione dei punti nel grafico. Le categorie sono rappresentate dai diversi simboli marcatori nel grafico. I grafici a dispersione vengono in genere utilizzati per confrontare dati aggregati tra categorie. Per altre informazioni sull'aggiunta di dati a un grafico a dispersione, vedere [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 Nella figura seguente viene illustrato un esempio di grafico a dispersione.  
  
 ![Grafico a dispersione](../media/rs-scatterchart.gif "Grafico a dispersione")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variazioni  
  
-   **A bolle.** I grafici a bolle consentono di visualizzare la differenza tra due valori di un punto dati sulla base delle dimensioni della bolla. Più grande è la bolla, maggiore sarà la differenza tra i due valori.  
  
-   **Bolle 3D**. Grafico a bolle visualizzato in 3D.  
  
## <a name="data-considerations-for-a-scatter-chart"></a>Considerazioni sui dati per un grafico a dispersione  
  
-   I grafici a dispersione vengono in genere utilizzati per visualizzare e confrontare valori numerici, ad esempio dati scientifici, statistici e ingegneristici.  
  
-   Utilizzare un grafico a dispersione quando si desidera confrontare un numero elevato di punti dati senza tener conto del tempo. Maggiore è la quantità di dati inclusi in un grafico a dispersione, migliori saranno i confronti che è possibile effettuare.  
  
-   Per un grafico a bolle sono necessari due valori (massimo e minimo) per ogni punto dati.  
  
-   I grafici a dispersione sono ideali per gestire la distribuzione di valori e cluster di punti dati. Si tratta del tipo di grafico migliore se il set di dati contiene molti punti, ad esempio diverse migliaia. È opportuno evitare di visualizzare più serie in un grafico a punti poiché può causare distrazione. In uno scenario di questo tipo è preferibile utilizzare un grafico a linee.  
  
-   Per impostazione predefinita, nei grafici a dispersione i punti dati vengono visualizzati come cerchi. Se in un grafico a dispersione sono presenti più serie, è preferibile modificare la forma del marcatore di ogni punto in modo che sia quadrata, triangolare, romboidale o comunque diversa.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Grafici a linee &#40;Generatore report e SSRS&#41;](line-charts-report-builder-and-ssrs.md)  
  
  
