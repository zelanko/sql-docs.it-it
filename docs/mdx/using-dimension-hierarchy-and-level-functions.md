---
title: Utilizzo di funzioni di dimensioni, gerarchie e livelli | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097181"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Utilizzo di funzioni per dimensioni, gerarchie e livelli


  Le funzioni per dimensioni, gerarchie e livelli consentono di attraversare le strutture multidimensionali utilizzate Analysis Services. Tali funzioni vengono in genere utilizzate insieme ad altre funzioni, per ottenere informazioni sui membri di una dimensione, di una gerarchia o di un livello.  
  
 Nell'esempio seguente viene illustrato come utilizzare l'oggetto **. Dimensione** **. Gerarchia**, e **. **Funzioni di livello:  
  
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
 [&#41;MDX della dimensione &#40;](../mdx/dimension-mdx.md)   
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Gerarchia &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Livello &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
