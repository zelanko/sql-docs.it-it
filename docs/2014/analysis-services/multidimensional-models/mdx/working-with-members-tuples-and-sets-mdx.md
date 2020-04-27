---
title: Utilizzo di membri, Tuple e set (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], tuples
- member keys [MDX]
- MDX [Analysis Services], sets
- calculated members [MDX]
- members [MDX]
- Multidimensional Expressions [Analysis Services], members
- named sets [MDX]
- Multidimensional Expressions [Analysis Services], tuples
- member functions [MDX]
- sets [MDX]
- MDX [Analysis Services], members
- member names [MDX]
- Multidimensional Expressions [Analysis Services], sets
- tuple functions
- tuples
- set functions [MDX]
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a8532b20ae5b71a9ef2353893272c628b9a80b3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073674"
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>Utilizzo di membri, tuple e set (MDX)
  MDX offre numerose funzioni che restituiscono uno o più membri, tuple o set oppure eseguono operazioni su un membro, una tupla o un set.  
  
## <a name="member-functions"></a>Funzioni di membro  
 MDX offre diverse funzioni per il recupero di membri da altre entità MDX, ad esempio dimensioni, livelli, set o tuple. Con la funzione [FirstChild](/sql/mdx/firstchild-mdx) , ad esempio, vengono eseguite operazioni su un membro e viene restituito un membro.  
  
 Per ottenere il primo membro figlio di una dimensione temporale, è possibile indicare il membro in modo esplicito come nell'esempio seguente.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 È inoltre possibile restituire lo stesso membro utilizzando la funzione `FirstChild`, come nell'esempio seguente.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 Per altre informazioni sulle funzioni di membro MDX, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="tuple-functions"></a>funzioni di tupla  
 MDX offre diverse funzioni che restituiscono tuple e che possono essere utilizzate in tutti i casi in cui viene accettata una tupla. La funzione [Item &#40;Tuple&#41; &#40;MDX&#41;](/sql/mdx/item-tuple-mdx), ad esempio, può essere usata per estrarre la prima tupla dal set e si rivela estremamente utile quando si è certi che un set è costituito da una singola tupla e si desidera specificare tale tupla per una funzione che ne richiede una.  
  
 Nell'esempio seguente viene restituita la prima tupla dal set di tuple sull'asse delle colonne.  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 Per altre informazioni sulle funzioni di tupla, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="set-functions"></a>Funzioni di set  
 MDX offre diverse funzioni che restituiscono set. La digitazione esplicita di tuple racchiuse tra parentesi graffe non è l'unico metodo disponibile per il recupero di un set. Per altre informazioni sulle funzioni relative ai membri che restituiscono un set, vedere [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md). Sono disponibili numerose funzioni aggiuntive di questo tipo.  
  
 L'operatore Range (:) consente di utilizzare l'ordine naturale dei membri per la creazione di un set. Il set illustrato nell'esempio seguente contiene le tuple per i primi quattro trimestri dell'anno di calendario 2002.  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 Se non si utilizza l'operatore Range (:) per creare il set, è possibile creare lo stesso set di membri specificando le tuple come illustrato nell'esempio seguente:  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 L'operatore Range (:) è una funzione inclusiva. I membri ai due lati dell'operatore vengono infatti inclusi nel set risultante.  
  
 Per altre informazioni sulle funzioni di set, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="array-functions"></a>Funzioni di matrice  
 Con una funzione per matrici vengono eseguite operazioni su un set e viene restituita una matrice. Per altre informazioni sulle funzioni del di matrice, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="hierarchy-functions"></a>Funzioni di gerarchia  
 Una funzione di gerarchia restituisce una gerarchia eseguendo operazioni su un membro, un livello, una gerarchia o una stringa. Per altre informazioni sulle funzioni di gerarchia, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="level-functions"></a>Funzioni di livello  
 Una funzione di livello restituisce un livello eseguendo operazioni su un membro, un livello o una stringa. Per altre informazioni sulle funzioni di livello, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="logical-functions"></a>Funzioni logiche  
 Con una funzione logica vengono eseguite operazioni su un'espressione MDX per la restituzione di informazioni sulle tuple, sui membri o sui set nell'espressione. La funzione [IsEmpty &#40;MDX&#41;](/sql/mdx/isempty-mdx), ad esempio, valuta se un'espressione ha restituito un valore di cella vuota. Per altre informazioni sulle funzioni logiche, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="numeric-functions"></a>Funzioni numeriche  
 Con una funzione numerica vengono eseguite operazioni su un'espressione MDX per la restituzione di un valore scalare. La funzione [Aggregate &#40;MDX&#41;](/sql/mdx/aggregate-mdx), ad esempio, restituisce un valore scalare calcolato mediante l'aggregazione di misure sulle tuple in un set specificato. Per altre informazioni sulle funzioni numeriche, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="string-functions"></a>Funzioni stringa  
 Con una funzione per i valori stringa vengono eseguite operazioni su un'espressione MDX per la restituzione di una stringa. La funzione [UniqueName &#40;MDX&#41;](/sql/mdx/uniquename-mdx), ad esempio, restituisce un valore stringa contenente il nome univoco di una dimensione, una gerarchia, un livello o un membro. Per altre informazioni sulle funzioni per i valori stringa, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="see-also"></a>Vedi anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
