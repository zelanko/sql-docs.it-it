---
description: PredictSequence (DMX)
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 31f99205f3e23db23c5c2a38750f75212763e8de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426103"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Vengono stimati i valori di sequenza futuri per un set specificato di dati in sequenza.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>Tipo restituito  
 Oggetto \<table expression>.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificato il parametro *n* , vengono restituiti i valori seguenti:  
  
-   Se *n* è maggiore di zero, i valori di sequenza più probabili nei successivi *n* passaggi.  
  
-   Se vengono specificati sia *n-Start* che *n-end* , i valori di sequenza da *n-Start* a *n-end*.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita una sequenza dei cinque prodotti che più probabilmente verranno acquistati da un cliente nel database [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] in base al modello di data mining Sequence Clustering.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
