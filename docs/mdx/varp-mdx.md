---
description: VarP (MDX)
title: VarP (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c850ba60ac9900228c6adaa03aa97b46b1abddf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429723"
---
# <a name="varp-mdx"></a>VarP (MDX)


  Restituisce la varianza della popolazione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione distorta (dividendo per *n*-1).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **VarP** restituisce la varianza distorta di un'espressione numerica specificata, valutata su un set specificato.  
  
 La funzione **VarP** usa la formula della popolazione distorta, mentre la funzione [var](../mdx/var-mdx.md) usa la formula della popolazione non distorta.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
