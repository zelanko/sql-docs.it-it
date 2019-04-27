---
title: RangeMin (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe9ee0a5fc9c354d24668b828403e937f6d935f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658960"
---
# <a name="rangemin-dmx"></a>RangeMin (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il limite inferiore del bucket stimato individuato per una colonna discretizzata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RangeMin(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonne scalari.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare.  
  
## <a name="remarks"></a>Note  
 Il **RangeMin** funzione può essere utilizzata nelle [SELECT DISTINCT FROM &#60;modello &#62; &#40;DMX&#41; ](../dmx/select-distinct-from-model-dmx.md) query. Quando viene utilizzato con questo tipo di query, il riferimento alla colonna scalare può contenere colonne discrete o continue stimabili o di input.  
  
 Quando abbinata [SELECT FROM &#60;modello&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), il **RangeMin**, **RangeMid**, e **RangeMax**  funzioni restituiscono i valori limite effettivi del bucket specificato. Se ad esempio si esegue una stima su una colonna discretizzata, la query restituirà il numero del bucket stimato nella colonna discretizzata. Il **RangeMin**, **RangeMid**, e **RangeMax** il bucket specificato dalla stima è descritto dalle funzioni. Quando la **RangeMin** funzione viene usata con un'istruzione PREDICTION JOIN, il riferimento alla colonna scalare può contenere solo colonne discrete e stimabili.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i valori minimi, massimi e medi della colonna continua Yearly Income nel modello di data mining TM Decision Tree.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Functions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
  
