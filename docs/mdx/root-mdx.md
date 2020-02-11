---
title: Radice (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037045"
---
# <a name="root-mdx"></a>Radice (MDX)


  Restituisce una tupla costituita da **tutti** i membri di ogni gerarchia dell'attributo nell'ambito corrente in un cubo, una dimensione o una tupla. Per ulteriori informazioni sull'ambito, vedere [istruzione scope &#40;&#41;MDX ](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Se una gerarchia dell'attributo non dispone di un membro **totale** , la tupla contiene il membro predefinito per la gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Dimension_Name*  
 Espressione stringa valida che specifica il nome di una dimensione.  
  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
## <a name="remarks"></a>Osservazioni  
 Se non viene specificato né un nome di dimensione né un'espressione di tupla, la funzione **radice** restituisce una tupla contenente il membro **totale** (o il membro predefinito se il membro **totale** non esiste) da ogni gerarchia dell'attributo nel cubo. L'ordine dei membri nella tupla dipende dalla sequenza in cui sono definite le gerarchie dell'attributo nel cubo.  
  
 Se viene specificato un nome di dimensione, la funzione **radice** restituisce una tupla contenente il membro **totale** (o il membro predefinito se il membro **totale** non esiste) da ogni gerarchia dell'attributo nella dimensione specificata in base al contesto del membro corrente. L'ordine dei membri nella tupla dipende dalla sequenza in cui sono definite le gerarchie dell'attributo nella dimensione.  
  
> [!NOTE]  
>  Se viene specificato un nome di gerarchia, la funzione **tupla** selezionerà il nome della dimensione dal nome della gerarchia specificato.  
  
 Se viene specificata un'espressione di tupla, la funzione **radice** restituisce una tupla contenente l'intersezione della tupla specificata e **tutti** i membri di tutti gli altri attributi della dimensione non inclusi in modo esplicito nella tupla specificata.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la tupla contenente il membro **totale** (o l'impostazione predefinita se il membro **totale** non esiste) da ogni gerarchia del cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituita la tupla contenente il membro **totale** (o l'impostazione predefinita se il membro **totale** non esiste) da ogni gerarchia della dimensione Date del cubo Adventure Works e il valore del membro specificato della dimensione Measures che si interseca con questi membri predefiniti.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 Nell'esempio seguente viene restituita la tupla contenente il membro della tupla specificato (il 1 ° luglio 2001, insieme al membro **totale** (o l'impostazione predefinita se il membro **totale** non esiste) da ogni gerarchia non specificata nella dimensione Date Adventure Works Cube e il valore per il membro specificato della dimensione Measures che si interseca con questi membri.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
