---
title: Elemento padre (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9449c81e9f8e8de0c21d96062337e91b2f56398d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037190"
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
  
## <a name="remarks"></a>Note  
 Il **padre** funzione restituisce il membro padre del membro specificato.  
  
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
  
  
