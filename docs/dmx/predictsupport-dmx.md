---
description: PredictSupport (DMX)
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cea4913bf3668c89fb0c1c66632359a372f3d54b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422255"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Viene restituito il valore di supporto per uno stato specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonna scalare.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare del tipo specificato da *\<*scalar column reference*>* .  
  
## <a name="remarks"></a>Osservazioni  
 Se lo stato stimato viene omesso, verrà utilizzato lo stato con la più alta probabilità stimabile, escludendo il bucket degli stati mancanti. Per includere il bucket degli stati mancanti, impostare \<predicted state> su **INCLUDE_NULL**.  
  
 Per restituire il supporto per gli stati mancanti, impostare \<predicted state> su null.  
  
> [!NOTE]  
>  I valori di supporto vengono calcolati in modo diverso o potrebbero essere interpretati in modo diverso a seconda del tipo di modello su cui si esegue la query. Per ulteriori informazioni sul modo in cui viene calcolato il supporto per un tipo di modello specifico, vedere il singolo tipo di algoritmo nel [contenuto del modello di data mining &#40;Analysis Services-&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata una query singleton per stimare se un individuo sarà un acquirente di biciclette e determinare il supporto per la stima sulla base del modello di data mining TM Decision Tree.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
