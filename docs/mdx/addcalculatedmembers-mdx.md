---
description: AddCalculatedMembers (MDX)
title: AddCalculatedMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 81e048ef534d12f282315562713e40d08512b121
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461702"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)


  Restituisce un set generato mediante l'aggiunta di membri calcolati a un set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 Per impostazione predefinita, durante la risoluzione delle funzioni sui set MDX esclude i membri calcolati. La funzione **AddCalculatedMembers** esamina l'espressione set specificata in *set_expression* e include i membri calcolati che sono elementi di pari livello dei membri contenuti nell'ambito di tale espressione set.  
  
> [!NOTE]  
>  Questa funzione può essere utilizzata solo con espressioni set unidimensionali.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questa funzione.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 Nell'esempio seguente viene restituito il `Measures.[Unit Price]` membro, oltre a tutti i membri calcolati nella dimensione **measures** , dal cubo **Adventure Works** .  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
