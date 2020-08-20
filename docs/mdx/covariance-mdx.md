---
description: Covariance (MDX)
title: Covarianza (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32471a48f0a669f7b72b5946f07403d6851dfb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500534"
---
# <a name="covariance-mdx"></a>Covariance (MDX)


  Restituisce la covarianza della popolazione delle coppie di valori x-y valutata su un set, utilizzando la formula della popolazione distorta (dividendo per il numero di coppie x-y).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Covariance** valuta il set specificato rispetto alla prima espressione numerica, per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla seconda espressione numerica, se specificata, per ottenere il set di valori per l'asse x. Se la seconda espressione numerica non è specificata, la funzione utilizza il contesto corrente delle celle nel set specificato come valori per l'asse x.  
  
 La funzione **Covariance** usa la formula della popolazione distorta. Si differenzia dalla funzione [Covariant](../mdx/covariancen-mdx.md) che usa la formula della popolazione non distorta (dividendo il numero di coppie x-y, quindi sottraendo 1).  
  
> [!NOTE]  
>  La funzione **Covariance** ignora le celle vuote o le celle che contengono testo o valori logici vengono ignorate. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare la funzione Covariance:  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
