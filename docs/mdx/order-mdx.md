---
title: Order (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055685"
---
# <a name="order-mdx"></a>Order (MDX)


  Organizza i membri di un set specificato, facoltativamente rispettando o violando la gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *String_Expression*  
 Espressione stringa valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero espresso come stringa.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Order** può essere gerarchica (come specificato tramite il flag **ASC** o **desc** ) o non gerarchica (come specificato tramite il flag **BASC** o **BDESC** ; **B** sta per "Break Hierarchy"). Se viene specificato **ASC** o **desc** , la funzione **Order** dispone innanzitutto i membri in base alla relativa posizione nella gerarchia e quindi Ordina ogni livello. Se si specifica **BASC** o **BDESC** , la funzione **Order** dispone i membri nel set indipendentemente dalla gerarchia. Se non si specifica alcun flag, **ASC** è il valore predefinito.  
  
 Se la funzione **Order** viene utilizzata con un set in cui due o più gerarchie sono Crossjoin e viene utilizzato il flag **desc** , vengono ordinati solo i membri dell'ultima gerarchia nel set. Questa situazione rappresenta una modifica rispetto ad Analysis Services 2000 in cui tutte le gerarchie del set sono ordinate.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito, dal cubo **Adventure Works** , il numero di ordini dei rivenditori per tutti i trimestri di calendario dalla gerarchia Calendar nella dimensione Date. La funzione **Order** riordina il set per l'asse ROWS. La funzione **Order** Ordina il set in `[Reseller Order Count]` base all'ordine gerarchico decrescente in base a `[Calendar]` quanto determinato dalla gerarchia.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Si noti che in questo esempio, quando il flag **desc** viene modificato in **BDESC**, la gerarchia viene interruppe e viene restituito l'elenco di trimestri del calendario senza considerare la gerarchia:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Nell'esempio seguente viene restituita la misura Reseller Sales per le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base a Reseller Gross Profit. La funzione **subset** viene utilizzata per restituire solo le prime 5 tuple nel set dopo che il risultato viene ordinato utilizzando la funzione **Order** .  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 Nell'esempio seguente la funzione **Rank** viene utilizzata per classificare i membri della gerarchia City in base alla misura Reseller Sales Amount e quindi visualizzarli in ordine di classificazione. Utilizzando la funzione **Order** per ordinare innanzitutto il set di membri della gerarchia City, l'ordinamento viene eseguito una sola volta e quindi seguito da un'analisi lineare prima che venga visualizzato in ordine ordinato.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il numero di prodotti del set univoco, utilizzando la funzione **Order** per ordinare le tuple non vuote prima di utilizzare la funzione **Filter** . La funzione **CurrentOrdinal** viene usata per confrontare ed eliminare i vincoli.  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 Per comprendere il funzionamento del flag **desc** con i set di tuple, considerare prima i risultati della query seguente:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Sull'asse delle righe è possibile vedere che i Sales Territory Groups sono stati ordinati in ordine decrescente per Quantità della tassa nel modo seguente: America del Nord, Europa, Pacifico, NA. Osservare ora cosa accade se si Crossjoin il set di gruppi di territorio di vendita con il set di sottocategorie di prodotto e si applica la funzione **Order** nello stesso modo, come indicato di seguito:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Mentre il set Product Subcategories è stato ordinato in modo gerarchico decrescente, gli elementi Sales Territory Groups attualmente non sono ordinati e vengono visualizzati nello stesso ordine in cui sono presenti nella gerarchia, ovvero Europa, NA, America del Nord e Pacific. Questa situazione si verifica perché solo l'ultima gerarchia del set di tuple, ovvero Product Subcategories, è ordinata. Per riprodurre il comportamento di Analysis Services 2000, utilizzare una serie di funzioni di **generazione** annidate per ordinare ogni set prima di Crossjoin, ad esempio:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
