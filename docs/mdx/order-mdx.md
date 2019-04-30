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
manager: kfile
ms.openlocfilehash: 43a75f4a42193c231c1acc710512b05537675991
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277851"
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
  
## <a name="remarks"></a>Note  
 Il **ordine** funzione possa essere di tipo gerarchica (come specificato dal **ASC** o **DESC** flag) o gerarchico (come specificato dal **BASC**  oppure **BDESC** flag; il **B** è l'acronimo di "rispettare la gerarchia"). Se **ASC** o **DESC** viene specificato, il **ordine** funzione ordina prima i membri in base alla loro posizione nella gerarchia e quindi gli ordini ogni livello. Se **BASC** oppure **BDESC** viene specificato, il **ordine** funzione Organizza i membri del set indipendentemente dalla gerarchia. Viene specificato alcun flag, **ASC** è il valore predefinito.  
  
 Se il **ordine** funzione viene usata con un set in cui sono presenti due o più gerarchie e i **DESC** flag viene utilizzato, vengono ordinati solo i membri dell'ultima gerarchia del set. Questa situazione rappresenta una modifica rispetto ad Analysis Services 2000 in cui tutte le gerarchie del set sono ordinate.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce, dal **Adventure Works** del cubo, il numero di ordini dei rivenditori per tutti elementi Calendar Quarters dalla gerarchia Calendar nella dimensione Date. Il **ordine** funzione Riordina il set per l'asse ROWS. Il **ordine** funzione ordina il set da `[Reseller Order Count]` in ordine gerarchico discendente come stabilito dal `[Calendar]` gerarchia.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Si noti che in questo esempio, quando la **DESC** flag viene impostato su **BDESC**, la gerarchia viene interrotta e l'elenco di elementi Calendar Quarters viene restituito senza considerare la gerarchia:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Nell'esempio seguente viene restituita la misura Reseller Sales per le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base a Reseller Gross Profit. Il **sottoinsieme** funzione viene utilizzata per restituire solo i primi 5 tuple nel set di dopo l'ordinamento del risultato utilizzando il **ordine** (funzione).  
  
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
  
 L'esempio seguente usa il **Rank** funzione per classificare i membri della gerarchia City in base alla misura Reseller Sales Amount e visualizzarli in ordine di rango. Tramite il **ordine** funzione per ordinare il set di membri della gerarchia City, l'ordinamento viene eseguito una sola volta ed è seguito da un'analisi lineare prima di essere visualizzato in modo ordinato.  
  
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
  
 L'esempio seguente restituisce il numero di prodotti nel set che sono univoche, tramite il **ordine** funzione per ordinare le tuple non vuote prima di applicare le **filtro** (funzione). Il **CurrentOrdinal** funzione viene utilizzata per confrontare ed eliminare i valori equivalenti.  
  
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
  
 Per comprendere come il **DESC** flag funziona con i set di tuple, considerare innanzitutto i risultati della query seguente:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Sull'asse delle righe è possibile vedere che i Sales Territory Groups sono stati ordinati in ordine decrescente per quantità della tassa nel modo seguente: Nord America, Europe, Pacific, NA. Osservare cosa accade se è crossjoin il set di Sales Territory Groups con il set di Product Subcategories e si applicano i **ordine** funzionano nello stesso modo, come indicato di seguito:  
  
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
  
 Mentre il set di Product Subcategories è stato ordinato in ordine gerarchico decrescente gli elementi Sales Territory Groups attualmente non sono ordinati e vengono visualizzati in ordine che vengono visualizzati nella gerarchia: Europe, NA, North America e Pacific. Questa situazione si verifica perché solo l'ultima gerarchia del set di tuple, ovvero Product Subcategories, è ordinata. Per riprodurre il comportamento di Analysis Services 2000, utilizzare una serie di annidati **genera** funzioni per ordinare ogni set prima che venga eseguito il cross join, ad esempio:  
  
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
  
  
