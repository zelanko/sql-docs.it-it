---
title: Impostare l'ambito di sincronizzazione (Generatore report) | Microsoft Docs
description: Impostare l'ambito di sincronizzazione in un report impaginato con indicatori che visualizzano i valori dei dati eseguendo la sincronizzazione nell'intervallo di valori degli indicatori in Generatore report.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ff29909da8662d39cadb064bab66eb14df9d013
ms.sourcegitcommit: f898aa83561e94626024916932568ab05e73b656
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84012594"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>Impostare l'ambito di sincronizzazione (Generatore report e SSRS)
  Nei report impaginati di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] gli indicatori consentono di visualizzare i valori dei dati eseguendo la sincronizzazione nell'intervallo di valori dell'indicatore in un ambito specificato.   
    
  Per impostazione predefinita, l'ambito è il contenitore padre dell'indicatore, ad esempio la tabella o la matrice in cui è contenuto l'indicatore. È possibile modificare la sincronizzazione dell'indicatore a seconda del layout del report. Se, ad esempio, un'area dati quale una tabella dispone di un gruppo di righe, è possibile specificare il gruppo come ambito dell'indicatore. L'indicatore può inoltre omettere la sincronizzazione.  
  
 Opzioni come le unità di misura possono essere impostate tramite espressioni. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Per informazioni generali sull'impostazione dell'ambito all'interno dei report, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="to-change-the-synchronization-scope-of-an-indicator"></a>Per modificare l'ambito di sincronizzazione di un indicatore  
  
1.  Fare clic con il pulsante destro del mouse sull'indicatore da modificare e scegliere **Proprietà indicatore**.  
  
2.  Scegliere **Valori e stati** dal riquadro sinistro.  
  
3.  Nell'elenco **Ambito sincronizzazione** fare clic sull'ambito da applicare.  
  
     L'opzione **(nessuno)** , che consente di rimuovere l'ambito di sincronizzazione dall'indicatore, è sempre disponibile. Le altre opzioni dipendono dal layout del report.  
  
     È possibile fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che imposta l'ambito.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Indicatori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
