---
description: AllMembers (MDX)
title: AllMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba70d4ad8b301cbd8af2fd76ce058f2dab2e4a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461673"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


  Valuta un'espressione di gerarchia o di livello e restituisce un set che contiene tutti i membri della gerarchia o del livello specificato, inclusi tutti i membri calcolati in tale gerarchia o livello.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **AllMembers** restituisce un set contenente tutti i membri, inclusi i membri calcolati, nella gerarchia o nel livello specificato. La funzione **AllMembers** restituisce i membri calcolati anche se la gerarchia o il livello specificato non contiene membri visibili.  
  
> [!IMPORTANT]  
>  Quando una dimensione contiene una sola gerarchia visibile, è possibile fare riferimento alla gerarchia con il nome della dimensione o della gerarchia poiché in questo caso il nome della dimensione viene risolto in base all'unica gerarchia visibile che contiene. `Measures.AllMembers` è ad esempio un'espressione MDX valida perché esegue la risoluzione nell'unica gerarchia nella dimensione Measures.  
  
> [!NOTE]  
>  La funzione **AllMembers** è semanticamente simile alla funzione [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i membri nella `Date].[Calendar Year]` gerarchia [attribute sull'asse delle colonne, inclusi i membri calcolati e il set di tutti gli elementi figlio della `[Product].[Model Name]` gerarchia dell'attributo sull'asse delle righe dal cubo **Adventure Works** .  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 Nell'esempio seguente vengono restituiti tutti i membri della dimensione **measures** sull'asse delle colonne, inclusi tutti i membri calcolati e il set di tutti gli elementi figlio della `[Product].[Model Name]` gerarchia dell'attributo sull'asse delle righe dal cubo **Adventure Works** .  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [AddCalculatedMembers &#40;&#41;MDX ](../mdx/addcalculatedmembers-mdx.md)   
 [Elementi figlio &#40;&#41;MDX ](../mdx/children-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
