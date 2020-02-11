---
title: Utilizzo di espressioni set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1588d955e728830da4417160591a5c2b6c231473
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893498"
---
# <a name="using-set-expressions"></a>Utilizzo di espressioni set


  Un set è costituito da un elenco ordinato di zeri o più tuple. Un set che non contiene tuple è detto set vuoto.  
  
 L'espressione completa di un set è costituita da zero o più tuple specificate in modo esplicito e racchiuse tra parentesi graffe:  
  
 {[{ *Tuple_expression* | *Member_expression* } [, { *Tuple_expression* | *Member_expression* }]...]}  
  
 Le espressioni di membro specificate in un'espressione set vengono convertite in espressioni di tupla a un membro.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono illustrate due espressioni set utilizzate sugli assi Columns e Rows di una query:  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Sull'asse di Columns, il set  
  
 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 è costituito da due membri della dimensione Measures. Sull'asse di Rows, il set  
  
 {([Prodotto]. [Categorie di prodotti]. [Category]. & [4], [DATE]. [Calendario]. [Anno di calendario]. & [2004]),  
  
 ([Prodotto]. [Categorie di prodotti]. [Category]. & [1], [DATE]. [Calendario]. [Anno di calendario]. & [2003]),  
  
 ([Prodotto]. [Categorie di prodotti]. [Category]. & [3], [DATE]. [Calendario]. [Anno di calendario]. & [2004])}  
  
 è costituito da tre tuple, ognuna delle quali contiene due riferimenti espliciti a membri sulla gerarchia Product Categories della dimensione Product e sulla gerarchia Calendar della dimensione Date.  
  
 Per esempi di funzioni che restituiscono set, vedere [utilizzo di membri, Tuple e set &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx).  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
