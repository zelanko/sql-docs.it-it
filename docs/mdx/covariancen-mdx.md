---
description: CovarianceN (MDX)
title: Covarianza (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e9475b7402a5317c18ad0ac5d4065ca2f4fdce26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500524"
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)


  Restituisce la covarianza del campione delle coppie di valori x-y valutata su un set, utilizzando la formula della popolazione non distorta (dividendo per il numero di coppie x-y).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Covariant** valuta il set specificato rispetto alla prima espressione numerica, per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla seconda espressione numerica, se specificata, per ottenere il set di valori per l'asse x. Se la seconda espressione numerica viene omessa, come valori per l'asse X la funzione utilizza il contesto corrente delle celle contenute nel set specificato.  
  
 La funzione **Covariant** usa la formula della popolazione non distorta. Si differenzia dalla funzione [Covariance](../mdx/covariance-mdx.md) che usa la formula della popolazione distorta (dividendo per il numero di coppie x-y).  
  
> [!NOTE]  
>  La funzione **Covariant** ignora le celle vuote o le celle che contengono testo o valori logici. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
