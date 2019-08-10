---
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 701d8fb43b468f6bbd33fbff9ff7cfc8deb386f9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893832"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Viene restituito il valore di supporto per uno stato specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonna scalare.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare del tipo specificato dal riferimento *\<* *>* a una colonna scalare.  
  
## <a name="remarks"></a>Note  
 Se lo stato stimato viene omesso, verrà utilizzato lo stato con la più alta probabilità stimabile, escludendo il bucket degli stati mancanti. Per includere il bucket degli stati mancanti, impostare \<il > di stato stimato su **INCLUDE_NULL**.  
  
 Per restituire il supporto per gli stati mancanti, impostare lo \<stato stimato > su null.  
  
> [!NOTE]  
>  I valori di supporto vengono calcolati in modo diverso o potrebbero essere interpretati in modo diverso a seconda del tipo di modello su cui si esegue la query. Per ulteriori informazioni sul calcolo del supporto per un tipo di modello specifico, vedere il tipo di algoritmo singolo nel [contenuto &#40;del modello di data mining&#41;Analysis Services-Data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
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
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni &#40;di stima generali DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
