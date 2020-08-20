---
description: Ancestors (MDX)
title: Predecessori (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d92f15f20c872fbe63db09a55356b5d1e35ff0d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461683"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  Funzione che restituisce il set di tutti i predecessori di un membro specificato al livello specificato oppure alla distanza specificata dal membro. Con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , il set restituito è sempre costituito da un singolo membro, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non supporta più elementi padre per un singolo membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Level syntax  
Ancestors(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestors(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Distanza*  
 Espressione numerica valida che specifica la distanza dal membro specificato.  
  
## <a name="remarks"></a>Osservazioni  
 Con la funzione **predecessori** , si fornisce la funzione con un'espressione di membro MDX e quindi si fornisce un'espressione MDX di un livello che è un predecessore di tale membro o un'espressione numerica che rappresenta il numero di livelli al di sopra di tale membro. Con queste informazioni, la funzione **predecessores** restituisce il set di membri (che sarà un set costituito da un membro) a tale livello.  
  
> [!NOTE]  
>  Per restituire un membro predecessore, anziché un set predecessore, utilizzare la funzione [predecessore](../mdx/ancestor-mdx.md) .  
  
 Se viene specificata un'espressione di livello, la funzione **predecessores** restituisce il set di tutti i predecessori del membro specificato al livello specificato. Se il membro specificato non è incluso nella stessa gerarchia del livello specificato, la funzione restituisce un errore.  
  
 Se viene specificata una distanza, la funzione **progenitori** restituisce il set di tutti i membri che corrispondono al numero di passaggi specificato nella gerarchia specificata dall'espressione del membro. Un membro può essere specificato come membro di una gerarchia dell'attributo, una gerarchia definita dall'utente o, in alcuni casi, una gerarchia padre-figlio. Con il numero 1 viene restituito il set di membri al livello padre, mentre con il numero 2 viene restituito il set di membri al livello dell'elemento padre del padre, se esistente. Il numero 0 restituisce il set contenente soltanto il membro stesso.  
  
> [!NOTE]  
>  Usare questa forma della funzione **predecessori** per i casi in cui il livello dell'elemento padre è sconosciuto o non può essere denominato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata la funzione **Predecessors** per restituire la misura Internet Sales Amount per un membro, il relativo padre e il relativo padre padre. Nell'esempio vengono utilizzate espressioni di livello per specificare i livelli da restituire. I livelli sono contenuti nella stessa gerarchia del membro specificato nell'espressione di membro.  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene utilizzata la funzione **Predecessors** per restituire la misura Internet Sales Amount per un membro, il relativo padre e il relativo padre padre. Nell'esempio vengono utilizzate espressioni numeriche per specificare i livelli restituiti. I livelli sono contenuti nella stessa gerarchia del membro specificato nell'espressione di membro.  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],2  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],1  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],0  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM  [Adventure Works]  
```  
  
 Nell'esempio seguente viene utilizzata la funzione **Predecessors** per restituire la misura Internet Sales Amount per l'elemento padre di un membro di una gerarchia dell'attributo. Nell'esempio viene utilizzata un'espressione numerica per specificare il livello restituito. Poiché il membro dell'espressione di membro è membro di una gerarchia dell'attributo, il relativo elemento padre è costituito dal livello [Totale].  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
