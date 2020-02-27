---
title: Formattazione degli intervalli su un misuratore (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1540979cedf5fc77675e7bca3036ddd6524bcc8e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77079647"
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>Formattazione di intervalli su un misuratore (Generatore report e SSRS)
 In un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , l'intervallo del misuratore è un'area sulla scala del misuratore tramite cui viene indicata un'importante sottosezione dei valori sul misuratore. L'uso di un intervallo del misuratore consente di indicare visivamente quando il valore dell'indicatore di misura rientra in un determinato intervallo di valori. Gli intervalli sono definiti da un valore iniziale e un valore finale.  
  
 È anche possibile utilizzare gli intervalli per definire le diverse sezioni di un misuratore. Su un misuratore con valori compresi tra 0 e 10 è ad esempio possibile definire un intervallo rosso contenente i valori da 0 a 3, un intervallo giallo contenente i valori da 4 a 7 e un intervallo verde contenente i valori da 8 a 10. Se il valore iniziale specificato è maggiore di quello finale specificato, i valori vengono scambiati in modo che quello iniziale diventi quello finale e viceversa.  
  
 È possibile posizionare l'intervallo con una procedura analoga a quella che consente di posizionare gli indicatori di misura su una scala. La posizione dell'intervallo dipende dalle proprietà **Posizione** e **Distanza dalla scala** . Per altre informazioni, vedere [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di scale su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formattazione degli indicatori di misura su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Impostare un valore minimo o massimo su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiunta di un indicatore di prestazioni chiave al report &#40;Generatore report&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
