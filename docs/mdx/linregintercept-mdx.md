---
title: LinRegIntercept (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a0c153182e1405ebedd26cc875c10068e280b654
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136413"
---
# <a name="linregintercept-mdx"></a>LinRegIntercept (MDX)


  Calcola la regressione lineare di un set e restituisce il valore dell'intersezione-x nella retta di regressione y = ax + b.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Note  
 La regressione lineare, che utilizza il metodo dei minimi quadrati, calcola l'equazione di una retta di regressione, ovvero la retta di migliore approssimazione per una serie di punti. Retta di regressione contiene l'equazione seguente, in cui una è l'inclinazione e b è l'intercetta:  
  
 y = ax+b  
  
 Il **LinRegIntercept** funzione valuta il set specificato in base alla prima espressione numerica per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla seconda espressione numerica, se specificata, per ottenere i valori per l'asse X. Se la seconda espressione numerica viene omessa, come valori per l'asse X la funzione utilizza il contesto corrente delle celle contenute nel set specificato. L'omissione dell'argomento dell'asse x è frequente con le dimensioni temporali.  
  
 Dopo aver ottenuto il set di punti, il **LinRegIntercept** funzione restituisce l'intercetta della retta di regressione (b nell'equazione riportata sopra).  
  
> [!NOTE]  
>  Il **LinRegIntercept** funzione ignora le celle vuote o che contengono testo o valori logici. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita l'intercetta della linea di regressione relativa alle misure Unit Sales e Store Sales.  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
