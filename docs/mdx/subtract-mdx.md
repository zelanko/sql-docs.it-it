---
title: '- Sottrarre (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3b8003bdeddea32f80636dc10a78e200d6b0e0be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036679"
---
# <a name="--subtract-mdx"></a>- (sottrazione) (MDX)


  Esegue un'operazione aritmetica che sottrae un numero da un altro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric_Expression - Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *Numeric_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore con il tipo di dati del parametro con precedenza maggiore.  
  
## <a name="remarks"></a>Osservazioni  
 È necessario che alle due espressioni sia applicato lo stesso tipo di dati oppure che un'espressione possa essere convertita in modo implicito nel tipo di dati dell'altra espressione. Se una delle due espressioni restituisce un valore Null, l'operatore restituirà il risultato dell'altra espressione.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
-- This member returns the increase or decrease  
-- in gross profit margin over a month.  
WITH MEMBER [Measures].[GPM Delta] AS  
 (  
(Measures.[Gross Profit Margin]) -   
([Date].[Calendar].CurrentMember.PrevMember,   
Measures.[Gross Profit Margin])  
  ), FORMAT_STRING = 'Percent'  
  
SELECT   
DESCENDANTS(  
[Date].[Calendar].[Calendar Year].&[2002],   
[Date].[Calendar].[Month]) ON 0,  
[Product].[Category].[Category].Members ON 1  
FROM  
[Adventure Works]  
WHERE  
([Measures].[GPM Delta])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
