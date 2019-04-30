---
title: Intersect (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b24049cb81982075fa9234c6fa792db273d404db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224868"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  Restituisce l'intersezione di due set di input, mantenendo facoltativamente i duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Note  
 Il **Intersect** funzione restituisce l'intersezione di due set. Per impostazione predefinita la funzione rimuove i duplicati da entrambi i set prima di eseguire l'intersezione. I due set specificati devono disporre della stessa dimensionalità.  
  
 L'opzione facoltativa **tutti** flag consente di mantenere i duplicati. Se **tutti i** è specificato, il **Intersect** interseca gli elementi come di consueto (funzione) e ogni elemento duplicato del primo set che contiene un elemento duplicato nel secondo set. I due set specificati devono disporre della stessa dimensionalità.  
  
## <a name="example"></a>Esempio  
 Per la seguente query vengono restituiti gli anni 2003 e 2004, ovvero i due membri visualizzati in entrambi i set specificati:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La query seguente non viene eseguita correttamente perché i due set specificati contengono membri da gerarchie diverse:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
