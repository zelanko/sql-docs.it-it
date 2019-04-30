---
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff7ffb1b57c8af38e1b2eeebc64f2a3e753fc5b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278490"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  Restituisce una stringa in formato multidimensionale espressioni MDX che corrisponde a un membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 Questa funzione restituisce una stringa che contiene l'elemento uniquename di un membro In genere utilizzato per passare l'elemento uniquename di un membro a una funzione esterna.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente restituisce la stringa [Geography]. [Geography]. [Paese]. & [United States]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
