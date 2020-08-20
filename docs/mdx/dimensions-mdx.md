---
description: Dimensions (MDX)
title: Dimensioni (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c98167516f9e01525ecd351389c885c48626636e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491418"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  Restituisce la gerarchia specificata da un'espressione numerica o stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Number*  
 Espressione numerica valida che specifica il numero di una gerarchia.  
  
 *Hierarchy_Name*  
 Espressione stringa valida che specifica il nome di una gerarchia.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificato un numero di gerarchia, la funzione **Dimensions** restituisce una gerarchia la cui posizione in base zero all'interno del cubo è specificata come numero di gerarchia.  
  
 Se viene specificato un nome di gerarchia, la funzione **Dimensions** restituisce la gerarchia specificata. In genere, questa versione di stringa della funzione **Dimensions** viene utilizzata con funzioni definite dall'utente.  
  
> [!NOTE]  
>  La dimensione **measures** è sempre rappresentata da `Dimensions(0)` .  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene utilizzata la funzione **Dimensions** per restituire il nome, il numero di livelli e il numero di membri di una gerarchia specificata, utilizzando un'espressione numerica e un'espressione stringa.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
