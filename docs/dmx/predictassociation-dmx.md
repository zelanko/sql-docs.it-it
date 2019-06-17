---
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a23407b546bcde2dd1fde81654da4fe861e0719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501839"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di stimare l'appartenenza associativa.  
  
Ad esempio, è possibile usare la funzione PredictAssociation per ottenere il set di raccomandazioni ha lo stato corrente del carrello acquisti per cliente. 
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Algoritmi che contengono tabelle nidificate stimabili, tra cui alcuni algoritmi di classificazione e associazione. Gli algoritmi di classificazione che supportano le tabelle nidificate includono la [!INCLUDE[msCoName](../includes/msconame-md.md)] alberi delle decisioni [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, e [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi Neural Network.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella >  
  
## <a name="remarks"></a>Note  
 Le opzioni per la **PredictAssociation** funzione includono EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predefinita), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS sono applicabili solo a riferimenti a colonne di tabella, mentre EXCLUDE_NULL e INCLUDE_NULL sono applicabili solo a riferimenti a colonne scalari.  
  
 INCLUDE_STATISTICS restituisce solo **$Probability** e **$AdjustedProbability**.  
  
 Se il parametro numerico *n* è specificato, il **PredictAssociation** funzione restituisce i primi n valori più probabili in base alla probabilità:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Se si include **$AdjustedProbability**, l'istruzione restituisce le prime *n* valori in base il **$AdjustedProbability**.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente usa il **PredictAssociation** funzione per restituire i quattro prodotti Adventure Works di database che sono probabilmente verranno venduti insieme.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
Nell'esempio seguente viene illustrato come è possibile usare una tabella nidificata come input per la funzione di stima utilizzando la clausola SHAPE. Query SHAPE crea un set di righe con customerId come una sola colonna e una tabella nidificata come una seconda colonna, che contiene l'elenco dei prodotti di che un cliente ha già evidenziato. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Functions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
