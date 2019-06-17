---
title: This (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77db403ee016283a565a6bc86d2f6857de0eff45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259026"
---
# <a name="this-mdx"></a>This (MDX)


  Restituisce il sottocubo corrente da utilizzare con le assegnazioni nello script di calcolo MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Note  
 Il **ciò** funzione può essere utilizzata al posto di un'espressione di sottocubo per ottenere il sottocubo corrente all'interno dell'ambito corrente all'interno di script di calcolo MDX. Il **ciò** necessario utilizzare la funzione sul lato sinistro di un'assegnazione.  
  
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
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Calcoli](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
