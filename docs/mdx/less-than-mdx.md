---
title: '&lt; (Minore di) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 70a22115250fd525e4451a5aa110fa4bb61da306
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905700"
---
# <a name="lt-less-than-mdx"></a>&lt; (Minore di) (MDX)


  Esegue un'operazione di confronto che determina se il valore di un'espressione MDX (Multidimensional Expression) è minore di quello di un'altra espressione MDX.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MDX_Expression < MDX_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *MDX_Expression*  
 Espressione MDX valida.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano basato sulle condizioni seguenti:  
  
-   **true** se entrambi i parametri sono non null e il primo parametro è un valore che è inferiore al valore del secondo parametro.  
  
-   **false** se entrambi i parametri sono non null e il primo parametro è un valore che è uguale a o maggiore del valore del secondo parametro.  
  
-   Null se uno o entrambi i parametri restituiscono un valore Null.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is less than 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] < .3,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
