---
title: '* (Crossjoin) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 132b237fd8baa9c50dc254b02d90ed95d7159a0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249615"
---
# <a name="crossjoin----mdx-operator-reference"></a>Crossjoin - riferimento agli operatori MDX


  Esegue un'operazione sui set che restituisce il prodotto incrociato di due set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>Parametro  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="return-value"></a>Valore restituito  
 Set che contiene il prodotto incrociato di entrambi i parametri specificati.  
  
## <a name="remarks"></a>Note  
 Il  **\* (Crossjoin)** è funzionalmente equivalente all'operatore il [Crossjoin](../mdx/crossjoin-mdx.md) (funzione).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
