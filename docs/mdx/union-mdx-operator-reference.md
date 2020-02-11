---
title: + Unione (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd352b95853cc5fe52857a080b6ca2e515f5c013
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097348"
---
# <a name="union---mdx-operator-reference"></a>Riferimento all'operatore Union-MDX


  Esegue un'operazione sui set che restituisce l'unione di due set, rimuovendo i membri duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>Parametri  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="return-value"></a>Valore restituito  
 Set che include i membri di entrambi i set specificati.  
  
## <a name="remarks"></a>Osservazioni  
 L'operatore **+ (Union)** equivale dal punto di vista funzionale alla funzione di [unione &#40;MDX&#41;](../mdx/union-mdx.md) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
