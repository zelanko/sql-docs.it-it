---
description: Parent (MDX)
title: Elemento padre (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bbedef9142d87c1522df516884797a0a6dff0b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471713"
---
# <a name="parent-mdx"></a>Parent (MDX)


  Restituisce il membro padre di un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **padre** restituisce il membro padre del membro specificato.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene restituito il membro padre del membro July 1, 2001. Nel primo esempio viene specificato questo membro nel contesto della gerarchia dell'attributo Date e viene restituito il membro All Periods.  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente il membro July 1, 2001 viene specificato nel contesto della gerarchia Calendar.  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
