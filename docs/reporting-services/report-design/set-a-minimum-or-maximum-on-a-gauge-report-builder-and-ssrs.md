---
title: Impostare un valore minimo o massimo su un misuratore (Generatore report) | Microsoft Docs
description: Informazioni sulle differenze tra il misuratore e i grafici in un report impaginato. In Generatore report è necessario definire i valori minimo e massimo della scala.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2277867a1709ddaa735c00934468800c23841548
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84886579"
---
# <a name="set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs"></a>Impostare un valore minimo o massimo su un misuratore (Generatore report e SSRS)
  A differenza dei grafici in un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , in cui sono definiti più gruppi, i misuratori mostrano un solo valore. Poiché Generatore report e Progettazione report possono determinare il significato contestuale o relativo del valore che si sta tentando di visualizzare sul misuratore, è necessario definire il valore minimo e massimo per la scala.   
    
  Se, ad esempio, i valori dei dati sono ranghi compresi tra 0 e 10, è possibile impostare il valore minimo su 0 e quello massimo su 10. I numeri dell'intervallo vengono calcolati automaticamente in base ai valori specificati per l'impostazione minima e massima. Per impostazione predefinita, i valori minimo e massimo vengono impostati su 0 e 100, ovvero due valori arbitrari che è necessario modificare. L'applicazione non calcola il valore come percentuale.  
  
 Se l'intervallo dei valori è grande, ad esempio da 0 a 10000, utilizzare un moltiplicatore per ridurre il numero di zero sul misuratore. Il moltiplicatore ridurrà solo la scala dei numeri sul misuratore, non il valore stesso.  
  
 È possibile usare espressioni per impostare i valori delle opzioni **Minimo** e **Massimo** . Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## <a name="to-set-the-minimum-and-maximum-on-the-gauge"></a>Per impostare i valori minimo e massimo sul misuratore  
  
1.  Fare clic con il pulsante destro del mouse sulla scala e selezionare **Proprietà scala**. Verrà visualizzata la finestra di dialogo **Proprietà scala** .  
  
2.  In **Generale**specificare un valore per **Minimo**. Per impostazione predefinita, questo valore è 0. Se lo si desidera, fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione che imposta il valore per l'opzione.  
  
3.  Specificare un valore per **Massimo**. Per impostazione predefinita, tale valore è 100. Se lo si desidera, fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione che imposta il valore per l'opzione.  
  
4.  (Facoltativo) Se i valori per le impostazioni Minimo e Massimo sono elevati, specificare un valore per l'opzione **Moltiplica etichette di scala per** . Per specificare un moltiplicatore in modo da ridurre la scala, utilizzare un numero decimale. Se, ad esempio, si dispone di una scala compresa tra 0 e 1000, è possibile specificare un valore di moltiplicatore pari a 0,01 per ridurre la scala ai valori compresi tra 0 e 10.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di scale su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formattazione degli indicatori di misura su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
