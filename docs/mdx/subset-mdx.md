---
description: Subset (MDX)
title: Subset (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386727"
---
# <a name="subset-mdx"></a>Subset (MDX)


  Restituisce un subset di tuple dal set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Inizia*  
 Espressione numerica valida che specifica la posizione della prima tupla da restituire.  
  
 *Numero*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
## <a name="remarks"></a>Osservazioni  
 Dal set specificato, la funzione **subset** restituisce un subset che contiene il numero specificato di tuple, a partire dalla posizione iniziale specificata. La posizione iniziale è definita secondo un indice in base zero, ovvero zero (0) corrisponde alla prima tupla nel set specificato, 1 corrisponde alla seconda e così via.  
  
 Se *count* non è specificato, la funzione restituisce tutte le tuple dall' *inizio* alla fine del set.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la misura Reseller Sales per le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base a Reseller Gross Profit. La funzione **subset** viene utilizzata per restituire solo i primi cinque set nel risultato dopo che il risultato viene ordinato utilizzando la funzione **Order** .  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
