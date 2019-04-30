---
title: Root (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c2301f44cbdac4505bef95d590ce206c8b6b509
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150235"
---
# <a name="root-mdx"></a>Radice (MDX)


  Restituisce una tupla costituita la **tutti** i membri di ogni gerarchia dell'attributo all'interno dell'ambito corrente in un cubo, dimensione o tupla. Per altre informazioni sull'ambito, vedere [istruzione SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Se una gerarchia dell'attributo non dispone di un **tutti** membro, tupla conterrà il membro predefinito per tale gerarchia.  
  
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
  
## <a name="remarks"></a>Note  
 Se viene specificata né un nome di dimensione né un'espressione di tupla, il **radice** funzione restituisce una tupla contenente il **tutti** membro (o il membro predefinito se la **tutti i** membro inesistente) di ogni gerarchia dell'attributo nel cubo. L'ordine dei membri nella tupla dipende dalla sequenza in cui sono definite le gerarchie dell'attributo nel cubo.  
  
 Se viene specificato un nome di dimensione, il **radice** funzione restituisce una tupla contenente il **tutti** membro (o il membro predefinito se la **tutti i** membro non esiste) da ogni gerarchia dell'attributo nella dimensione specificata in base al contesto del membro corrente. L'ordine dei membri nella tupla dipende dalla sequenza in cui sono definite le gerarchie dell'attributo nella dimensione.  
  
> [!NOTE]  
>  Se viene specificato un nome di gerarchia, il **tupla** funzione selezionerà il nome della dimensione dal nome della gerarchia specificato.  
  
 Se viene specificata un'espressione di tupla, la **radice** funzione restituisce una tupla che contiene l'intersezione della tupla specificata e il **tutte** i membri di tutti gli altri attributi di dimensione non esplicitamente incluso nella tupla specificata.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce la tupla contenente il **tutti i** membro (o il valore predefinito se il **tutte** membro non esiste) di ogni gerarchia nel cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 L'esempio seguente restituisce la tupla contenente il **tutti i** membro (o il valore predefinito se il **tutte** membro non esiste) di ogni gerarchia nella dimensione Date del cubo Adventure Works e il valore di il membro specificato della dimensione Measures che si interseca con tali membri predefiniti.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 L'esempio seguente restituisce la tupla contenente membro della tupla specificato (1 luglio 2001, insieme al **tutti i** membro (o il valore predefinito se il **tutti i** membro non esiste) di ogni gerarchia non specificati in il cubo di Adventure Works di dimensione di data e il valore per il membro specificato della dimensione Measures che si interseca con tali membri.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
