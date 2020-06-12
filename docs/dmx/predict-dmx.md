---
title: Predict (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a21336db54ab6fadaa219a3ef3d743dcf860087
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669270"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La funzione **Predict** restituisce un valore stimato, o un set di valori, per una colonna specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Riferimento a colonna scalare o a colonna di tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<riferimento a colonna scalare>  
  
 oppure  
  
 \<riferimento a colonne di tabella>  
  
 Il tipo restituito dipende dal tipo di colonna a cui è applicata la funzione.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS sono applicabili solo a riferimenti a colonne di tabella, mentre EXCLUDE_NULL e INCLUDE_NULL sono applicabili solo a riferimenti a colonne scalari.  
  
## <a name="remarks"></a>Commenti  
 Le opzioni disponibili includono EXCLUDE_NULL (predefinita), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predefinita), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Per i modelli Time Series, la funzione Predict non supporta INCLUDE_STATISTICS.  
  
 Se è specificato il parametro INCLUDE_NODE_ID, nel risultato verrà restituita la colonna $NODEID. NODE_ID è il nodo di contenuto su cui viene eseguita la stima per un case specifico. Questo parametro è facoltativo quando si utilizza Predict per le colonne della tabella.  
  
 Il parametro *n* si applica alle colonne della tabella. Imposta il numero delle righe restituite in base al tipo di stima. Se la colonna sottostante è Sequence, viene chiamata la funzione **PredictSequence** . Se la colonna sottostante è Time Series, viene chiamata la funzione **PredictTimeSeries** . Per i tipi associativi di stima, viene chiamata la funzione **PredictAssociation** .  
  
 La funzione **Predict** supporta il polimorfismo.  
  
 Vengono spesso utilizzate le seguenti forme abbreviate alternative:  
  
-   [Gender] è un'alternativa per **Predict**([gender], EXCLUDE_NULL).  
  
-   [Products Purchases] è un'alternativa per **Predict**([Products Purchases], EXCLUDE_NULL, Exclusive).  
  
    > [!NOTE]  
    >  Il tipo restituito da questa funzione viene a sua volta gestito come riferimento a colonna. Ciò significa che la funzione **Predict** può essere utilizzata come argomento in altre funzioni che accettano un riferimento di colonna come argomento (ad eccezione della funzione **Predict** ).  
  
 Il passaggio di INCLUDE_STATISTICS a una stima in una colonna con valori di tabella aggiunge le colonne **$Probability** e **$support** alla tabella risultante. che descrivono la probabilità dell'esistenza del record della tabella nidificata associato.  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente viene utilizzata la funzione Predict per restituire i quattro prodotti del database Adventure Works che con maggiore probabilità verranno venduti insieme. Poiché la funzione stima in base a un modello di data mining Association Rules, USA automaticamente la funzione **PredictAssociation** , come descritto in precedenza.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 Risultati dell'esempio:  
  
 Questa query restituisce una singola riga di dati con una sola colonna, `Expression`, che però contiene la seguente tabella nidificata.  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
