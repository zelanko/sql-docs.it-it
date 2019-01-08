---
title: Impostazione del contenuto di un asse della Query (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38a48fd99ae9a03599914a1dfdac0bf204301c4c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399574"
---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-query-axis"></a>Query MDX e assi di sezionamento - Specificare il contenuto di un asse di query
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gli assi della query specificano i bordi di un set di celle restituito dall'istruzione SELECT di MDX (Multidimensional Expression). L'impostazione dei bordi di un set di celle consente di limitare i dati restituiti visibili al client.  
  
 Per specificare gli assi della query è necessario assegnare un set a un asse particolare utilizzando `<SELECT query axis clause>` . Ogni valore `<SELECT query axis clause>` definisce un asse della query. Il numero di assi nel set di dati è pari al numero di valori `<SELECT query axis clause>` nell'istruzione SELECT.  
  
## <a name="query-axis-syntax"></a>Sintassi degli assi della query  
 Di seguito è illustrata la sintassi per `<SELECT query axis clause>`:  
  
```  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression [ <SELECT dimension property list clause> ] [<HAVING clause>]  
   ON {  
      Integer_Expression |   
      AXIS( Integer_Expression ) |   
      {COLUMNS | ROWS | PAGES | SECTIONS | CHAPTERS}     
      }  
  
```  
  
 Ogni asse della query è associato a un numero: zero (0) per l'asse X, 1 per l'asse Y, 2 per l'asse Z e così via. Nella sintassi per `<SELECT query axis clause>`, il valore `Integer_Expression` specifica il numero dell'asse. Una query MDX può supportare fino a 128 assi specificati ma pochissime query MDX utilizzano più di cinque assi. Per i primi cinque assi è possibile utilizzare gli alias COLUMNS, ROWS, PAGES, SECTIONS e CHAPTERS.  
  
 Una query MDX non può ignorare gli assi della query. In altre parole, una query che include almeno un asse della query non deve escludere gli assi con una numerazione più bassa o intermedia. Ad esempio, una query non può includere un asse ROWS senza un asse COLUMNS oppure gli assi COLUMNS e PAGES senza un asse ROWS.  
  
 È tuttavia possibile specificare una clausola SELECT senza assi, ovvero una clausola SELECT vuota. In questo caso, tutte le dimensioni sono dimensioni di sezionamento e la query MDX seleziona una cella.  
  
 Nella sintassi dell'asse della query riportata in precedenza, ogni valore `Set_Expression` specifica il set che definisce il contenuto dell'asse della query. Per altre informazioni sui set, vedere [Utilizzo di membri, tuple e set &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="examples"></a>Esempi  
 L'istruzione SELECT semplice seguente restituisce la misura Internet Sales Amount nell'asse Columns e utilizza la funzione MDX MEMBERS per restituire tutti i membri della gerarchia Calendar nella dimensione Date sull'asse delle righe:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 Le due query seguenti restituiscono esattamente gli stessi risultati, ma illustrano l'utilizzo dei numeri degli assi anziché degli alias.  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON 0,  
{[Date].[Calendar].MEMBERS} ON 1  
FROM [Adventure Works]  
  
SELECT {[Measures].[Internet Sales Amount]} ON AXIS(0),  
{[Date].[Calendar].MEMBERS} ON AXIS(1)  
FROM [Adventure Works]  
  
```  
  
 La parola chiave NON EMPTY, utilizzata prima delle definizione del set, è un rapido metodo per rimuovere tutte tuple vuote da un asse. Ad esempio, negli esempi che abbiamo visto finora non vi è alcun dato nel cubo dall'agosto 2004 e versioni successive. Per rimuovere tutte le righe dal set di celle che non includono dati in alcuna colonna, è sufficiente aggiungere NON EMPTY prima del set nella definizione dell'asse delle righe, nel modo seguente:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 È possibile utilizzare NON EMPTY in tutti gli assi in una query. Confrontare i risultati delle due query seguenti, la prima delle quali non utilizza NON EMPTY, mentre la seconda delle quali utilizza NON EMPTY su entrambi gli assi.  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
SELECT NON EMPTY {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
```  
  
 È possibile utilizzare la clausola HAVING per filtrare il contenuto di un asse in base a criteri specifici. Benché sia meno flessibile di altri metodi che producono gli stessi risultati, ad esempio la funzione FILTER, è più semplice da utilizzare. Nell'esempio seguente vengono restituite solo le date in cui Internet Sales Amount è maggiore di $15,000:  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Date].MEMBERS}   
HAVING [Measures].[Internet Sales Amount]>15000  
ON ROWS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione del contenuto di un asse di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
