---
title: LinRegPoint (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3719071beca4dbd8cc991befbb7b2b74f8982c89
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905571"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  Calcola la regressione lineare di un set e restituisce il valore dell' *intersezione y* nella retta di regressione y = ax + b per un determinato valore di x.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Slice_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse di sezionamento.  
  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Osservazioni  
 La regressione lineare, che utilizza il metodo dei minimi quadrati, calcola l'equazione di una retta di regressione, ovvero la retta di migliore approssimazione per una serie di punti. La linea di regressione presenta l'equazione seguente, dove a è la pendenza e b è l'intercetta:  
  
 y = ax+b  
  
 La funzione **LinRegPoint** valuta il set specificato rispetto alla seconda espressione numerica per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla terza espressione numerica, se specificata, per ottenere i valori per l'asse x. Se la terza espressione numerica viene omessa, come valori per l'asse x la funzione utilizza il contesto corrente delle celle contenute nel set specificato. L'omissione dell'argomento dell'asse x è frequente con le dimensioni temporali.  
  
 Dopo il calcolo della regressione lineare, viene calcolato e quindi restituito il valore dell'equazione per la prima espressione numerica.  
  
> [!NOTE]  
>  La funzione **LinRegPoint** ignora le celle vuote o le celle che contengono testo. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore stimato di Unit Sales negli ultimi dieci periodi in base alla relazione statistica tra Unit Sales e Store Sales.  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
