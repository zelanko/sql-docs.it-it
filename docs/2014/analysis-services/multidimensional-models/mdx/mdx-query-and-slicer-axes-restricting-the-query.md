---
title: Restrizione della Query con Progettazione Query e assi di sezionamento (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3413f4da8443df07732e1c6acca5ed6112cb59dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725345"
---
# <a name="restricting-the-query-with-query-and-slicer-axes-mdx"></a>Restrizione della query con gli assi della query e di sezionamento (MDX)
  Per la formulazione di un'istruzione SELECT di MDX (Multidimensional Expression), un'applicazione in genere analizza il cubo e suddivide il set di gerarchie in due subset:  
  
-   **Assi della query**-il set di gerarchie da cui recuperare i dati per più membri. Per altre informazioni sugli assi delle query, vedere [Impostazione del contenuto di un asse della query &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   **Asse di sezionamento**-il set di gerarchie da cui recuperare i dati per un singolo membro. Per altre informazioni sull'asse di sezionamento, vedere [Impostazione del contenuto di un asse di sezionamento &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
 Poiché gli assi della query e di sezionamento possono essere costruiti da più gerarchie del cubo su cui eseguire la query, questi termini vengono utilizzati per distinguere le gerarchie utilizzate dal cubo su cui eseguire la query dalle gerarchie create nel cubo restituito da una query MDX.  
  
 Per vedere un semplice esempio di uso degli assi delle query e degli assi di sezionamento, vedere [Utilizzo di assi di query e assi di sezionamento in un semplice esempio &#40;MDX&#41;](mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di membri, tuple e set &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
