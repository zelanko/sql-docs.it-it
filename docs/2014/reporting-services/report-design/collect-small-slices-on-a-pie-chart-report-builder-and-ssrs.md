---
title: Raccogliere piccole sezioni in un grafico a torta (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c85692c3ae50df88c59d2622fc1ca06925413ba2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940867"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>Raccogliere piccole sezioni in un grafico a torta (Generatore report e SSRS)
  Quando in un grafico a torta viene visualizzato un numero eccessivo di punti dati, l'aspetto finale risulta poco chiaro. Per risolvere questo problema, è possibile visualizzare tutti i dati al di sotto di un determinato valore come un'unica sezione del grafico a torta.  
  
 Per raccogliere le piccole sezioni in un'unica sezione, determinare innanzitutto se la soglia deve essere misurata come percentuale del grafico a torta o come valore fisso. Impostare le proprietà CollectedThreshold e CollectedThresholdUsePercent. Impostare la proprietà CollectedThreshold su una percentuale del grafico che il valore di raccolta non deve superare o il valore dei dati soglia effettivo per la raccolta. Impostare la proprietà CollectedThresholdUsePercent su `True` per usare una percentuale o `False` usare un valore effettivo.  
  
 È anche possibile raccogliere le piccole sezioni in un secondo grafico a torta derivato da una sezione del primo grafico ottenuta tramite raccolta. Il secondo grafico a torta verrà disegnato a destra di quello originale.  
  
 Non è possibile combinare in un'unica sezione le sezioni di grafici a imbuto o a piramide.  
  
 Un esempio di questo grafico è disponibile come report di esempio. Per altre informazioni sul download di questo e di altri report di esempio, vedere[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][Report Builder and Report Designer sample reports](https://go.microsoft.com/fwlink/?LinkId=198283) (Report di esempio di Generatore report e Progettazione report).  
  
### <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>Per raccogliere le piccole sezioni in una singola sezione di un grafico a torta  
  
1.  Aprire il riquadro Proprietà.  
  
2.  Nell'area di progettazione fare clic su una sezione del grafico a torta. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
3.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
4.  Impostare la proprietà CollectedStyle su **SingleSlice**.  
  
5.  Impostare il valore soglia e il tipo di soglia per la raccolta. Di seguito sono riportati alcuni esempi comuni di impostazione di queste soglie.  
  
    -   **Per percentuale.** Ad esempio, per raccogliere in un'unica sezione tutte le sezioni del grafico a torta minori del 10%:  
  
         Impostare la proprietà CollectedThresholdUsePercent su `True`.  
  
         Impostare la proprietà CollectedThreshold su **10**.  
  
        > [!NOTE]  
        >  Se si imposta CollectedStyle su **SingleSlice**, CollectedThreshold su un valore maggiore **100**, e CollectedThresholdUsePercent è `True`, il grafico genererà un'eccezione perché non è possibile calcolare una percentuale. Per risolvere questo problema, impostare CollectedThreshold su un valore inferiore a **100**.  
  
    -   **Per valore di dati.** Ad esempio, per raccogliere in un'unica sezione tutte le sezioni del grafico a torta inferiori a 5000:  
  
         Impostare la proprietà CollectedThresholdUsePercent su `False`.  
  
         Impostare la proprietà CollectedThreshold su **5000**.  
  
6.  Impostare la proprietà CollectedLabel su una stringa che rappresenta l'etichetta di testo che verrà visualizzata nella sezione raccolta.  
  
7.  (Facoltativo) Impostare le proprietà CollectedSliceExploded, CollectedColor, CollectedLegendText e CollectedToolTip. Queste proprietà consentono di modificare l'aspetto, il colore, il testo di etichette e legende e l'aspetto delle descrizioni comando della singola sezione.  
  
### <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>Per raccogliere le piccole sezioni in un grafico a torta secondario  
  
1.  Completare i passaggi da 1 a 3 descritti sopra.  
  
2.  Impostare la proprietà CollectedStyle su **CollectedPie**.  
  
3.  Impostare la proprietà CollectedThresholdproperty su un valore che rappresenta la soglia in corrispondenza della quale le sezioni piccole verranno raccolte in un'unica sezione. Quando la proprietà CollectedStyle è impostata **CollectedPie**, la proprietà CollectedThresholdUsePercentproperty è sempre impostata su `True`, e la soglia raccolta viene sempre misurata in percentuale.  
  
4.  (Facoltativo) Impostare le proprietà CollectedColor, CollectedLabel, CollectedLegendText e CollectedToolTip. Tutte le altre proprietà denominate "Collected" non si applicano alla torta raccolta.  
  
> [!NOTE]  
>  Il grafico a torta secondario viene calcolato in base alle piccole sezioni di dati, in modo che verrà visualizzato solo in anteprima, non nell'area di progettazione.  
  
> [!NOTE]  
>  Non è possibile formattare il grafico a torta secondario. Per questo motivo, si consiglia di utilizzare il primo approccio per la raccolta delle sezioni della torta.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a torta &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Visualizzare i valori in percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Aggiungere effetti 3D a un grafico &#40;Generatore report e SSRS&#41;](chart-effects-add-3d-effects-report-builder.md)  
  
  
