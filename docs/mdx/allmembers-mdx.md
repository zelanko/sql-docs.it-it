---
title: AllMembers=2==restituisce (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92cde0acf07f62d0678da6dd96efa707dedc1a1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63066249"
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
  
## <a name="remarks"></a>Note  
 Il **AllMembers** funzione restituisce un set contenente tutti i membri, che include i membri calcolati, nella gerarchia specificata o del livello. Il **AllMembers** funzione restituisce i membri calcolati anche se il livello o la gerarchia specificata non contiene membri visibili.  
  
> [!IMPORTANT]  
>  Quando una dimensione contiene una sola gerarchia visibile, è possibile fare riferimento alla gerarchia con il nome della dimensione o della gerarchia poiché in questo caso il nome della dimensione viene risolto in base all'unica gerarchia visibile che contiene. `Measures.AllMembers` è ad esempio un'espressione MDX valida perché esegue la risoluzione nell'unica gerarchia nella dimensione Measures.  
  
> [!NOTE]  
>  Il **AllMembers** funzione è semanticamente simile al [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) (funzione).  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce tutti i membri nel [`Date].[Calendar Year]` gerarchia dell'attributo sull'asse delle colonne, inclusi i membri calcolati e il set di tutti gli elementi figlio del `[Product].[Model Name]` gerarchia sull'asse delle righe dell'attributo di **Adventure Works** cubo.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 L'esempio seguente restituisce tutti i membri il **misure** dimensione sull'asse delle colonne, inclusi tutti i membri calcolati e il set di tutti gli elementi figlio del `[Product].[Model Name]` gerarchia sull'asse delle righe dell'attributo dal **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Children &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
