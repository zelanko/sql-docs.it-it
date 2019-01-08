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
manager: kfile
ms.openlocfilehash: 054786440afaf2b7ab458b4704bd5f8e2e26c135
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524531"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  Restituisce la tupla specificata da una stringa di formato Multidimensional.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Specification*  
 Espressione stringa valida che specifica, in modo diretto o indiretto, una tupla.  
  
## <a name="remarks"></a>Note  
 Il **StrToTuple** funzione restituisce il set specificato. Il **StrToTuple** funzione viene in genere utilizzata con funzioni definite dall'utente per la restituzione di una tupla specificata da una funzione esterna a un'istruzione MDX.  
  
-   Quando viene utilizzato il flag CONSTRAINED, la tupla specificata deve contenere nomi di membri completi o non qualificati. Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se viene fornita una stringa che non i nomi dei membri direttamente risolvibile in o non qualificati, viene visualizzato l'errore seguente: "Le restrizioni imposte dal CONSTRAINED flag nella funzione STRTOTUPLE sono state violate."  
  
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
  
  
