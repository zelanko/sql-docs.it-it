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
ms.openlocfilehash: ea0a9915e062d7b6f15b63e18976e88cc339202d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "76939502"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di stimare l'appartenenza associativa.  
  
Ad esempio, è possibile usare la funzione PredictAssociation per ottenere il set di raccomandazioni dato lo stato corrente del carrello acquisti per un cliente. 
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Algoritmi che contengono tabelle nidificate stimabili, tra cui associazioni e alcuni algoritmi di classificazione. Gli algoritmi di classificazione che supportano le tabelle nidificate includono [!INCLUDE[msCoName](../includes/msconame-md.md)] gli [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi Decision Trees [!INCLUDE[msCoName](../includes/msconame-md.md)] , Naive Bayes e Neural Network.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella>  
  
## <a name="remarks"></a>Osservazioni  
 Le opzioni per la funzione **PredictAssociation** includono EXCLUDE_NULL, INCLUDE_NULL, inclusive, Exclusive (default), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS sono applicabili solo a riferimenti a colonne di tabella, mentre EXCLUDE_NULL e INCLUDE_NULL sono applicabili solo a riferimenti a colonne scalari.  
  
 INCLUDE_STATISTICS restituisce solo **$Probability** e **$AdjustedProbability**.  
  
 Se viene specificato il parametro numerico *n* , la funzione **PredictAssociation** restituisce i primi n valori più probabili in base alla probabilità:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Se si include **$AdjustedProbability**, l'istruzione restituisce i primi *n* valori in base al **$AdjustedProbability**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata la funzione **PredictAssociation** per restituire i quattro prodotti del database Adventure Works che con maggiore probabilità verranno venduti insieme.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
Nell'esempio seguente viene illustrato come è possibile utilizzare una tabella nidificata come input per la funzione di stima, utilizzando la clausola SHAPE. La query SHAPE crea un set di righe con customerId come una colonna e una tabella nidificata come seconda colonna, che contiene l'elenco dei prodotti già portati da un cliente. 

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
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
