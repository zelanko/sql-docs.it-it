---
title: Predict (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 165d03b886ad8e9beeb09bf5a835c879cc23a2a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055579"
---
# <a name="predict-mdx"></a>Predict (MDX)


    
> [!CAUTION]  
>  Questa funzione è in corso di rimozione a causa di inconsistenze interne.  
>   
>  Per una soluzione alternativa che utilizza un'espressione DMX, rivedere la sezione di esempio.  
  
 Restituisce il valore di un'espressione numerica valutata su un modello di data mining.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Mining_Model_Name*  
 Espressione stringa valida che rappresenta il nome di un modello di data mining.  
  
 *String_Expression*  
 Espressione stringa valida che restituisce un'espressione DMX valida per il modello di data mining specificato.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Predict** valuta l'espressione stringa specificata nel contesto del modello di data mining specificato.  
  
 La sintassi e le funzioni di data mining sono documentate nella specifica DMX (Data Mining Expressions).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono stimati il nome del cluster e la relativa distanza da un particolare cliente tramite il modello di data mining Customer Clusters:  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
