---
title: Definizione del contesto di cubo in una Query (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9f0f960c531fac8bae8f03479bacd507ffc3078
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074595"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>Definizione del contesto di cubo in una query (MDX)
  Ogni query MDX viene eseguita nel contesto di cubo specificato. Tale contesto definisce i membri che vengono valutati dalle espressioni incluse nella query.  
  
 Il contesto di cubo è determinato dalla clausola FROM dell'istruzione SELECT. Può corrispondere all'intero cubo o a una sezione del cubo, o sottocubo. Dopo aver specificato il contesto di cubo tramite la clausola FROM, è possibile utilizzare funzioni aggiuntive per espandere o limitare tale contesto.  
  
> [!NOTE]  
>  Per la gestione del contesto di cubo è inoltre possibile utilizzare le istruzioni SCOPE e CALCULATE che consentono di gestire il contesto in uno script MDX. Per altre informazioni, vedere [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md).  
  
## <a name="from-clause-syntax"></a>Sintassi della clausola FROM  
 La sintassi della clausola FROM è la seguente:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 Si noti che il cubo o sottocubo in cui viene eseguita l'istruzione SELECT è descritta nella clausola `<SELECT subcube clause>` .  
  
 Una clausola FROM semplice viene eseguita nell'intero cubo di esempio Adventure Works. Il formato di tale clausola è il seguente:  
  
```  
FROM [Adventure Works]  
```  
  
 Per altre informazioni sulla clausola FROM nell'istruzione MDX SELECT, vedere [Istruzione SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select).  
  
## <a name="refining-the-context"></a>Ridefinizione del contesto  
 Sebbene la clausola FROM specifichi il contesto di cubo come singolo cubo, ciò non impedisce di utilizzare i dati di più cubi contemporaneamente.  
  
 Tramite la funzione MDX [LookupCube](/sql/mdx/lookupcube-mdx) è possibile recuperare dati di cubi all'esterno del contesto di cubo. Sono inoltre disponibili funzioni che consentono una limitazione temporale del contesto durante la valutazione della query, ad esempio la funzione [Filter](/sql/mdx/filter-mdx) .  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
