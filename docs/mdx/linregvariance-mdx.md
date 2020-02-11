---
title: LinRegVariance (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b45328614bbefe730c815f528e82f220ad0093e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905509"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  Calcola la regressione lineare di un set e restituisce la varianza associata alla retta di regressione y = ax + b.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Osservazioni  
 La regressione lineare, che utilizza il metodo dei minimi quadrati, calcola l'equazione di una retta di regressione, ovvero la retta di migliore approssimazione per una serie di punti. La linea di regressione presenta l'equazione seguente, dove a è la pendenza e b è l'intercetta:  
  
 y = ax+b  
  
 La funzione **LinRegVariance** valuta la prima espressione numerica specificata per ottenere i valori per l'asse y. La funzione valuta quindi la seconda espressione numerica specificata, se specificata, per ottenere i valori per l'asse x. Se la seconda espressione numerica non è specificata, la funzione utilizza il contesto corrente delle celle nel set specificato come valori per l'asse x. L'omissione dell'argomento dell'asse x è frequente con le dimensioni temporali.  
  
 Una volta ottenuto il set di punti, la funzione **LinRegVariance** restituisce la varianza statistica che descrive l'adattamento dell'equazione lineare ai punti.  
  
> [!NOTE]  
>  La funzione **LinRegVariance** ignora le celle vuote o le celle che contengono testo o valori logici. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la varianza statistica che descrive in quale misura l'equazione lineare si adatta ai punti per le misure relative a vendite unitarie e vendite dei negozi.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
