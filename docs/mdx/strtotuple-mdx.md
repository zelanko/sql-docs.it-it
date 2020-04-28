---
title: StrToTuple (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 232d1e94892165430867ec5217f8c87ccd625b48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036709"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  Restituisce la tupla specificata da una stringa in formato MDX (Multidimensional Expression).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Specification*  
 Espressione stringa valida che specifica, in modo diretto o indiretto, una tupla.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **StrToTuple** restituisce il set specificato. La funzione **StrToTuple** viene in genere utilizzata con funzioni definite dall'utente per la restituzione di una specifica di tupla da una funzione esterna a un'istruzione MDX.  
  
-   Quando viene utilizzato il flag CONSTRAINED, la tupla specificata deve contenere nomi di membri completi o non qualificati. Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se viene specificata una stringa non direttamente risolvibile in nomi di membri completi o non qualificati, viene visualizzato l'errore seguente: "Le restrizioni imposte dal flag CONSTRAINED nella funzione STRTOTUPLE sono state violate".  
  
-   Quando non viene utilizzato il flag CONSTRAINED, la tupla specificata può essere risolta in un'espressione MDX valida che restituisce una tupla.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente la funzione viene utilizzata per restituire la misura Reseller Sales Amount relativa al membro Bayern per l'anno di calendario 2004. La specifica della tupla fornita contiene un'espressione di tupla MDX valida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente la funzione viene utilizzata per restituire la misura Reseller Sales Amount relativa al membro Bayern per l'anno di calendario 2004. La specifica della tupla fornita contiene nomi di membri qualificati, come richiesto dal flag CONSTRAINED.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente la funzione viene utilizzata per restituire la misura Reseller Sales Amount relativa al membro Bayern per l'anno di calendario 2004. La specifica della tupla fornita contiene un'espressione di tupla MDX valida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito un errore a causa del flag CONSTRAINED. Nonostante la tupla specificata contenga un'espressione di tupla MDX valida, il flag CONSTRAINED richiede in essa nomi di membri completi o non qualificati.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
