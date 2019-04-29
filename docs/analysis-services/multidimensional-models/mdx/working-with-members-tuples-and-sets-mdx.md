---
title: Uso di membri, tuple e set (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 295a094505fdc2b532f337aaa87dc93ae0923dd2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62988619"
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>Utilizzo di membri, tuple e set (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX offre numerose funzioni che restituiscono uno o più membri, tuple o set oppure eseguono operazioni su un membro, una tupla o un set.  
  
## <a name="member-functions"></a>Funzioni di membro  
 MDX offre diverse funzioni per il recupero di membri da altre entità MDX, ad esempio dimensioni, livelli, set o tuple. Con la funzione [FirstChild](../../../mdx/firstchild-mdx.md) , ad esempio, vengono eseguite operazioni su un membro e viene restituito un membro.  
  
 Per ottenere il primo membro figlio di una dimensione temporale, è possibile indicare il membro in modo esplicito come nell'esempio seguente.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 È inoltre possibile restituire lo stesso membro usando la funzione **FirstChild** , come nell'esempio seguente.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 Per altre informazioni sulle funzioni di membro MDX, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="tuple-functions"></a>funzioni di tupla  
 MDX offre diverse funzioni che restituiscono tuple e che possono essere utilizzate in tutti i casi in cui viene accettata una tupla. La funzione [Item &#40;Tuple&#41; &#40;MDX&#41;](../../../mdx/item-tuple-mdx.md), ad esempio, può essere usata per estrarre la prima tupla dal set e si rivela estremamente utile quando si è certi che un set è costituito da una singola tupla e si desidera specificare tale tupla per una funzione che ne richiede una.  
  
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
  
 Per altre informazioni sulle funzioni di tupla, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="set-functions"></a>Funzioni di set  
 MDX offre diverse funzioni che restituiscono set. La digitazione esplicita di tuple racchiuse tra parentesi graffe non è l'unico metodo disponibile per il recupero di un set. Per altre informazioni sulle funzioni relative ai membri che restituiscono un set, vedere [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md). Sono disponibili numerose funzioni aggiuntive di questo tipo.  
  
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
  
 Per altre informazioni sulle funzioni di set, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="array-functions"></a>Funzioni di matrice  
 Con una funzione per matrici vengono eseguite operazioni su un set e viene restituita una matrice. Per altre informazioni sulle funzioni del di matrice, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="hierarchy-functions"></a>Funzioni di gerarchia  
 Una funzione di gerarchia restituisce una gerarchia eseguendo operazioni su un membro, un livello, una gerarchia o una stringa. Per altre informazioni sulle funzioni di gerarchia, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="level-functions"></a>Funzioni di livello  
 Una funzione di livello restituisce un livello eseguendo operazioni su un membro, un livello o una stringa. Per altre informazioni sulle funzioni di livello, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="logical-functions"></a>Funzioni logiche  
 Con una funzione logica vengono eseguite operazioni su un'espressione MDX per la restituzione di informazioni sulle tuple, sui membri o sui set nell'espressione. La funzione [IsEmpty &#40;MDX&#41;](../../../mdx/isempty-mdx.md), ad esempio, valuta se un'espressione ha restituito un valore di cella vuota. Per altre informazioni sulle funzioni logiche, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="numeric-functions"></a>Funzioni numeriche  
 Con una funzione numerica vengono eseguite operazioni su un'espressione MDX per la restituzione di un valore scalare. La funzione [Aggregate &#40;MDX&#41;](../../../mdx/aggregate-mdx.md), ad esempio, restituisce un valore scalare calcolato mediante l'aggregazione di misure sulle tuple in un set specificato. Per altre informazioni sulle funzioni numeriche, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="string-functions"></a>Funzioni per i valori stringa  
 Con una funzione per i valori stringa vengono eseguite operazioni su un'espressione MDX per la restituzione di una stringa. La funzione [UniqueName &#40;MDX&#41;](../../../mdx/uniquename-mdx.md), ad esempio, restituisce un valore stringa contenente il nome univoco di una dimensione, una gerarchia, un livello o un membro. Per altre informazioni sulle funzioni per i valori stringa, vedere [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
