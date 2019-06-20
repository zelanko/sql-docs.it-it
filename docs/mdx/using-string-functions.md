---
title: Uso di funzioni stringa | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e151d06d086569b16fcdf1dc3570f9b220dfcd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62928154"
---
# <a name="using-string-functions"></a>Utilizzo di funzioni stringa


  Nel linguaggio MDX (Multidimensional Expressions) è possibile utilizzare funzioni stringa su quasi tutti gli oggetti. Nelle stored procedure le funzioni stringa vengono utilizzate principalmente per convertire un oggetto in una rappresentazione stringa. Le funzioni stringa possono essere inoltre utilizzate per valutare un'espressione stringa su un oggetto per restituire un valore.  
  
 Le funzioni di stringa più diffuse sono **Name** e **Uniquename**. Queste funzioni restituiscono rispettivamente il nome e il nome univoco di un oggetto. Sono utilizzate soprattutto durante i calcoli di debug per individuare quale membro viene restituito da una funzione.  
  
## <a name="examples"></a>Esempi  
 Negli esempi di query seguenti viene illustrato l'utilizzo di queste funzioni:  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Il **genera** funzione può essere utilizzata per eseguire una funzione stringa su ogni membro di un set e concatenare i risultati. Può essere utile anche durante il debug di calcoli in quanto consente di visualizzare il contenuto di un set. Nell'esempio seguente viene illustrato questo tipo di utilizzo:  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Un altro gruppo di funzioni per i valori stringa molto diffuso è costituito dalle funzioni che consentono di eseguire il cast di una stringa che contiene il nome univoco di un oggetto o un'espressione che viene risolta nell'oggetto all'interno dell'oggetto stesso. La query di esempio seguente viene illustrato come la **StrToMember** e **StrToSet** funzioni eseguire questa operazione:  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  Il **StrToMember** e **StrToSet** funzioni devono essere utilizzate con cautela. in quanto, se utilizzate all'interno di definizioni di calcoli, possono ridurre drasticamente le prestazioni delle query.  
  
## <a name="see-also"></a>Vedere anche  
 [Generate &#40;MDX&#41;](../mdx/generate-mdx.md)   
 [Nome &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Le funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Utilizzo delle Stored procedure &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
