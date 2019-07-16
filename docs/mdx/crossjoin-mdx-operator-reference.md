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
ms.openlocfilehash: 2f8377acec8f213c423de5d19d8859c8b3d93a06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047145"
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
  
  
