---
title: Impostare un valore minimo o massimo su un misuratore (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c7a9ad23124105443349720d2d5769fb9227db2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105033"
---
# <a name="set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs"></a>Impostare un valore minimo o massimo su un misuratore (Generatore report e SSRS)
  A differenza del grafico in cui sono definiti più gruppi, il misuratore mostra un solo valore. Poiché Generatore report e Progettazione report possono determinare il significato contestuale o relativo del valore che si sta tentando di visualizzare sul misuratore, è necessario definire il valore minimo e massimo per la scala. Se, ad esempio, i valori dei dati sono ranghi compresi tra 0 e 10, è possibile impostare il valore minimo su 0 e quello massimo su 10. I numeri dell'intervallo vengono calcolati automaticamente in base ai valori specificati per l'impostazione minima e massima. Per impostazione predefinita, i valori minimo e massimo vengono impostati su 0 e 100, ovvero due valori arbitrari che è necessario modificare. L'applicazione non calcola il valore come percentuale.  
  
 Se l'intervallo dei valori è grande, ad esempio da 0 a 10000, utilizzare un moltiplicatore per ridurre il numero di zero sul misuratore. Il moltiplicatore ridurrà solo la scala dei numeri sul misuratore, non il valore stesso.  
  
 È possibile usare espressioni per impostare i valori delle opzioni **Minimo** e **Massimo** . Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-minimum-and-maximum-on-the-gauge"></a>Per impostare i valori minimo e massimo sul misuratore  
  
1.  Fare clic con il pulsante destro del mouse sulla scala e selezionare **Proprietà scala**. Verrà visualizzata la finestra di dialogo **Proprietà scala** .  
  
2.  In **Generale**specificare un valore per **Minimo**. Per impostazione predefinita, questo valore è 0. Se lo si desidera, fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione che imposta il valore per l'opzione.  
  
3.  Specificare un valore per **Massimo**. Per impostazione predefinita, tale valore è 100. Se lo si desidera, fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione che imposta il valore per l'opzione.  
  
4.  (Facoltativo) Se i valori per le impostazioni Minimo e Massimo sono elevati, specificare un valore per l'opzione **Moltiplica etichette di scala per** . Per specificare un moltiplicatore in modo da ridurre la scala, utilizzare un numero decimale. Se, ad esempio, si dispone di una scala compresa tra 0 e 1000, è possibile specificare un valore di moltiplicatore pari a 0,01 per ridurre la scala ai valori compresi tra 0 e 10.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di scale su un misuratore &#40;Generatore report e SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formattazione degli indicatori di misura su un misuratore &#40;Generatore report e SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
