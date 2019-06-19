---
title: Le sub-SELECT nelle query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c9fb5d1300b6f50f7ef0a765881896069becf0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073894"
---
# <a name="subselects-in-queries"></a>Sub-SELECT nelle query
  Le espressioni sub-SELECT sono espressioni SELECT nidificate utilizzate per limitare lo spazio del cubo dal quale viene valutata l'istruzione SELECT esterna. Le sub-SELECT consentono di definire un nuovo spazio sul quale tutti i calcoli vengono valutati.  
  
## <a name="subselects-by-example"></a>Esempio di sub-SELECT  
 Si inizia con un esempio di come le sub-SELECT possono consentire di produrre i risultati che si desidera mostrare. Si supponga che sia stato richiesto di produrre una tabella che mostri il comportamento delle vendite, durante gli anni, per i primi 10 prodotti.  
  
 Il risultato sarà simile a quello contenuto nella tabella seguente:  
  
|||||  
|-|-|-|-|  
||Somma degli anni|Anno 1|...|  
|Somma dei primi 10 prodotti||||  
|Prodotto A||||  
|...||||  
  
 Per eseguire un'operazione simile alla precedente, si potrebbe scrivere l'espressione MDX seguente:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 Vengono restituiti i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 20062|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 nero, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 nero, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 argento, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 nero, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 argento, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 argento, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 rosso, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 nero, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W giallo, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 Questo risultato è molto vicino a quello che si sta cercando, ma la query ha restituito 9 e non 10 prodotti e il totale di Tutti i prodotti riflette la somma di tutti i prodotti e non la somma dei primi 9 restituiti (in questo caso). Un altro tentativo di risolvere il problema viene presentato nella query MDX seguente:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 Vengono restituiti i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 nero, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 nero, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 argento, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 nero, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 argento, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 argento, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 rosso, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 nero, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W giallo, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 rosso, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 Questo risultato è molto vicino a quello desiderato perché manca solo la somma dei prodotti. In questa fase è possibile iniziare modificando l'espressione MDX precedente per aggiungere la riga mancante. Tuttavia, questa attività potrebbe rivelarsi complicata.  
  
 Un altro approccio per risolvere il problema sarebbe quello di ridefinire lo spazio del cubo sul quale l'espressione MDX viene risolta. Si supponga che il "nuovo" cubo contenga solo i dati dei primi 10 prodotti. In questo caso il membro Totale contenuto nel cubo verrà modificato in modo da includere solo i primi 10 prodotti e ora una semplice query soddisferebbe le nostre esigenze.  
  
 Nell'espressione MDX seguente viene utilizzata un'istruzione sub-SELECT per ridefinire lo spazio del cubo in base ai primi 10 prodotti e produrre i risultati desiderati:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Tramite l'espressione sopra indicata vengono restituiti i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 argento, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 argento, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 argento, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 nero, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 nero, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 nero, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 nero, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 rosso, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 rosso, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W giallo, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 I risultati precedenti sono esattamente quelli desiderati.  
  
 Di seguito vengono esaminate le operazioni eseguite dall'istruzione sub-SELECT. La sub-SELECT ha restituito un nuovo cubo che contiene tutte le altre dimensioni del prodotto così come sono. Nella dimensione del prodotto sono stati tuttavia filtrati tutti i membri in modo da farli corrispondere ai primi 10 prodotti a cui si è interessati. È come se fossero stati rimossi tutti i dati che non hanno soddisfatto i Primi 10 criteri e avevano ricostruito il cubo. L'altro concetto importante da capire in questo esempio è il fatto che i primi 10 prodotti sono stati calcolati sul membro Totale di tutte le altre dimensioni del cubo. L'affermazione precedente è vera perché non è stata imposta nessun'altra restrizione di filtro nella sub-SELECT.  
  
 Le sub-SELECT possono avere il livello di complessità desiderato. Nell'esempio seguente viene illustrato come produrre una tabella simile a quella menzionata sopra, ma filtrata sulla Francia per la dimensione Sales Territory (territorio di vendita) e su Internet per la dimensione Sales Channel (canale di vendita).  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Vengono prodotti i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 argento, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 argento, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 argento, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 nero, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 nero, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 nero, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 nero, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 rosso, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 rosso, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W giallo, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 I risultati sopra riportati sono i primi 10 prodotti venduti in Francia tramite il canale Internet.  
  
## <a name="subselect-statement"></a>Istruzione sub-SELECT  
 La notazione BNF per la sub-SELECT è:  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 La sub-SELECT è un'altra istruzione SELECT in cui le specifiche dell'asse e la specifica del sezionamento filtrano lo spazio del cubo sul quale viene valutata l'istruzione SELECT esterna.  
  
 Quando un membro viene specificato in una delle clausole dell'asse o di sezionamento, tale membro e i relativi predecessori e discendenti vengono inclusi nello spazio del sottocubo per la sub-SELECT. Tutti i membri di pari livello non menzionati nella clausola dell'asse o di sezionamento e i relativi discendenti vengono filtrati dal sottospazio. In tal modo lo spazio dell'istruzione SELECT esterna è stato limitato ai membri esistenti nella clausola dell'asse o nella clausola di sezionamento, con i relativi predecessori e discendenti come menzionato in precedenza.  
  
 Poiché il membro Totale di tutte le dimensioni non menzionate nelle clausole dell'asse o di sezionamento appartiene allo spazio dell'istruzione SELECT, anche tutti i discendenti del membro Totale su tali dimensioni fanno parte dello spazio della sub-SELECT.  
  
 Il membro Totale, in tutte le dimensioni, nello spazio del sottocubo viene rivalutato in modo da riflettere l'impatto dei vincoli del nuovo spazio.  
  
 Nell'esempio seguente viene mostrato quanto detto sopra. La prima espressione MDX consente di visualizzare i valori non filtrati nel cubo e nella seconda viene illustrato l'effetto del filtro nella clausola sub-SELECT:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 Restituisce i valori seguenti:  
  
||||  
|-|-|-|  
||Importo vendite Internet|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|United States|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 Nell'esempio precedente Seattle è un figlio di Washington, Portland è un figlio di Oregon, Oregon e Washington sono figli di Stati Uniti e Stati Uniti è un figlio di [Customer Geography].[All Customers]. Tutti i membri mostrati in questo esempio dispongono di altri elementi di pari livello che contribuiscono al valore aggregato padre, ovvero Spokane, Tacoma ed Everett sono città di pari livello di Seattle e contribuiscono all'importo vendite Internet di Washington. Il valore di Importo vendite venditore è indipendente dall'attributo Customer Geography (Dati geografici cliente), pertanto il valore Totale viene visualizzato nei risultati. L'espressione MDX successiva illustra l'effetto del filtro della clausola sub-SELECT:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 Restituisce i valori seguenti:  
  
||||  
|-|-|-|  
||Importo vendite Internet|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 I risultati precedenti mostrano che solo i predecessori e i discendenti dello Stato di Washington fanno parte del sottospazio in cui è stata valutata l'istruzione SELECT esterna. Oregon e Portland sono stati rimossi dal sottocubo perché Oregon e tutti gli altri stati di pari livello non sono stati menzionati nella sub-SELECT quando è stato menzionato Washington.  
  
 Il membro Totale è stato modificato in modo da riflettere l'applicazione del filtro su Washington. È stato modificato non solo nella dimensione [Customer Geography], ma in tutte le altre dimensioni incrociate con [Customer Geography]. Tutte le dimensioni che non si incrociano con [Customer Geography] restano inalterate nel sottocubo.  
  
 Le due istruzioni MDX seguenti illustrano come il membro Totale nelle altre dimensioni viene modificato per soddisfare l'effetto del filtro della sub-SELECT. La prima query visualizza i risultati inalterati e la seconda mostra l'impatto dell'applicazione del filtro:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessorio|Componenti|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|United States|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessorio|Componenti|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|United States|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 I risultati precedenti mostrano che i valori di Tutti i prodotti sono stati adattati solo ai valori dello Stato di Washington, come previsto.  
  
 Le sub-SELECT possono essere annidate senza limiti di profondità, compatibilmente con la memoria disponibile. La sub-SELECT più interna definisce il sottospazio iniziale sul quale il filtro viene applicato e passato alla SELECT esterna successiva. È importante notare il fatto che l'annidamento non è un'operazione commutativa, quindi l'ordine nel quale viene impostato potrebbe produrre risultati diversi. Negli esempi seguenti viene mostrata la differenza quando si sceglie un ordine di nidificazione.  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Vengono restituiti i risultati seguenti.  
  
||||||||  
|-|-|-|-|-|-|-|  
||Tutti i territori di vendita|Australia|Canada|Centro|Nord-ovest|Sud-ovest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 argento, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 nero, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 nero, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 nero, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 rosso, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Vengono restituiti i risultati seguenti.  
  
||||||||  
|-|-|-|-|-|-|-|  
||Tutti i territori di vendita|Australia|Canada|Nord-ovest|Sud-ovest|United Kingdom|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 argento, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 argento, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 nero, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 nero, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 nero, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 Come è possibile notare, ci sono differenze nei risultati in entrambi i set. La prima query ha risposto alla domanda sui prodotti più venduti nelle 5 aree principali, la seconda query ha risposto alla domanda sulle aree in cui si è verificato il maggior numero di vendite dei 5 prodotti più venduti.  
  
### <a name="remarks"></a>Note  
 Le sub-SELECT sono sottoposte alle restrizioni e limitazioni seguenti:  
  
-   La clausola WHERE non filtra il sottospazio.  
  
-   La clausola WHERE modifica solo il membro predefinito nel sottocubo.  
  
-   La clausola NON EMPTY non è consentita in una clausola dell'asse; usare invece un'espressione della funzione [NonEmpty &#40;MDX&#41;](/sql/mdx/nonempty-mdx).  
  
-   La clausola HAVING non è consentita in una clausola dell'asse; usare invece un'espressione della funzione [Filter &#40;MDX&#41;](/sql/mdx/filter-mdx) .  
  
-   Per impostazione predefinita i membri calcolati non sono consentiti nelle sub-SELECT; Tuttavia, questa restrizione può essere modificata, singola per ogni sessione, assegnando un valore per il `SubQueries` proprietà stringa di connessione <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> o `DBPROP_MSMD_SUBQUERIES` proprietà nel [proprietà XMLA supportate &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties). Visualizzare [membri calcolati in sub-SELECT e sottocubi](calculated-members-in-subselects-and-subcubes.md) per una spiegazione dettagliata del comportamento dei membri calcolati a seconda dei valori di `SubQueries` o `DBPROP_MSMD_SUBQUERIES`.  
  
  
