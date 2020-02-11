---
title: LinRegR2 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e38df1a24b76ee40aae3a5ab3c28dd9bca2b310
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905524"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  Calcola la regressione lineare di un set e restituisce il coefficiente di determinazione, R<sup>2</sup>.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 La funzione **LinRegR2** valuta l'oggetto di cui è stato specificato il valore per il primo espressione numerico per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla seconda espressione numerica, se specificata, per ottenere i valori per l'asse X. Se la seconda espressione numerica non è specificata, la funzione utilizza il contesto corrente delle celle nel set specificato come valori per l'asse x. La mancata specifica di x-axisargument viene spesso utilizzata con la dimensione temporale.  
  
 Dopo avere ottenuto il set di punti, la funzione **LinRegR2** restituisce l'oggetto statistico R<sup>2</sup> che descrive l'adattamento dell'equazione lineare ai punti.  
  
> [!NOTE]  
>  La funzione **LinRegR2** ignora le celle vuote o le celle che contengono testo o valori logici. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il risultato statistico R<sup>2</sup> che descrive il grado di adattamento dell'equazione di regressione lineare ai punti per le misure Sales unit e Store Sales.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
