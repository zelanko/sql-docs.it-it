---
title: DrillupLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e00851557b502bda3a98763eff4bac9c3abdccff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690772"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)


  Esegue il drill-up dei membri di un set situati al livello immediatamente inferiore al livello specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
## <a name="remarks"></a>Note  
 Il **DrillupLevel** funzione restituisce un set di membri organizzato gerarchicamente in base i membri inclusi nel set specificato. L'ordine dei membri nel set specificato viene mantenuto.  
  
 Se viene specificata un'espressione di livello, il **DrillupLevel** funzione costruisce il set recuperando solo i membri che sono di sopra del livello specificato. Se si specifica un'espressione di livello ma nessun membro del livello specificato è rappresentato nel set specificato, viene restituito tale set.  
  
 Se non si specifica un'espressione di livello, la funzione genera il set recuperando solo i membri del livello superiore rispetto al livello inferiore della prima dimensione indicata nel set specificato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il set di membri del primo set che si trovano al di sopra del livello Subcategory.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
