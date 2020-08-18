---
description: This (MDX)
title: This (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e00435741516fd1ed1942506084c26192b6d47da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413097"
---
# <a name="this-mdx"></a>This (MDX)


  Restituisce il sottocubo corrente da utilizzare con le assegnazioni nello script di calcolo MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Osservazioni  
 **Questa** funzione può essere utilizzata al posto di qualsiasi espressione di sottocubo per fornire il sottocubo corrente nell'ambito corrente all'interno dello script di calcolo MDX. **Questa** funzione deve essere utilizzata sul lato sinistro di un'assegnazione.  
  
## <a name="examples"></a>Esempi  
 Nel frammento di Script MDX seguente viene illustrato come utilizzare la parola chiave This con istruzioni SCOPE per fare assegnazioni ai sottocubi:  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Calcoli](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
  
