---
title: Aggiungere un rettangolo o un contenitore (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2079eeb5cb871b5006ac4b2c45b60e9c8a3a3c97
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574778"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Aggiungere un rettangolo o un contenitore (Generatore report e SSRS)
  Aggiungere un rettangolo al report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] quando si desidera separare le aree del report con un elemento grafico, enfatizzare aree del report o fornire uno sfondo per uno o più elementi del report. I rettangoli sono utilizzati anche come contenitori per consentire di controllare il rendering di aree dati in un report. È possibile personalizzare l'aspetto di un rettangolo modificandone le proprietà quali lo sfondo e i colori del bordo. Per altre informazioni sull'uso di un rettangolo come contenitore, vedere [Rettangoli e linee &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) e [Visualizzare dati identici in una matrice e in un grafico &#40;Generatore report&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).    
   
## <a name="to-add-a-rectangle"></a>Per aggiungere un rettangolo    
    
1.  Nella gruppo **Elementi del report** della scheda **Inserisci** fare clic su **Rettangolo**.    
    
2.  Fare clic sul punto in cui si desidera posizionare l'angolo superiore sinistro del rettangolo nell'area di progettazione, quindi trascinare fino al punto in cui si desidera posizionare l'angolo inferiore destro.    
    
     Si noti che quando si sposta il cursore, le "guide di allineamento" vengono visualizzate quando il cursore viene allineato agli altri oggetti sull'area di progettazione. In tal modo si semplifica l'allineamento degli oggetti.    
    
## <a name="to-create-a-container"></a>Per creare un contenitore    
    
1.  Aggiungere un elemento del report Rettangolo al report.    
    
2.  Trascinare altri elementi del report nel rettangolo.    
    
    > [!NOTE]    
    >  Un rettangolo è solo un contenitore di elementi che in esso vengono creati o trascinati. Se si disegna un rettangolo intorno a un elemento esistente nell'area di progettazione, il rettangolo non agirà da contenitore.    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>Per modificare le proprietà del rettangolo, ad esempio colore, stile o spessore    
    
1.  Selezionare il rettangolo, quindi fare clic sull'opzione del colore, dello stile o dello spessore della linea nella sezione **Bordo** della scheda Home.    
    
2.  Fare clic sulla freccia accanto al pulsante **Bordo** per determinare i lati del rettangolo da modificare.    
    
    > [!NOTE]    
    >  Se si imposta lo stile di linea su **Doppio** e lo spessore di linea è minore o uguale a 1,5 punti, è possibile che la linea non venga visualizzata come doppia quando si esegue il report in Generatore report o Progettazione report o nel portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Risulterà doppia quando si esporta il report in altri formati, ad esempio Microsoft Word e Acrobat PDF.    
    
## <a name="see-also"></a>Vedere anche    
 [Rettangoli e linee &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
