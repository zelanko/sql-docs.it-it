---
title: Spazio del cubo | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b663f86b16576360083050c5709433eed7d4dc4a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074705"
---
# <a name="cube-space"></a>Spazio del cubo
  Lo spazio del cubo è il prodotto dei membri delle gerarchie dell'attributo di un cubo per le misure del cubo. Quindi lo spazio del cubo è determinato dal prodotto combinatorio di tutti i membri della gerarchia dell'attributo nel cubo e delle misure del cubo e definisce la dimensione massima del cubo. È importante sottolineare che questo spazio comprende tutte le possibili combinazioni di membri della gerarchia dell'attributo, anche combinazioni che si possono considerare impossibili nel mondo reale, ad esempio combinazioni in cui la città è Parigi e i paesi sono Inghilterra o Spagna o Giappone o India o altro.  
  
## <a name="autoexists-and-cube-space"></a>Spazio del cubo e Auto Exist  
 Il concetto di *Auto Exist* limita questo spazio del cubo alle celle effettivamente esistenti. È possibile che membri di una gerarchia dell'attributo non contengano membri di un'altra gerarchia dell'attributo nella stessa dimensione.  
  
 Se, ad esempio, si dispone di un cubo con una gerarchia dell'attributo City, una gerarchia dell'attributo Country e una misura Internet Sales Amount, lo spazio di questo cubo include solo i membri che esistono in ogni livello superiore. Se, ad esempio, la gerarchia dell'attributo City include le città di New York, London, Paris, Tokyo e Melbourne e la gerarchia dell'attributo Country include i paesi Stati Uniti, United Kingdom, France, Japan e Australia, lo spazio del cubo non include lo spazio (cella) nel punto di intersezione tra Paris e Stati Uniti.  
  
 Quando si esegue una query su celle inesistenti, tali celle restituiscono valori Null, cioè non possono contenere calcoli e non è possibile definire un calcolo esegua operazioni di scrittura in questo spazio. L'istruzione seguente, ad esempio, include celle che non esistono.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  In questa query viene usata la funzione [Members (Set) (MDX)](/sql/mdx/members-set-mdx) per restituire il set di membri della gerarchia dell'attributo Gender sull'asse delle colonne e questo set viene incrociato con il set di membri specificato della gerarchia dell'attributo Customer sull'asse delle righe.  
  
 Quando si esegue la query precedente, nella cella nel punto di intersezione tra Aaron A. Allen e Female viene visualizzato un valore null. Analogamente, viene visualizzato un valore Null nella cella nel punto di intersezione tra Abigail Clark e Male. Sebbene non esistano e non possano contenere valori, le celle inesistenti possono essere visualizzate nel risultato restituito da una query.  
  
 Quando si usa la funzione [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) per restituire il prodotto incrociato dei membri della gerarchia dell'attributo dalle gerarchie dell'attributo nella stessa dimensione, Auto Exist limita le tuple da restituire al set di tuple effettivamente esistenti, invece di restituire un prodotto cartesiano completo. Ad esempio, eseguire e quindi esaminare i risultati dell'esecuzione della query seguente.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Si noti che per designare l'asse delle colonne viene utilizzato 0, la forma abbreviata per Axis(0), indicante l'asse delle colonne.  
  
 La query precedente restituisce solo le celle dei membri di ogni gerarchia dell'attributo della query che esistono in ogni livello superiore. La query precedente può anche essere scritta con la nuova variante * della funzione [ \* (Crossjoin) (MDX)](/sql/mdx/crossjoin-mdx) .  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 La query precedente può anche essere scritta nel modo seguente:  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 I valori delle celle restituiti saranno identici, sebbene i metadati nel set di risultati saranno diversi. Con la query precedente, ad esempio, la gerarchia Country è stata spostata sull'asse di sezionamento (nella clausola WHERE) e pertanto non viene visualizzata in modo esplicito nel set di risultati.  
  
 Ognuna di queste tre query precedenti dimostra l'effetto del comportamento di auto exist in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>Gerarchie definite dall'utente e spazio del cubo  
 Negli esempi precedenti di questo argomento vengono definite le posizioni nello spazio del cubo utilizzando le gerarchie dell'attributo. È tuttavia possibile definire una posizione nello spazio del cubo anche utilizzando gerarchie definite dall'utente in base alle gerarchie dell'attributo in una dimensione. Una gerarchia definita dall'utente è una gerarchia di gerarchie dell'attributo utilizzata per facilitare l'esplorazione dei dati del cubo da parte degli utenti.  
  
 È ad esempio possibile scrivere la query `CROSSJOIN` della sezione precedente anche come segue:  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 Nella query precedente la gerarchia definita dall'utente Customer Geography all'interno della dimensione Customer viene utilizzata per definire la posizione nello spazio del cubo definita in precedenza utilizzando una gerarchia dell'attributo. La medesima posizione nello spazio del cubo può essere definita utilizzando gerarchie dell'attributo o gerarchie definite dall'utente.  
  
##  <a name="attribute-relationships-and-cube-space"></a><a name="AttribRelationships"></a> Relazioni tra attributi e spazio del cubo  
 La definizione delle relazioni tra attributi correlati migliora le prestazioni delle query (facilitando la creazione di aggregazioni appropriate) e influisce sul membro di una gerarchia dell'attributo correlata che include un membro della gerarchia dell'attributo. Quando, ad esempio, si definisce una tupla che include un membro della gerarchia dell'attributo City e la tupla non definisce in modo esplicito il membro della gerarchia dell'attributo Country, ci si potrebbe aspettare che il membro predefinito della gerarchia dell'attributo Country fosse il membro correlato della gerarchia dell'attributo Country. Questo tuttavia si verifica solo se tra la gerarchia dell'attributo City e la gerarchia dell'attributo Country è definita una relazione tra attributi.  
  
 Nell'esempio seguente viene restituito il membro di una gerarchia dell'attributo correlata non inclusa in modo esplicito nella query.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Si noti che `WITH` la parola chiave viene utilizzata con le funzioni [CurrentMember (MDX)](/sql/mdx/current-mdx) e [Name (MDX)](/sql/mdx/members-string-mdx) per creare un membro calcolato da utilizzare nella query. Per altre informazioni, vedere [Query MDX di base &#40;MDX&#41;](mdx-query-the-basic-query.md).  
  
 Nella query precedente, viene restituito il nome del membro della gerarchia dell'attributo Country associata a ogni membro della gerarchia dell'attributo State. Viene visualizzato il membro Country previsto, perché tra gli attributi City e Country è definita una relazione. Se tuttavia tra le gerarchie dell'attributo della stessa dimensione non venisse definita alcuna relazione tra attributi, verrebbe restituito il membro (Totale), come illustrato nella query seguente.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 Nella query precedente viene restituito il membro (Totale) ("All Customers"), perché non esiste alcuna relazione tra Education e City. Pertanto, il membro (Totale) della gerarchia dell'attributo Education sarà il membro predefinito della gerarchia dell'attributo Education utilizzata in qualsiasi tupla con la gerarchia dell'attributo City dove nessun membro Education è specificato in modo esplicito.  
  
## <a name="calculation-context"></a>Contesto di calcolo  
  
## <a name="see-also"></a>Vedi anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Tuple](tuples.md)   
 [Autoexists](autoexists.md)   
 [Utilizzo di membri, Tuple e set &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [Totali visivi e totali non visualizzati](visual-totals-and-non-visual-totals.md)   
 [Guida di riferimento al linguaggio MDX &#40;&#41;MDX](/sql/mdx/mdx-language-reference-mdx)   
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
