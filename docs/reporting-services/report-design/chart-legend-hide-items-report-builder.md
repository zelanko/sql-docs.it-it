---
title: Nascondere elementi della legenda nel grafico (Generatore report) | Microsoft Docs
description: Informazioni su come scegliere elementi visualizzati nella legenda per visualizzare i dati essenziali in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f745b3eb2c862f4105bcdd872a8915845341942
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681420"
---
# <a name="chart-legend---hide-items-report-builder"></a>Legenda del grafico - Nascondere elementi (Generatore report)
Per impostazione predefinita, qualsiasi serie aggiunta a un grafico senza forme in un report impaginato di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verrà aggiunta come elemento nella legenda. Per grafici a torta, ad anello, a imbuto e a piramide, qualsiasi serie aggiunta al grafico determina l'aggiunta di punti dati singoli nella legenda.  
  
 È possibile nascondere qualsiasi elemento della legenda. Quando si nasconde un elemento della legenda, questo rimane comunque visualizzato nel grafico. Ciò si rivela utile nelle situazioni in cui non si desidera mostrare ulteriori informazioni per una serie aggiunta al grafico. Se ad esempio è stata aggiunta una serie calcolata come una media mobile al grafico, potrebbe essere necessario nascondere questa voce nella legenda in modo che vengano mostrate informazioni aggiuntive solo per la serie originale.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>Per nascondere un elemento visualizzato nella legenda  
  
1.  Fare clic con il pulsante destro del mouse sulla serie da nascondere e scegliere **Proprietà serie**.  
  
2.  Fare clic su **Legenda**. Selezionare l'opzione **Non mostrare questa serie in una legenda** .  
  
    > [!NOTE]  
    >  Non è possibile nascondere una serie per un solo gruppo. Se è stato aggiunto un campo all'area **Gruppi di serie** , verranno nascoste tutte le serie che appartengono a questo gruppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione della legenda in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Modificare il testo di un elemento legenda &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [Aggiungere una media mobile a un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà legenda, Generale &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  
