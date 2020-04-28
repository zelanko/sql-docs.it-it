---
title: Var (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 96bb307607792a3846ee6566027457a05ce3b905
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037932"
---
# <a name="var-mdx"></a>Var (MDX)


  Restituisce la varianza di esempio di un'espressione numerica valutata su un set, utilizzando la formula della popolazione non distorta (dividendo per *n*).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **var** restituisce la varianza non distorta di un'espressione numerica specificata valutata su un set specificato.  
  
 La funzione **var** utilizza la formula della popolazione non distorta, mentre la funzione [VarP](../mdx/varp-mdx.md) utilizza la formula della popolazione distorta.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
