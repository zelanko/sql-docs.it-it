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
ms.openlocfilehash: ec18b600c369de872df5f6eadf06ef6c30c88efa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098507"
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
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificata un'espressione numerica, la funzione **LookupCube** valuta l'espressione numerica specificata nel cubo specificato e restituisce il valore numerico risultante.  
  
 Se viene specificata un'espressione stringa, la funzione **LookupCube** valuta l'espressione stringa specificata nel cubo specificato e restituisce il valore stringa risultante.  
  
 La funzione **LookupCube** funziona sui cubi nello stesso database del cubo di origine in cui è in esecuzione la query MDX che contiene la funzione **LookupCube** .  
  
> [!IMPORTANT]  
>  Poiché il contesto della query corrente non viene trasferito al cubo sul quale viene eseguita la query, tutti i membri correnti necessari devono essere specificati nell'espressione numerica o stringa.  
  
 È probabile che qualsiasi calcolo che utilizza la funzione **LookupCube** risenta di ridurre le prestazioni. Anziché utilizzare questa funzione, riprogettare la soluzione in modo che tutti i dati necessari siano presenti in un cubo.  
  
## <a name="examples"></a>Esempi  
 Nella query seguente viene illustrato l'utilizzo di LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
