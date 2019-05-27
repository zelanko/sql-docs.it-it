---
title: Aggiungere o rimuovere i margini da un grafico (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ce2fcfe65c3b674f89b3174fd1e88421a7bdb853
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106541"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>Aggiungere o rimuovere i margini da un grafico (Generatore report e SSRS)
  Nei tipi di grafico istogramma e a dispersione vengono automaticamente aggiunti margini laterali alle estremità dell'asse X. Nei tipi di grafico a barre vengono automaticamente aggiunti margini laterali alle estremità dell'asse Y. In tutti gli altri tipi di grafico non vengono aggiunti margini laterali. Non è possibile modificare le dimensioni del margine.  
  
 Questo argomento non è applicabile per grafici a torta, ad anello, a imbuto o a piramide.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-or-disable-side-margins"></a>Per abilitare o disabilitare i margini laterali  
  
1.  Fare clic con il pulsante destro del mouse sull'asse e selezionare **Proprietà asse**. Verrà visualizzata la finestra di dialogo **Proprietà asse verticale** o **orizzontale** .  
  
2.  Nella pagina **Opzioni asse** impostare la proprietà **Margini laterali** :  
  
    -   **Automatico** Il grafico determinerà se aggiungere o meno un margine laterale in base al tipo di grafico.  
  
    -   **Disabilitato** I grafici a barre, a dispersione e gli istogrammi non disporranno di margini laterali.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà asse, Opzioni asse &#40;Generatore report e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRSSSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
