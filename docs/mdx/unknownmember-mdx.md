---
description: UnknownMember (MDX)
title: UnknownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0489556836b943ba91d4e17b3a164aeca0c648d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341147"
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
  
## <a name="remarks"></a>Osservazioni  
 Analysis Services crea un membro sconosciuto per associare i dati della tabella dei fatti a una gerarchia quando la gerarchia non è nota. Il membro sconosciuto può trovarsi a uno dei livelli seguenti:  
  
-   Al livello principale per le gerarchie di attributi non aggregate.  
  
-   Al primo livello sotto il livello **All** per le gerarchie naturali.  
  
-   A qualsiasi livello per le gerarchie non naturali.  
  
 Se viene specificata un'espressione di membro, la funzione **UnknownMember** restituisce il membro sconosciuto figlio del membro specificato. Se il membro specificato non esiste, la funzione restituirà Null.  
  
 Se viene specificata un'espressione di gerarchia, la funzione **UnknownMember** restituisce il membro sconosciuto al primo livello se ne esiste uno.  
  
 Se il membro sconosciuto non esiste nel livello o nel membro, la funzione **UnknownMember** crea un membro null.  
  
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
  
  
