---
title: Dimensioni (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 84d5ab0caa22c6f35f3e7b790dbfb3348df8ceb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999971"
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
  
## <a name="remarks"></a>Note  
 Se viene specificato un numero di gerarchia, il **dimensioni** funzione restituisce una gerarchia la cui posizione in base zero all'interno del cubo è un numero di gerarchia specificato.  
  
 Se viene specificato un nome di gerarchia, il **dimensioni** funzione restituisce la gerarchia specificata. In genere, si utilizza questa versione di stringa di **dimensioni** funzione con funzioni definite dall'utente.  
  
> [!NOTE]  
>  Il **misure** dimensione è sempre rappresentata dallo `Dimensions(0)`.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti usano il **dimensioni** funzione per restituire il nome, numero di livelli e conteggio dei membri di una gerarchia specificata, utilizzando un'espressione numerica sia un'espressione stringa.  
  
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
  
  
