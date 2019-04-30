---
title: Estrarre (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3c58799cc3e95efd7d49b3aff0bf31a1fce22b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155217"
---
# <a name="extract-mdx"></a>Extract (MDX)


  Restituisce un set di tuple dagli elementi della gerarchia estratti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Hierarchy_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Hierarchy_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
## <a name="remarks"></a>Note  
 Il **estrarre** funzione restituisce un set costituito da tuple dagli elementi della gerarchia estratti. Per ogni tupla nel set specificato, i membri delle gerarchie specificate vengono estratti in nuove tuple nel set dei risultati. Questa funzione rimuove sempre le tuple duplicate.  
  
 Il **estrarre** funzione esegue l'operazione opposta rispetto il [Crossjoin](../mdx/crossjoin-mdx.md) (funzione).  
  
## <a name="examples"></a>Esempi  
 La query seguente viene illustrato come utilizzare il **estrarre** in un set di tuple restituito dalla funzione il **NonEmpty** funzione:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
