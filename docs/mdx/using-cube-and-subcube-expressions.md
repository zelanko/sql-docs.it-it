---
title: Uso di espressioni di cubo e sottocubo | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f13d92c114783646bbeab9451c3d212ff01b8f8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125427"
---
# <a name="using-cube-and-subcube-expressions"></a>Utilizzo di espressioni di cubo e sottocubo


  È possibile utilizzare espressioni di cubo e sottocubo in istruzioni MDX (Multidimensional Expressions) per definire, modificare o recuperare dati da un cubo o da un sottocubo.  
  
## <a name="cube-expressions"></a>Espressioni di cubo  
 Un'espressione di cubo contiene un identificatore di cubo o la parola chiave CURRENTCUBE e pertanto può essere solo un'espressione semplice. In molte istruzioni MDX viene utilizzata la parola chiave CURRENTCUBE per identificare il contesto del cubo corrente anziché richiedere un identificatore di cubo.  
  
 Identificatore del cubo viene visualizzato come *Cube_Name* nelle descrizioni della annotazione BNF delle istruzioni MDX.  
  
 Le espressioni di cubo possono essere visualizzate in diverse posizioni. In un'istruzione MDX SELECT, tali espressioni specificano il cubo dal quale vengono recuperati i dati. Nell'esempio di query seguente, l'espressione [Adventure Works] fa riferimento all'omonimo cubo:  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 Nell'istruzione CREATE MEMBER, l'espressione di cubo specifica il cubo su cui viene visualizzato il membro calcolato che si sta creando. Nell'esempio seguente, l'istruzione crea una misura calcolata nella dimensione Measures del cubo Adventure Works:  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 Quando si utilizza l'istruzione CREATE MEMBER in uno script MDX, il nome del cubo può essere sostituito dalla parola chiave CURRENTCUBE, poiché il cubo dove deve essere creato il membro calcolato deve essere lo stesso cubo al quale appartiene lo script MDX, come illustrato nell'esempio seguente:  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 Diventa così più semplice copiare e incollare le definizioni dei membri calcolati da un cubo a un altro, dal momento che il nome del cubo non è più specificato a livello di codice.  
  
## <a name="subcube-expressions"></a>Espressioni di sottocubo  
 Un'espressione di sottocubo può contenere un identificatore di sottocubo o un'istruzione MDX che restituisce un sottocubo. Se l'espressione di sottocubo contiene un identificatore di sottocubo, sarà un'espressione semplice. Se invece contiene un'istruzione MDX che restituisce un sottocubo, sarà un'istruzione complessa. L'istruzione MDX SELECT ad esempio, restituisce un sottocubo e può essere utilizzata in tutte le situazioni in cui sono consentite espressioni di sottocubo, come illustrato nell'esempio seguente:  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 Questo utilizzo di un'istruzione SELECT nella clausola FROM viene definito anche come selezione secondaria.  
  
 Un altro scenario comune dove si incontrano espressioni di sottocubo è durante le assegnazioni con ambito in uno script MDX. Nell'esempio seguente, l'istruzione SCOPE viene utilizzata per limitare un'assegnazione a un sottocubo costituito da [Measures].[Internet Sales Amount]:  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 Un identificatore di sottocubo viene visualizzato come *Subcube_Name*. nelle descrizioni della annotazione BNF delle istruzioni MDX.  
  
## <a name="see-also"></a>Vedere anche  
 [Query MDX di base &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Compilazione di sottocubi in MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)   
 [Istruzione CREATE SUBCUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [Le espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [Istruzione SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)  
  
  
