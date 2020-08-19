---
description: PredictAssociation (DMX)
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b94af0ab8da71e5bf978852fd884d46b460715bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426153"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Consente di stimare l'appartenenza associativa.  
  
Ad esempio, è possibile usare la funzione PredictAssociation per ottenere il set di raccomandazioni dato lo stato corrente del carrello acquisti per un cliente. 
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Algoritmi che contengono tabelle nidificate stimabili, tra cui associazioni e alcuni algoritmi di classificazione. Gli algoritmi di classificazione che supportano le tabelle nidificate includono gli [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi Decision Trees, [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes e [!INCLUDE[msCoName](../includes/msconame-md.md)] Neural Network.  
  
## <a name="return-type"></a>Tipo restituito  
 \<table expression>  
  
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
  
  
