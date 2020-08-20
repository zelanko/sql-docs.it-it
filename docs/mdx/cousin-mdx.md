---
description: Cousin (MDX)
title: Cugino (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eff78bb06f935311f178d2e39be11bec3e959776
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500544"
---
# <a name="cousin-mdx"></a>Cousin (MDX)


  Restituisce il membro figlio con la stessa posizione relativa del membro figlio specificato rispetto a un membro padre.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Ancestor_Member_Expression*  
 Espressione di membro MDX (Multidimensional Expression) valida che restituisce un membro predecessore.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione agisce sull'ordine e sulla posizione dei membri all'interno dei livelli. Se sono presenti due gerarchie la prima delle quali dispone di quattro livelli e la seconda di cinque, il membro cousin del terzo livello della prima gerarchia è costituito dal terzo livello della seconda gerarchia.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperato il membro cousin del quarto trimestre dell'anno fiscale 2002, in base al relativo predecessore a livello di anno nell'anno fiscale 2003. Il membro cousin recuperato è costituito dal quarto trimestre dell'anno fiscale 2003.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene recuperato il membro cousin del mese di luglio dell'anno fiscale 2002, in base al relativo predecessore a livello di trimestre nel secondo trimestre dell'anno fiscale 2004. Il membro cousin recuperato è costituito dal mese di ottobre 2003.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
