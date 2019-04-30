---
title: UnknownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84eda6f42b674ebde8793605816f98e82af350d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065044"
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)


  Restituisce il membro sconosciuto associato a un livello o a un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
## <a name="remarks"></a>Note  
 Analysis Services consente di creare un membro sconosciuto per associare i dati della tabella dei fatti a una gerarchia quando la gerarchia non è noto. Il membro sconosciuto può trovarsi a uno dei livelli seguenti:  
  
-   Al livello principale per le gerarchie di attributi non aggregate.  
  
-   Al primo livello sotto il **tutti** livello per le gerarchie naturali.  
  
-   A qualsiasi livello per le gerarchie non naturali.  
  
 Se viene specificata un'espressione di membro, il **UnknownMember** funzione restituisce il membro sconosciuto figlio del membro specificato. Se il membro specificato non esiste, la funzione restituirà Null.  
  
 Se viene specificata un'espressione di gerarchia, il **UnknownMember** funzione restituisce il membro sconosciuto al livello superiore, se presente.  
  
 Se il membro sconosciuto non esiste sul livello o membro, il **UnknownMember** funzione crea un membro null.  
  
> [!NOTE]  
>  Se il membro sconosciuto non esiste sulla gerarchia o sul membro, verrà generato un errore.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il membro sconosciuto per il membro All Products nella gerarchia dell'attributo Product per tutti i membri della dimensione Measures.  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il membro sconosciuto per la gerarchia Product Categories per tutti i membri della dimensione Measures.  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
