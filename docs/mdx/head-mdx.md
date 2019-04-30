---
title: Head (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 05cfcb3c23a0369f010b8440d4a27e94ffacdb21
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125567"
---
# <a name="head-mdx"></a>Head (MDX)


  Restituisce il primo numero specificato di elementi in un set, mantenendo i duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
## <a name="remarks"></a>Note  
 Il **Head** funzione restituisce il numero di tuple specificato dall'inizio del set specificato. L'ordine degli elementi viene mantenuto. Il valore predefinito di Count è 1. Se il numero specificato di tuple è minore di 1, il **Head** funzione restituisce un set vuoto. Se il numero di tuple specificato supera il numero di tuple nel set, la funzione restituisce il set originale.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituite le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base al profitto lordo del rivenditore. Il **Head** funzione viene utilizzata per restituire solo i primi 5 set del risultato dopo l'ordinamento del risultato utilizzando il **ordine** (funzione).  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Item &#40;Tuple&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Elemento &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Rank &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
