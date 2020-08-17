---
description: Unione (MDX)
title: Union (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b0b4240d6c646761c5d962e4b9fa1ca54e0dcc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341207"
---
# <a name="union--mdx"></a>Unione (MDX)


  Restituisce un set generato dall'unione di due set, mantenendo facoltativamente i membri duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>Argomenti  
 *Imposta espressione 1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Imposta espressione 2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione restituisce l'Unione di due o più set specificati. Con la sintassi standard e con la sintassi alternativa 1, i duplicati vengono eliminati per impostazione predefinita. Con la sintassi standard, l'utilizzo del flag **All** mantiene i duplicati nel set Unito in join. I duplicati vengono eliminati dalla parte finale del set. Con la sintassi alternativa 2, i duplicati vengono sempre mantenuti.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato il comportamento della funzione **Union** utilizzando ogni sintassi.  
  
### <a name="standard-syntax-duplicates-eliminated"></a>Sintassi standard, con eliminazione dei duplicati  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>Sintassi standard, con mantenimento dei duplicati  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>Sintassi alternativa 1, con eliminazione dei duplicati  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>Sintassi alternativa 2, con mantenimento dei duplicati  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [+ &#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
