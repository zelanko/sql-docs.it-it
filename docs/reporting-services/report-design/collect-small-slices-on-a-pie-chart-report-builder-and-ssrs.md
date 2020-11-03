---
title: Raccogliere piccole sezioni in un grafico a torta (Generatore report) | Microsoft Docs
description: Informazioni sulla raccolta di molte piccole sezioni molte in un grafico a torta in un'unica sezione nei report impaginati di Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4e51e1a12f28ae18ff6ba833ace19a1a97ba72dd
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907239"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>Raccogliere piccole sezioni in un grafico a torta (Generatore report e SSRS)
I grafici a torta con un numero eccessivo di sezioni potrebbero apparire poco chiari. In questo articolo viene illustrato come raccogliere molte piccole sezioni in un grafico a torta in un'unica sezione nei report impaginati di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].
 
 Per raccogliere le piccole sezioni in un'unica sezione, determinare innanzitutto se la soglia deve essere misurata come percentuale del grafico a torta o come valore fisso. 
 
 L'[Esercitazione: Aggiungere un grafico a torta al report (Generatore report)](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)spiega come raccogliere più sezioni di piccole dimensioni in un'unica sezione, se per iniziare si preferisce provare con dati di esempio.
 
 ![Screenshot di un grafico a torta di Generatore report che mostra la sezione Other.](../../reporting-services/report-design/media/report-builder-pie-chart-other-slice.png)
  
 È anche possibile raccogliere le piccole sezioni in un secondo grafico a torta derivato da una sezione del primo grafico ottenuta tramite raccolta. Il secondo grafico a torta verrà disegnato a destra di quello originale.  
  
 Non è possibile combinare in un'unica sezione le sezioni di grafici a imbuto o a piramide.  
  
 
## <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>Per raccogliere le piccole sezioni in una singola sezione di un grafico a torta  
  
1.  Aprire il riquadro Proprietà.  
  
2.  Nell'area di progettazione fare clic su una sezione del grafico a torta. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
3.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
4.  Impostare la proprietà CollectedStyle su **SingleSlice**.  

    ![Screenshot di un grafico a torta di Generatore report che Mostra come configurare una proprietà su singola sezione.](../../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
  
5.  Impostare il valore soglia e il tipo di soglia per la raccolta. Di seguito sono riportati alcuni esempi comuni di impostazione di queste soglie.  
  
    -   **Per percentuale.** Ad esempio, per raccogliere in un'unica sezione tutte le sezioni del grafico a torta minori del 10%:  
  
         Impostare la proprietà CollectedThresholdUsePercent su **True**.  
  
         Impostare la proprietà CollectedThreshold su **10**.  
  
        > [!NOTE]  
        >  Se si imposta CollectedStyle su **SingleSlice** , CollectedThreshold su un valore maggiore di **100** e CollectedThresholdUsePercent su **True** , il grafico genererà un'eccezione perché non riesce a calcolare una percentuale. Per risolvere questo problema, impostare CollectedThreshold su un valore inferiore a **100**.  
  
    -   **Per valore di dati.** Ad esempio, per raccogliere in un'unica sezione tutte le sezioni del grafico a torta inferiori a 5000:  
  
         Impostare la proprietà CollectedThresholdUsePercent su **False**.  
  
         Impostare la proprietà CollectedThreshold su **5000**.  
  
6.  Impostare la proprietà CollectedLabel su una stringa che rappresenta l'etichetta di testo che verrà visualizzata nella sezione raccolta.  
  
7.  (Facoltativo) Impostare le proprietà CollectedSliceExploded, CollectedColor, CollectedLegendText e CollectedToolTip. Queste proprietà consentono di modificare l'aspetto, il colore, il testo di etichette e legende e l'aspetto delle descrizioni comando della singola sezione.  
  
## <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>Per raccogliere le piccole sezioni in un grafico a torta secondario  
  
1.  Completare i passaggi da 1 a 3 descritti sopra.  
  
2.  Impostare la proprietà CollectedStyle su **CollectedPie**.  
  
3.  Impostare la proprietà CollectedThresholdproperty su un valore che rappresenta la soglia in corrispondenza della quale le sezioni piccole verranno raccolte in un'unica sezione. Quando la proprietà CollectedStyle è impostata su **CollectedPie** , la proprietà CollectedThresholdUsePercentproperty è sempre impostata su **True** e la soglia raccolta viene sempre misurata in percentuale.  
  
4.  (Facoltativo) Impostare le proprietà CollectedColor, CollectedLabel, CollectedLegendText e CollectedToolTip. Tutte le altre proprietà denominate "Collected" non si applicano alla torta raccolta.  
  
> [!NOTE]  
>  Il grafico a torta secondario viene calcolato in base alle piccole sezioni di dati, in modo che verrà visualizzato solo in anteprima, non nell'area di progettazione.  
  
> [!NOTE]  
>  Non è possibile formattare il grafico a torta secondario. Per questo motivo, si consiglia di utilizzare il primo approccio per la raccolta delle sezioni della torta.  
  
## <a name="see-also"></a>Vedere anche  
* [Esercitazione: Aggiungere un grafico a torta al report (Generatore report)](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)
*  [Grafici a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
*  [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
*  [Visualizzazione di valori percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)     
  
