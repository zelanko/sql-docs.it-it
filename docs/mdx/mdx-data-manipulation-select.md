---
title: Istruzione SELECT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83a381e36a31542d6ad39ed9d26864350004af5c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891143"
---
# <a name="mdx-data-manipulation---select"></a>Manipolazione dei dati MDX - SELECT


  Recupera dati da un cubo specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Integer*  
 Valore integer compreso tra 0 e 127.  
  
 *Cube_Name*  
 Stringa valida che specifica il nome di un cubo.  
  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
 *CellProperty_Name*  
 Stringa valida che rappresenta la proprietà di una cella.  
  
 *DimensionProperty_Name*  
 Stringa valida che rappresenta la proprietà di una dimensione.  
  
 *LevelProperty_Name*  
 Stringa valida che rappresenta la proprietà di un livello.  
  
 *MemberProperty_Name*  
 Stringa valida che rappresenta la proprietà di un membro.  
  
## <a name="remarks"></a>Note  
 L'espressione `<SELECT slicer axis clause>` deve contenere membri di dimensioni e gerarchie diverse da quelle a cui fanno riferimento le espressioni `<SELECT query axis clause>` specificate.  
  
 Se nelle espressioni `<SELECT query axis clause>` specificate e nel valore `<SELECT slicer axis clause>` viene omesso un attributo del cubo, il membro predefinito dell'attributo viene aggiunto in modo implicito all'asse di sezionamento.  
  
 L'opzione NON VISUAL nell'istruzione sub-SELECT consente di filtrare i membri mentre e mantenere i totali veri anziché i totali filtrati. In tal modo è possibile eseguire una query per le prime dieci vendite (persone/prodotti/aree) e ottenere il totale vero delle vendite per tutti i membri inclusi nella query, anziché il valore totale delle vendite dei primi dieci restituiti. Per ulteriori informazioni, vedere gli esempi seguenti.  
  
 I membri calcolati possono essere \<inclusi nella clausola SELECT query Axis > ogni volta che la connessione è stata aperta utilizzando il parametro della stringa di connessione *sottoquery = 1*; vedere le [ &#40;proprietà XMLA supportate XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>per l'utilizzo dei parametri. Un esempio è fornito sui membri calcolati nelle sub-SELECT.  
  
## <a name="autoexists"></a>Auto Exist  
 Quando in un'istruzione SELECT vengono utilizzati due o più attributi della dimensione, Analysis Services valuta le espressioni degli attributi per verificare che i relativi membri siano correttamente limitati per soddisfare i criteri di tutti gli altri attributi. Si supponga ad esempio di utilizzare gli attributi della dimensione Geografia. Se una delle espressioni restituisce tutti i membri dell'attributo Città e un'altra limita i membri dell'attributo Paese a tutti i paesi europei, allora i membri di Città saranno limitati alle sole città che appartengono a paesi europei. Questa caratteristica di Analysis Services, denominata Auto Exist, si applica solo agli attributi della stessa dimensione, un quanto tenta di impedire che i record di dimensioni esclusi nell'espressione di un attributo vengano inclusi dalle espressioni di altri attributi. La caratteristica Auto Exist può inoltre essere interpretata come l'intersezione risultante da diverse espressioni di attributi su record di dimensioni. Vedere gli esempi seguenti:  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0,04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$ 0,00**|**0,00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0,04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$ 0,00**|**0,00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 Negli esempi precedenti sono stati creati due set, uno come espressione calcolata e l'altro come espressione costante. In questi esempi vengono illustrate le versioni diverse di Auto Exist.  
  
 La caratteristica Auto Exist può essere applicata in modo completo o superficiale alle espressioni. Per impostazione predefinita viene applicata in modo completo, come illustrato nell'esempio seguente. Nell'esempio si filtra Top10SellingProducts in base all'attributo [Product].[Product Line] per i membri del gruppo [Mountain]. Si noti che entrambi gli attributi (sezionamento e asse) appartengono alla stessa dimensione, [Product].  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1.62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0.05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0.05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0,04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2.56%**|  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 Nei risultati precedenti il sezionamento fornisce un risultato che contiene solo i prodotti dell'elenco Preferred10Products che fanno parte del gruppo [Mountain] in [Product].[Product Line], come previsto, in quanto Preferred10Products è un'espressione costante.  
  
 Questo set di risultati viene interpretato anche come Auto Exist superficiale, in quanto l'espressione viene valutata prima della clausola di sezionamento. Nell'esempio precedente, l'espressione è un'espressione costante a scopo illustrativo, al fine di presentare il concetto.  
  
 Il comportamento di Auto Exist può essere modificato a livello di sessione usando la proprietà della stringa di connessione **Autoexists** . L'esempio seguente inizia con l'apertura di una nuova sessione e l'aggiunta della proprietà *Autoexists=3* alla stringa di connessione. Per eseguire l'esempio, è necessario aprire una nuova connessione. Una volta stabilita la connessione con l'impostazione Auto Exist, quest'ultima rimarrà effettiva fino al termine della connessione.  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 Il comportamento di Auto Exist può essere modificato utilizzando il parametro auto EXISTs = [1 | 2 | 3] nella stringa di connessione. vedere [proprietà &#40;XMLA supportate XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> per l'utilizzo dei parametri.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la somma `Measures.[Order Quantity]` del membro, aggregata nei primi otto mesi dell'anno di calendario 2003 contenuti `Date` nella dimensione, dal cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 Per comprendere l'assenza di oggetti **visivi,** l'esempio seguente è una query di [Adventure Works] per ottenere le cifre di [Reseller Sales Amount] in una tabella in cui le categorie dei prodotti sono le colonne e i tipi di attività dei rivenditori sono le righe. I totali vengono forniti per sia i prodotti che per i rivenditori.  
  
 L'istruzione SELECT seguente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 Per produrre una tabella solo con i dati per i prodotti Accessories e Clothing, i rivenditori Value Added Reseller e Warehouse, conservando tuttavia i totali complessivi, si potrebbe scrivere una query come la seguente utilizzando NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce i risultati seguenti:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 Per produrre una tabella che visivamente somma le colonne, ma per i totali delle righe riporta il totale vero di [Category], immettere la query seguente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Notare come NON VISUAL è applicato solo a [Category].  
  
 La query precedente produce i seguenti risultati:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Se si confrontano i risultati precedenti, è possibile osservare che la riga [All Resellers] si aggiunge ai valori visualizzati di [Value Added Reseller] e [Warehouse] ma che la colonna [All Products] mostra il valore totale per tutti i prodotti, compresi quelli non visualizzati.  
  
 Nell'esempio seguente viene dimostrato come si utilizzano i membri calcolati nelle sub-SELECT per filtrarli. Per poter riprodurre questo esempio, la connessione deve essere stabilita utilizzando il parametro della stringa di connessione *sottoquery = 1*.  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 La query precedente produce i seguenti risultati:  
  
|||||  
|-|-|-|-|  
|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|Reseller Gross Profit Margin|  
|$80,450,596.98|$79,980,114.38|$470,482.60|0.58%|  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [MDX istruzioni &#40;di manipolazione dei dati MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Restrizione della query con gli assi &#40;di query e di sezionamento MDX&#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

