---
title: Utilizzo dimensioni, gerarchie e funzioni di livello | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097181"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Utilizzo di funzioni per dimensioni, gerarchie e livelli


  Le funzioni per dimensioni, gerarchie e livelli consentono di attraversare le strutture multidimensionali utilizzate Analysis Services. Tali funzioni vengono in genere utilizzate insieme ad altre funzioni, per ottenere informazioni sui membri di una dimensione, di una gerarchia o di un livello.  
  
 Nell'esempio seguente viene illustrato come utilizzare il **. Dimensione**, **. Gerarchia**, e **. Livello** funzioni:  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensione &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [Le funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Gerarchia di &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Livello &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
