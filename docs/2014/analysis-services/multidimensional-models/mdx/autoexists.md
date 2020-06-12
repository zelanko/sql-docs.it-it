---
title: Auto Exist | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 56283497-624c-45b5-8a0d-036b0e331d22
author: minewiskan
ms.author: owend
ms.openlocfilehash: dd35958a364456c12d58392afe3754f6adcf97b8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546593"
---
# <a name="autoexists"></a>Auto Exist
  Il concetto di *Auto Exist* limita lo spazio del cubo a quelle celle che esistono effettivamente nel cubo, in contrapposizione con quelle che potrebbero esistere come risultato della creazione di tutte le possibili combinazioni di membri delle gerarchie di attributi dalla medesima gerarchia. La distinzione è necessaria perché i membri di una gerarchia di attributi non possono coesistere con membri di un'altra gerarchia di attributi nella stessa dimensione. Quando in un'istruzione SELECT si utilizzano due o più gerarchie di attributi della medesima dimensione, Analysis Services valuta le espressioni degli attributi per verificare che i relativi membri siano correttamente limitati per soddisfare i criteri di tutti gli altri attributi.  
  
 Si supponga ad esempio di utilizzare gli attributi della dimensione Geografia. Se una delle espressioni restituisce tutti i membri dell'attributo Città e un'altra limita i membri dell'attributo Paese a tutti i paesi Europai, allora i membri di Città saranno limitati alle sole città che appartengono a paesi Europai. Ciò è dovuto alla caratteristica Auto Exist in Analysis Services. un quanto tenta di impedire che i record di dimensioni esclusi nell'espressione di un attributo vengano inclusi dalle espressioni di altri attributi. La caratteristica Auto Exist può inoltre essere interpretata come l'intersezione risultante da diverse espressioni di attributi su righe di dimensioni.  
  
## <a name="cell-existence"></a>Esistenza della cella  
 Le celle seguenti esistono sempre:  
  
-   Il membro (Totale), di ogni gerarchia, quando incrociato con membri di altre gerarchie nella stessa dimensione.  
  
-   Membri calcolati quando incrociati con gli elementi di pari livello non calcolati o con i padri o discendenti degli elementi di pari livello non calcolati.  
  
## <a name="providing-non-existing-cells"></a>Celle non esistenti  
 Una cella non esistente è una cella fornita dal sistema in risposta a una query o a un calcolo che richiede una cella che non esiste nel cubo. Se, ad esempio, si dispone di un cubo con una gerarchia dell'attributo City e una gerarchia dell'attributo Country che appartiene alla dimensione Geography e una misura Internet Sales Amount, lo spazio di questo cubo include solo i membri che esistono in ogni livello superiore. Se, ad esempio, la gerarchia dell'attributo City include le città di New York, London, Paris, Tokyo e Melbourne e la gerarchia dell'attributo Country include i paesi Stati Uniti, United Kingdom, France, Japan e Australia, lo spazio del cubo non include lo spazio (cella) nel punto di intersezione tra Paris e Stati Uniti.  
  
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
  
 La query precedente restituisce solo le celle dei membri di ogni gerarchia dell'attributo della query che esistono in ogni livello superiore. La query precedente può anche essere scritta con la nuova variante * della funzione [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) .  
  
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
  
 Ognuna di queste tre query precedenti dimostra l'effetto del comportamento di auto exist in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
## <a name="deep-and-shallow-autoexists"></a>Auto Exist completo e superficiale  
 La caratteristica Auto Exist può essere applicata in modo completo o superficiale alle espressioni. `Deep Autoexists` significa che tutte le espressioni verranno valutate per soddisfare lo spazio più completo possibile dopo l'applicazione delle espressioni di sezionamento, delle espressioni sub-SELECT nell'asse e così via. `Shallow Autoexists` significa che espressioni esterne vengono valutate prima dell'espressione corrente e i risultati vengono specificati nell'espressione corrente. Per impostazione predefinita la caratteristica Auto Exist viene applicata in modo completo.  
  
 Lo scenario e gli esempi riportati di seguito consentiranno di illustrare i tipi diversi di Auto Exist. Negli esempi riportati di seguito verranno creati due set, uno come espressione calcolata e l'altro come espressione costante.  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 Il set di risultati che si ottiene è il seguente:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Road-150**|**$2,363,805.16**|**$0,00**|**0,00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 Il set di prodotti ottenuto sembra uguale a Preferred10Products, riportato di seguito per verifica:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 In base ai risultati seguenti, i due set (Top10SellingProducts, Preferred10Products) sono identici  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Road-150**|**$2,363,805.16**|**$0,00**|**0,00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 come illustrato nell'esempio seguente. Nell'esempio si filtra Top10SellingProducts in base all'attributo [Product].[Product Line] per i membri del gruppo [Mountain]. Si noti che entrambi gli attributi (sezionamento e asse) appartengono alla stessa dimensione, [Product].  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Viene prodotto il set di risultati seguente:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1,62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0.05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0.05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0.04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2,56%**|  
  
 Nel set di risultati precedente si registrano sette nuove presenze nell'elenco Top10SellingProducts, mentre Mountain-200, Mountain-100 e HL Mountain Frame sono stati spostati all'inizio dell'elenco. Questi tre valori sono frammisti.  
  
 Questa caratteristica viene denominata Auto Exist completa perché il set Top10SellingProducts viene valutato per soddisfare le condizioni di sezionamento della query. Auto Exist completo significa che tutte le espressioni verranno valutate per soddisfare lo spazio più completo possibile dopo l'applicazioni delle espressioni di sezionamento, delle espressioni sub-SELECT nell'asse e così via.  
  
 Tuttavia, è possibile decidere di eseguire l'analisi su Top10SellingProducts, in quanto equivalente a Preferred10Products, come nell'esempio seguente:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Viene prodotto il set di risultati seguente:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
  
 Nei risultati precedenti il sezionamento fornisce un risultato che contiene solo i prodotti dell'elenco Preferred10Products che fanno parte del gruppo [Mountain] in [Product].[Product Line], come previsto, in quanto Preferred10Products è un'espressione costante.  
  
 Questo set di risultati viene interpretato anche come Auto Exist superficiale, in quanto l'espressione viene valutata prima della clausola di sezionamento. Nell'esempio precedente, l'espressione è un'espressione costante a scopo illustrativo, al fine di presentare il concetto.  
  
 Il comportamento di Auto Exist può essere modificato a livello di sessione utilizzando la proprietà della stringa di connessione `Autoexists`. L'esempio seguente inizia con l'apertura di una nuova sessione e l'aggiunta della proprietà *Autoexists=3* alla stringa di connessione. Per eseguire l'esempio, è necessario aprire una nuova connessione. Una volta stabilita la connessione con l'impostazione Auto Exist, quest'ultima rimarrà effettiva fino al termine della connessione.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Nel set di risultati seguente è illustrato il comportamento superficiale di Auto Exist.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
  
 Il comportamento di Auto Exist può essere modificato utilizzando il parametro auto EXISTs = [1 | 2 | 3] nella stringa di connessione. vedere [Proprietà XMLA supportate &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> per l'utilizzo dei parametri.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Spazio del cubo](cube-space.md)   
 [Tuple](tuples.md)   
 [Utilizzo di membri, Tuple e set &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [Totali visivi e totali non visualizzati](visual-totals-and-non-visual-totals.md)   
 [Guida di riferimento al linguaggio MDX &#40;&#41;MDX](/sql/mdx/mdx-language-reference-mdx)   
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
