---
title: Visualizzare le etichette dei punti dati al di fuori di un grafico a torta (Generatore report) | Microsoft Docs
description: Informazioni sul fatto che la visualizzazione delle etichette all'esterno di un grafico a torta può creare più spazio per etichette dati più lunghe in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e09f4cd21015c0e1933154685e954fadd017943c
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462245"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>Visualizzazione delle etichette dei punti dati al di fuori di un grafico a torta (Generatore report e SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]le etichette del grafico a torta sono ottimizzate per essere visualizzate solo su diverse sezioni di dati. Se il grafico a torta contiene un numero eccessivo di sezioni, è possibile che le etichette si sovrappongano. Per risolvere questo problema, è possibile visualizzare le etichette al di fuori del grafico a torta, lasciando più spazio per le etichette dati più lunghe. Se le etichette continuano a sovrapporsi, è possibile creare più spazio abilitando gli effetti 3D. In questo modo il diametro del grafico a torta viene ridotto, creando uno spazio maggiore intorno al grafico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>Per visualizzare le etichette dei punti dati all'interno di un grafico a torta  
  
1.  Aggiungere un grafico a torta al report. Per altre informazioni, vedere [Aggiungere un grafico a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse sul grafico, quindi scegliere **Mostra etichette dati**.  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>Per visualizzare le etichette dei punti dati al di fuori di un grafico a torta  
  
1.  Creare un grafico a torta e visualizzare le etichette dati.  
  
2.  Aprire il riquadro Proprietà.  
  
3.  Nell'area di progettazione fare clic sulla torta stessa per visualizzare le proprietà **Categoria** nel riquadro Proprietà.  
  
4.  Espandere il nodo **CustomAttributes** . Verrà visualizzato un elenco di attributi per il grafico a torta.  
  
5.  Impostare la proprietà **PieLabelStyle** su **Outside**.  
  
6.  Impostare la proprietà **PieLineColor** su **Black**. La proprietà PieLineColor definisce le righe di callout per ogni etichetta di punti dati.  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>Per impedire la sovrapposizione delle etichette visualizzate all'esterno di un grafico a torta  
  
1.  Creare un grafico a torta con etichette esterne.  
  
2.  Nell'area di progettazione fare clic con il pulsante destro del mouse all'esterno del grafico a torta, ma all'interno dei bordi del grafico e selezionare **Proprietà area grafico**. Viene visualizzata la finestra di dialogo **Proprietà area grafico** .  
  
3.  Nella scheda **Opzioni 3D** selezionare **Abilita 3D**.  
  
4.  Se si desidera maggior spazio nel grafico per le etichette mantenendo un aspetto bidimensionale, impostare le proprietà **Rotazione** e **Inclinazione** su **0**.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Raccogliere piccole sezioni in un grafico a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Visualizzazione di valori percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
