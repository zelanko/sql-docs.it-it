---
title: Livello (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b419cbb05aa616f163f5878bda83c9d68203575d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905665"
---
# <a name="level-mdx"></a>Level (MDX)


  Restituisce il livello di un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata la funzione **Level** per restituire tutti i mesi nel cubo Adventure Works.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene utilizzata la funzione **Level** per restituire il nome del livello per la bike stand per tutti gli scopi nella gerarchia dell'attributo Model Name del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
