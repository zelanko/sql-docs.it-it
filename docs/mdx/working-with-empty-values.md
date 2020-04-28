---
title: Utilizzo di valori vuoti | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae8d6262f6502add09376b76a767a3076c830cb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125853"
---
# <a name="working-with-empty-values"></a>Utilizzo di valori vuoti


  Un valore vuoto indica che un determinato membro, tupla o cella è vuoto. Una cella vuota indica che nella tabella dei fatti sottostante non è possibile trovare i dati per la cella specificata oppure che la tupla per la cella specificata rappresenta una combinazione di membri non applicabile per il cubo.  
  
> [!NOTE]  
>  Sebbene un valore vuoto sia diverso da un valore zero, i valori vuoti vengono gestiti come zero nella maggior parte dei casi.  
  
 Nella query seguente viene illustrato il comportamento di valori vuoti e zero:  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 Per i valori vuoti vale quanto segue:  
  
-   La funzione [IsEmpty](../mdx/isempty-mdx.md) restituisce **true** solo se la cella identificata dalla tupla specificata nella funzione è vuota. In caso contrario, la funzione restituisce **false**.  
  
    > [!NOTE]  
    >  La funzione **IsEmpty** non è in grado di determinare se un'espressione di membro restituisce un valore null. Per determinare se un'espressione restituisce un membro null, utilizzare l'operatore [is](../mdx/is-mdx.md).  
  
-   Quando il valore di cella vuota è un operando per un operatore numerico (+, -, *, /), verrà trattato come zero se l'altro operando è un valore non vuoto. Se entrambi gli operandi sono vuoti, l'operatore numerico restituirà il valore di cella vuota.  
  
-   Quando il valore di cella vuota è un operando per l'operatore di concatenazione delle stringhe (+), verrà trattato come una stringa vuota se l'altro operando è un valore non vuoto. Se entrambi gli operandi sono vuoti, l'operatore di concatenazione delle stringhe restituirà il valore di cella vuota.  
  
-   Quando il valore di cella vuota è un operando per gli operatori di confronto (=. <>, >=, \<=, >, <), il valore di cella vuota viene considerato come zero o come una stringa vuota, a seconda che il tipo di dati dell'altro operando sia numerico o stringa, rispettivamente. Se entrambi gli operandi sono vuoti, verranno trattati come zero.  
  
-   Quando si confrontano valori numerici, il valore di cella vuota occupa la stessa posizione dello zero. Nel confronto tra il valore di cella vuota e lo zero, il valore di cella vuota precede lo zero.  
  
-   Quando si confrontano valori stringa, il valore di cella vuota occupa la stessa posizione della stringa vuota. Nel confronto tra il valore di cella vuota e la stringa vuota, il valore di cella vuota precede la stringa vuota.  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>Gestione di valori vuoti in cubi e istruzioni MDX  
 Nelle istruzioni MDX (Multidimensional Expressions) è possibile cercare valori vuoti e quindi eseguire determinati calcoli su celle contenenti dati validi, ovvero non vuote. L'eliminazione dei valori vuoti prima dell'esecuzione dei calcoli può essere molto importante, perché se vengono incluse celle vuote alcuni calcoli, ad esempio il calcolo della media, non vengono eseguiti correttamente.  
  
 Se nei dati della tabella dei fatti sottostante sono archiviati dei valori vuoti, per impostazione predefinita tali valori saranno convertiti in zeri durante l'elaborazione del cubo. È possibile utilizzare l'opzione di **elaborazione dei valori null** in una misura per controllare se i fact null vengono convertiti in 0, convertiti in un valore vuoto o addirittura generano un errore durante l'elaborazione. Se non si desidera che nei risultati di una query appaiano valori di cella vuoti, è necessario creare query, membri calcolati o istruzioni di script MDX che eliminano i valori vuoti o li sostituiscono con altri valori.  
  
 Per rimuovere righe o colonne vuote da una query, è possibile utilizzare l'istruzione NON EMPTY prima della definizione del set di assi. Ad esempio, nella query seguente viene restituita solo la categoria di prodotti Bikes perché è l'unica categoria che ha avuto vendite nell'anno 2001:  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 Più genericamente, per rimuovere tuple vuote da un set è possibile utilizzare la funzione NonEmpty. Nella query seguente vengono illustrate due misure calcolate, una delle quali conta il numero di Categorie prodotto e l'altra mostra il numero di Categorie prodotto che contengono valori per la misura [Imposte Internet] e per l’anno 2001:  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 Per ulteriori informazioni, vedere [&#41;MDX &#40;non empty ](../mdx/nonempty-mdx.md).  
  
## <a name="empty-values-and-comparison-operators"></a>Valori vuoti e operatori di confronto  
 Se i dati includono valori vuoti, oltre a TRUE e FALSE gli operatori logici e di confronto possono restituire un terzo valore, EMPTY. Questa logica a tre valori è necessaria, ma causa numerosi errori nelle applicazioni. Nelle tabelle seguenti vengono indicati i risultati ottenuti quando si includono valori vuoti in un confronto.  
  
 Nella tabella seguente vengono indicati i risultati ottenuti quando si applica l'operatore AND a due operandi booleani.  
  
|AND|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**TRUE**|TRUE|FALSE|FALSE|  
|**VUOTO**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 Nella tabella seguente vengono indicati i risultati ottenuti quando si applica l'operatore OR a due operandi booleani.  
  
|OR|TRUE|FALSE|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**VUOTO**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 Nella tabella seguente viene illustrato come l'operatore NOT esegue la negazione, ovvero inverte, il risultato di un operatore booleano.  
  
|Espressione booleana a cui viene applicato l'operatore NOT|Valutato su|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)   
 [Espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
