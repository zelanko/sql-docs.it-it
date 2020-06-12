---
title: Ritardo (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 04b06d1cbe14ee83915bd5626337720acf9bd2a9
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670338"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce l'intervallo di tempo tra la data del case corrente e l'ultima data del set di training.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare di tipo integer.  
  
## <a name="remarks"></a>Commenti  
 Se la funzione **lag** viene utilizzata in un modello in cui la colonna Key Time si trova all'interno di una tabella nidificata, la funzione deve trovarsi all'interno della selezione secondaria dell'istruzione.  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente vengono restituiti i casi che rientrano negli ultimi 12 mesi dei dati utilizzati per il training del modello.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
