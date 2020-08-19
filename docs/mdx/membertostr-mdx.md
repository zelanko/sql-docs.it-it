---
description: MemberToStr (MDX)
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6217120c7e6d5ee55670be3d902a9ea99333273f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483804"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  Restituisce una stringa in formato MDX (Multidimensional Expression) che corrisponde a un membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione restituisce una stringa che contiene l'elemento uniquename di un membro Viene in genere usato per passare l'oggetto UniqueName di un membro a una funzione esterna.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la stringa [Geography]. [Geography]. [Paese]. & [Stati Uniti]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
