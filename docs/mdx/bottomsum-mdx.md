---
title: BottomSum (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e49fc5a7ffd4c0adff38628a143ded695785e29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016884"
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)


  Dispone un set specificato in ordine crescente e restituisce un set di tuple con i valori più bassi la cui somma è uguale o inferiore a un valore specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Valore*  
 Espressione numerica valida che specifica il valore in base a cui ogni tupla viene valutata.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **BottomSum** calcola la somma di una misura specificata valutata su un set specificato, ordinando il set in ordine crescente. La funzione restituisce quindi gli elementi con i valori più bassi il cui totale per l'espressione numerica specificata corrisponde almeno al valore specificato (somma). La funzione restituisce il subset più piccolo di un set il cui totale cumulativo corrisponde almeno al valore specificato. Gli elementi restituiti sono ordinati dal più piccolo al più grande.  
  
> [!IMPORTANT]  
>  La funzione **BottomSum** , come la funzione [TopSum](../mdx/topsum-mdx.md) , interrompe sempre la gerarchia.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito per la categoria Bike il set più piccolo di membri del livello City nella gerarchia Geography della dimensione Geography per l'anno fiscale 2003 il cui totale cumulativo, utilizzando la misura Reseller Sales Amount, corrisponde almeno alla somma di 50.000 (a partire dai membri di questo set con il numero di vendite più basso):  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
