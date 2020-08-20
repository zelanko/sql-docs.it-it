---
description: TupleToStr (MDX)
title: TupleToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 69e81156b26d4becb05390c8684b433584793697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487624"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  Restituisce una stringa in formato MDX (Multidimensional Expression) che corrisponde a una tupla specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione viene utilizzata per trasferire una rappresentazione stringa di una tupla a una funzione esterna per l'analisi. La stringa restituita è racchiusa tra parentesi graffe {} e ogni membro, se più di uno è definito espressamente nella tupla, è separato da una virgola.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la stringa ([DATE]. [ Anno di calendario]. & [2001], [Geography]. [Geography]. [Paese]. & [Stati Uniti]):  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituita la stessa stringa dell'esempio precedente.  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
