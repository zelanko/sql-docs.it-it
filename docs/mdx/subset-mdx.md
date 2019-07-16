---
title: Subset (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b1f9a79c0e0ba6d578b82d7b1d072f3543888a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036697"
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
  
 *Start*  
 Espressione numerica valida che specifica la posizione della prima tupla da restituire.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
## <a name="remarks"></a>Note  
 Dal set specificato, il **Subset** funzione restituisce un subset che contiene il numero specificato di tuple, iniziando in corrispondenza della posizione di inizio specificata. La posizione iniziale è definita secondo un indice in base zero, ovvero zero (0) corrisponde alla prima tupla nel set specificato, 1 corrisponde alla seconda e così via.  
  
 Se *conteggio* non è specificato, la funzione restituisce tutte le tuple da *avviare* alla fine del set.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la misura Reseller Sales per le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base a Reseller Gross Profit. Il **sottoinsieme** funzione viene utilizzata per restituire solo i primi cinque set del risultato dopo l'ordinamento del risultato utilizzando il **ordine** (funzione).  
  
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
  
  
