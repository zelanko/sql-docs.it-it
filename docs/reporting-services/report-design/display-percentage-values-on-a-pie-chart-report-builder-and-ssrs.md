---
title: Display Percentage Values on a Pie Chart (Report Builder and SSRS) (Visualizzare i valori in percentuale in un grafico a torta (Generatore report e SSRS)) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fab9a9c5f6fbdbf3201ba597102450bad0d95629
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578196"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Visualizzare i valori in percentuale in un grafico a torta (Generatore report e SSRS)
Nei report impaginati [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], per impostazione predefinita la legenda visualizza tutte le categorie. È anche possibile visualizzare le percentuali nella legenda o nelle sezioni del grafico a torta.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 L'[Esercitazione: Aggiungere un grafico a torta al report (Generatore report)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)spiega come aggiungere le percentuali alle sezioni, se per iniziare si preferisce provare con dati di esempio.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Per visualizzare valori in percentuale come etichette in un grafico a torta  
  
1.  Aggiungere un grafico a torta al report. Per altre informazioni, vedere [Aggiungere un grafico a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sulla torta e scegliere **Mostra etichette dati**. Le etichette dati dovrebbero apparire in ogni sezione del grafico a torta.  
  
3.  Nell'area di progettazione fare clic con il pulsante destro del mouse sulle etichette e scegliere **Proprietà etichetta serie**. Verrà visualizzata la finestra di dialogo **Proprietà etichetta serie** .  
  
4.  Digitare **#PERCENT** per l'opzione **Dati etichetta** .  
  
5.  (Facoltativo) Per specificare il numero di cifre decimali da visualizzare nell'etichetta, digitare "#PERCENT{P*n*}" dove *n* è il numero di cifre decimali da visualizzare. Ad esempio per non visualizzare posizioni decimali, digitare "#PERCENT{P0}."  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Per visualizzare valori in percentuale nella legenda di un grafico a torta  
  
1.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico a torta e scegliere **Proprietà serie**. Verrà visualizzata la finestra di dialogo **Proprietà serie** .  
  
2.  In **Legenda**digitare **#PERCENT** per la proprietà **Testo legenda personalizzato** .  
  
## <a name="see-also"></a>Vedere anche  
* [Esercitazione: Aggiungere un grafico a torta al report (Generatore report)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Grafici a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formattazione della legenda in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
