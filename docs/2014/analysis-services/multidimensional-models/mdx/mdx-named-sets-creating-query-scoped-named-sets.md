---
title: Creazione di set denominati con ambito query (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- query-scoped named sets [MDX]
- WITH keyword
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a611d3d20d269bb9c3fa3a1f764181b1660713b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074065"
---
# <a name="creating-query-scoped-named-sets-mdx"></a>Creazione di set denominati con ambito query (MDX)
  Se un set denominato è richiesto esclusivamente per una sola query MDX (Multidimensional Expressions), è possibile definirlo specificando la parola chiave WITH. Un set denominato creato specificando questa parola chiave non esiste più dopo l'esecuzione della query.  
  
 Come descritto in questo argomento, la sintassi della parola chiave WITH è piuttosto flessibile e consente addirittura di definire un set denominato tramite l'utilizzo di funzioni.  
  
> [!NOTE]  
>  Per altre informazioni sui set denominati, vedere [Compilazione di set denominati in MDX &#40;MDX&#41;](mdx-named-sets-building-named-sets.md).  
  
## <a name="with-keyword-syntax"></a>Sintassi della parola chiave WITH  
 Per aggiungere la parola chiave WITH a un'istruzione MDX SELECT, utilizzare la sintassi seguente:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 Il parametro `Set_Identifier` include l'alias del set denominato. Il parametro `Set_Expression` include l'espressione set a cui fa riferimento l'alias del set denominato.  
  
## <a name="with-keyword-example"></a>Esempio della parola chiave WITH  
 Nella query MDX seguente vengono esaminate le vendite unitarie dei vari vini Chardonnay e Chablis in `FoodMart 2000`, il database di esempio per Microsoft SQL Server 2000 Analysis Services. Questa query, sebbene piuttosto semplice dal punto di vista del set di risultati, è lunga e laboriosa per quanto riguarda la manutenzione.  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 Per semplificare la manutenzione della query, è possibile creare un set denominato specificando la parola chiave WITH. Nel codice seguente viene illustrato l'utilizzo della parola chiave WITH per creare il set denominato `[ChardonnayChablis]`. Viene illustrato inoltre come grazie al set denominato l'istruzione SELECT risulti più breve e di più semplice manutenzione.  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### <a name="using-functions-together-with-the-with-keyword"></a>Utilizzo di funzioni insieme alla parola chiave WITH  
 Sebbene sia possibile definire ogni membro di un set denominato in modo esplicito, con questo approccio si potrebbe ottenere un'istruzione eccessivamente lunga. Per semplificare la creazione e la manutenzione di un set denominato, è possibile definirne i membri tramite funzioni MDX.  
  
 Nella query MDX seguente vengono ad esempio utilizzate le funzioni MDX [Filter](/sql/mdx/filter-mdx), [CurrentMember](/sql/mdx/current-mdx)e [Name](/sql/mdx/members-string-mdx) e la funzione VBA InStr per creare il set denominato `[ChardonnayChablis]` . Questa versione del set denominato `[ChardonnayChablis]` è equivalente alla versione definita in modo esplicito descritta più indietro in questo argomento.  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Creazione di set denominati con ambito sessione &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  
