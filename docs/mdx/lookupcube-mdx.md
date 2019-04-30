---
title: LookupCube (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8f8338a542bf9e15816205930704c45a536a5629
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208512"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  Restituisce il valore di un'espressione MDX (Multidimensional Expression) valutata su un altro cubo specificato nello stesso database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome di un cubo.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *String_Expression*  
 Espressione stringa valida che in genere è un'espressione MDX (Multidimensional Expression) valida di coordinate di celle che restituisce una stringa.  
  
## <a name="remarks"></a>Note  
 Se viene specificata un'espressione numerica, la **LookupCube** funzione valuta l'espressione numerica specificata nel cubo specificato e restituisce il valore numerico risulta.  
  
 Se viene specificata un'espressione stringa, il **LookupCube** funzione valuta l'espressione stringa specificata nel cubo specificato e restituisce il valore di stringa risultante.  
  
 Il **LookupCube** funzione funziona su cubi dello stesso database in quanto il cubo di origine in cui la query MDX che contiene il **LookupCube** funzione è in esecuzione.  
  
> [!IMPORTANT]  
>  Poiché il contesto della query corrente non viene trasferito al cubo sul quale viene eseguita la query, tutti i membri correnti necessari devono essere specificati nell'espressione numerica o stringa.  
  
 Qualsiasi calcolo eseguito utilizzando il **LookupCube** funzione è probabile che peggioramento delle prestazioni. Anziché utilizzare questa funzione, riprogettare la soluzione in modo che tutti i dati necessari siano presenti in un cubo.  
  
## <a name="examples"></a>Esempi  
 Nella query seguente viene illustrato l'utilizzo di LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
