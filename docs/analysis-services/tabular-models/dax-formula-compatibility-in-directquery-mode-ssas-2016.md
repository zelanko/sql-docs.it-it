---
title: Compatibilità delle formule DAX in modalità DirectQuery di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e3a9a9f8043a3251e928b7b13e706b407097894
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072718"
---
# <a name="dax-formula-compatibility-in-directquery-mode"></a>Compatibilità delle formule DAX in modalità DirectQuery 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Per i modelli 1200 e versioni successive in modalità DirectQuery, molte limitazioni funzionale nelle versioni precedenti non sono più valide. In particolare, per quanto riguarda le formule DAX:

- DirectQuery genera ora query più semplici, con un significativo miglioramento delle prestazioni.
- Sicurezza a livello di riga (RLS) è ora supportata in modalità DirectQuery.
- Le colonne calcolate sono ora supportate per i modelli tabulari in modalità DirectQuery.

## <a name="dax-functions-in-directquery-mode"></a>Funzioni DAX in modalità DirectQuery

In breve, tutte le funzioni DAX sono supportate per i modelli DirectQuery. Tuttavia, non tutte le funzioni sono supportate per tutti i tipi di formula e non tutte le funzioni sono state ottimizzate per i modelli DirectQuery. A livello di base, è possibile dividere le funzioni DAX in due categorie: Ottimizzati e Non ottimizzata. Di seguito vengono descritte le funzioni ottimizzate.


### <a name="optimized-for-directquery"></a>Funzioni ottimizzate per DirectQuery
Si tratta di funzioni che restituiscono principalmente risultati scalari o aggregati. Queste funzioni si dividono in due gruppi: quelle supportate in tutti i tipi di formule, ovvero formule di misura, query, colonne calcolate e sicurezza a livello di riga, e quelle che sono supportate soltanto nelle formule di misura e query. tra cui:    

| Supportate in tutte le formule DAX                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Supportate soltanto nelle formule di misura e query                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ABS</br>  ACOS</br>  ACOT</br>  AND</br>  ASIN</br>  ATAN</br>  BLANK</br>  CEILING</br>  CONCATENATE</br>  COS</br>  COT</br>  CURRENCY</br>  DATE</br>  DATEDIFF</br>  DATEVALUE</br>  DAY</br>  DEGREES</br>  Divisione</br>  EDATE</br>  EOMONTH</br>  EXACT</br>  EXP</br>  FALSE</br>  FIND</br>  HOUR</br>  IF</br>  INT</br>  ISBLANK</br>  ISO.CEILING</br>  KEEPFILTERS</br>  LEFT</br>  LEN</br>  LN</br>  LOG</br>  LOG10</br>  LOWER</br>  MAX</br>  MID</br>  MIN</br>  MINUTE</br>  MOD</br>  MONTH</br>  MROUND</br>  NOT</br>  NOW</br>  o</br>  PI</br>  POWER</br>  QUOTIENT</br>  RADIANS</br>  RAND</br>  RELATED</br>  REPT</br>  RIGHT</br>  ROUND</br>  ROUNDDOWN</br>  ROUNDUP</br>  SEARCH</br>  SECOND</br>  SIGN</br>  SIN</br>  SQRT</br>  SQRTPI</br>  SUBSTITUTE</br>  SWITCH</br>  TAN</br>  TIME</br>  TIMEVALUE</br>  TODAY</br>  TRIM</br>  TRUE</br>  TRUNC</br>  UNICODE</br>  UPPER</br>  USERNAME</br>  USERELATIONSHIP</br>  Value</br>  WEEKDAY</br>  WEEKNUM</br>  YEAR</br> | ALL</br> ALLEXCEPT</br> ALLNOBLANKROW</br> ALLSELECTED</br> AVERAGE</br> AVERAGEA</br> AVERAGEX</br> CALCULATE</br> CALCULATETABLE</br> COUNT</br> COUNTA</br> COUNTAX</br> COUNTROWS</br> COUNTX</br> DISTINCT</br> DISTINCTCOUNT</br> FILTER</br> FILTERS</br> HASONEFILTER</br> HASONEVALUE</br> ISCROSSFILTERED</br> ISFILTERED</br> MAXA</br> MAXX</br> MIN</br> MINA</br> MINX</br> RELATEDTABLE</br> STDEV.P</br> STDEV.S</br> STDEVX.P</br> STDEVX.S</br> SUM</br> SUMX</br> VALUES</br> VAR.P</br> VAR.S</br> VARX.P</br> VARX.S |



### <a name="non-optimized-for-directquery"></a>Funzioni non ottimizzate per DirectQuery
Queste funzioni non sono state ottimizzate per l'uso con DirectQuery. Queste funzioni *non* sono supportate nelle formule di colonna calcolata e sicurezza a livello di riga. Queste funzioni, tuttavia, *sono supportate* nelle formule di misura e query, anche se con prestazioni incerte.

 In questo articolo non viene fornito l'elenco di tutte queste funzioni. In sostanza, se una funzione non è inclusa nell'elenco delle funzioni ottimizzate riportato sopra, significa che si tratta di una funzione non ottimizzata per DirectQuery.

Il motivo per cui è possibile che una particolare funzione non sia ottimizzata per DirectQuery risiede nel fatto che il motore relazionale sottostante non è in grado di eseguire calcoli equivalenti a quelli eseguiti dal motore xVelocity oppure che la formula non può essere convertita in un'espressione SQL equivalente. In altri casi, le prestazioni dell'espressione convertita e i calcoli risultanti potrebbero essere inaccettabili.

Per informazioni su tutte le funzioni DAX, vedere il [riferimento alle funzioni DAX]. (https://msdn.microsoft.com/library/ee634396.aspx)

## <a name="dax-operators-in-directquery-mode"></a>Operatori DAX in modalità DirectQuery
Tutti gli operatori di confronto e aritmetici DAX sono completamente supportati nella modalità DirectQuery. Per altre informazioni, vedere [Guida di riferimento agli operatori DAX](https://msdn.microsoft.com/library/ee634237.aspx).


 
## <a name="differences-between-in-memory-and-directquery-mode"></a>Differenze tra la modalità in memoria e la modalità DirectQuery  
Le query eseguite su un modello distribuito nella modalità DirectQuery possono restituire risultati differenti se eseguite sullo stesso modello distribuito nella modalità in memoria. Questo si verifica perché con DirectQuery i dati vengono recuperati direttamente da un archivio dati relazionale e le aggregazioni richieste dalle formule vengono eseguite usando il motore relazionale pertinente (SQL, Oracle, Teradata) anziché il motore di analisi in memoria xVelocity per l'archiviazione e il calcolo.  
  
Ad esempio, esistono differenze nel modo in cui alcuni archivi dati relazionali gestiscono i valori numerici, le date, i valori Null e così via.  
  
Al contrario, il linguaggio DAX deve emulare il più possibile il comportamento delle funzioni di Microsoft Excel. Ad esempio, per gestire valori Null, stringhe vuote e valori zero, Excel tenta di fornire la risposta migliore, a prescindere dal tipo di dati preciso, di conseguenza anche il motore xVelocity terrà lo stesso comportamento. Tuttavia, quando un modello tabulare viene distribuito nella modalità DirectQuery e le formule vengono passate a un'origine dati relazionale, i dati devono essere gestiti in base alla semantica dell'origine dati relazionale che in genere prevede una gestione separata delle stringhe vuote rispetto a quelle null. Per questo motivo, la stessa formula potrebbe restituire un risultato diverso se valutata rispetto ai dati memorizzati nella cache e rispetto ai dati restituiti solo dall'archivio relazionale.  
  
Inoltre, alcune funzioni non sono ottimizzate per la modalità DirectQuery perché il calcolo richiederebbe l'invio dei dati presenti nel contesto corrente all'origine dati relazionale sotto forma di parametri. Può trattarsi, ad esempio, di misure che usano funzioni di Business Intelligence per le gerarchie temporali che fanno riferimento a intervalli di date riportati in una tabella di tipo calendario. Un'origine dati relazionale può non disporre di una tabella di tipo calendario, o almeno di una con .  
  
## <a name="semantic-differences"></a>Differenze semantiche  
In questa sezione sono elencati i tipi di differenze semantiche che potrebbero verificarsi e vengono descritte le limitazioni che potrebbero applicarsi all'utilizzo di funzioni o ai risultati delle query.  
  
### <a name="comparisons"></a>Confronti  
Il linguaggio DAX nei modelli in memoria supporta i confronti di due espressioni risolvibili in valori scalari di tipi di dati diversi. Tuttavia, i modelli distribuiti nella modalità DirectQuery utilizzano i tipi di dati e gli operatori di confronto del motore relazionale, pertanto potrebbero restituire risultati diversi.  
  
I confronti seguenti restituiscono sempre un errore quando vengono usati in un calcolo su un'origine dati DirectQuery:  
  
-   Tipo di dati numerico confrontato a un qualsiasi tipo di dati stringa  
  
-   Tipo di dati numerico confrontato a un valore booleano  
  
-   Qualsiasi tipo di dati stringa confrontato a un valore booleano  
  
In generale, il linguaggio DAX tollera meglio le mancate corrispondenze tra tipi di dati nei modelli in memoria e tenta fino a due volte un cast implicito dei valori, come descritto in questa sezione. Tuttavia, le formule inviate a un archivio dati relazionale in modalità DirectQuery vengono valutate in modo più rigoroso, in base alle regole del motore relazionale ed è più probabile che abbiano esito negativo.  
  
**Confronti tra stringhe e numeri**  
ESEMPIO: `"2" < 3`  
  
La formula confronta una stringa di testo a un numero. L'espressione è **true** sia in modalità DirectQuery sia nei modelli in memoria.  
  
In un modello in memoria, il risultato è **true** perché viene eseguito il cast implicito dei numeri come stringhe a un tipo di dati numerico per confronti con altri numeri. SQL prevede inoltre il cast implicito di numeri di testo come numeri per il confronto con tipi di dati numerici.  
  
Si noti che questo rappresenta un cambiamento nel comportamento rispetto alla prima versione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], che restituirebbe **false**, in quanto il testo "2" sarebbe stato considerato maggiore di qualsiasi numero.  
  
**Confronto tra valori di testo e valori booleani**  
ESEMPIO: `"VERDADERO" = TRUE`  
  
Questa espressione confronta una stringa di testo a un valore booleano. In generale, per i modelli DirectQuery o in memoria, il confronto tra un valore stringa e un valore booleano genera un errore. Le uniche eccezioni alla regola si hanno quando la stringa contiene la parola **true** o **false**; se la stringa contiene valori true o false, viene convertita in valore booleano e il confronto restituisce il risultato logico.  
  
**Confronto tra valori Null**  
ESEMPIO: `EVALUATE ROW("X", BLANK() = BLANK())`  
  
Questa formula confronta l'equivalente SQL di un valore Null a un valore Null. Restituisce **true** nei modelli in memoria e DirectQuery; nel modello DirectQuery un provisioning garantisce un comportamento simile al modello in memoria.  
  
Si noti che in Transact-SQL un valore Null non è mai uguale a un valore Null. Tuttavia, nel linguaggio DAX uno spazio vuoto è uguale a un altro spazio vuoto. Questo comportamento rimane invariato per tutti i modelli in memoria. È importante notare che la modalità DirectQuery utilizza la maggior parte della semantica di SQL Server, anche se in questo caso si distingue fornendo un nuovo comportamento per i confronti NULL.  
  
### <a name="casts"></a>Cast  
  
Il linguaggio DAX non prevede alcuna funzione cast di questo tipo, tuttavia i cast impliciti vengono eseguiti in molte operazioni aritmetiche e di confronto. È l'operazione aritmetica o di confronto a determinare il tipo di dati del risultato. Ad esempio,  
  
-   I valori booleani vengono trattati come valori numerici nelle operazioni aritmetiche, ad esempio TRUE + 1 o la funzione MIN applicata a una colonna di valori booleani. Anche un'operazione NOT restituisce un valore numerico.  
  
-   I valori booleani vengono sempre trattati come valori logici nei confronti e quando vengono usati con EXACT, AND, OR, &amp;&amp;o ||.  
  
**Cast di una stringa a un valore booleano**  
In memoria e i modelli DirectQuery, i cast sono consentiti per i valori booleani solo di queste stringhe: **""** (stringa vuota), **"true"**, **"false"**; in una stringa vuota cast a un valore false.  
  
Il cast a un tipo di dati booleano di qualsiasi altra stringa genera un errore.  
  
**Cast da stringa a data/ora**  
Nella modalità DirectQuery i cast da rappresentazioni stringa di date e ore a valori **datetime** effettivi si comportano come in SQL Server.   
  
I modelli che utilizzano l'archivio dati in memoria supportano una gamma più limitata di formati di testo per le date rispetto ai formati stringa per date supportati in SQL Server. Tuttavia, il linguaggio DAX supporta formati data e ora personalizzati.  
  
**Cast da stringa ad altri valori non booleani**  
In caso di cast da stringhe a valori non booleani, la modalità DirectQuery si comporta come SQL Server. Per altre informazioni, vedere [CAST e CONVERT (Transact-SQL)](http://msdn.microsoft.com/a87d0850-c670-4720-9ad5-6f5a22343ea8).  
  
**Cast da numeri a stringa non consentito**  
ESEMPIO: `CONCATENATE(102,",345")`  
  
Il cast da numeri a stringhe non è consentito in SQL Server.  
  
Questa formula restituisce un errore nei modelli tabulari e nella modalità DirectQuery, ma produce un risultato in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
**Cast a due tentativi non supportato in DirectQuery**  
I modelli in memoria spesso tentano un secondo cast se il primo ha esito negativo. Questo non si verifica mai nella modalità DirectQuery.  
  
ESEMPIO: `TODAY() + "13:14:15"`  
  
In questa espressione il primo parametro presenta il tipo **datetime** e il secondo il tipo **string**. Tuttavia, quando gli operandi vengono combinati i cast vengono gestiti in modo diverso. Il linguaggio DAX esegue un cast implicito da **string** a **double**. Nei modelli in memoria il motore delle formule tenta di eseguire il cast direttamente a **double**e, se ha esito negativo, tenta di eseguire il cast della stringa a **datetime**.  
  
Nella modalità DirectQuery verrà applicato solo il cast diretto da **string** a **double** . Se questo cast ha esito negativo, la formula restituisce un errore.  
  
### <a name="math-functions-and-arithmetic-operations"></a>Funzioni matematiche e operazioni aritmetiche  
Alcune funzioni matematiche restituiscono risultati diversi nella modalità DirectQuery a causa delle differenze nel tipo di dati sottostante o nei cast che possono essere applicati nelle operazioni. Inoltre, le limitazioni descritte in precedenza sull'intervallo di valori consentito potrebbero influire sul risultato delle operazioni aritmetiche.  
  
**Ordine di addizione**  
Quando si crea una formula per aggiungere una serie di numeri, un modello in memoria potrebbe elaborare i numeri in un ordine diverso rispetto a un modello DirectQuery.  Di conseguenza, quando si dispone di molti numeri positivi elevati e di numeri negativi molto elevati, è possibile che un'operazione restituisca un errore e un'altra dei risultati.  
  
**Utilizzo della funzione POWER**  
ESEMPIO: `POWER(-64, 1/3)`  
  
Nella modalità DirectQuery la funzione POWER non può utilizzare valori negativi come base se viene elevata a un esponente frazionario. Si tratta del comportamento previsto in SQL Server.  
  
In un modello in memoria la formula restituisce -4.  
  
**Operazioni di overflow numerico**  
In Transact-SQL le operazioni che generano un overflow numerico restituiscono un errore di overflow. Di conseguenza, le formule che generano un overflow restituiscono un errore nella modalità DirectQuery.  
  
Tuttavia, la stessa formula, se utilizzata in un modello in memoria, restituisce un numero intero a otto byte perché il motore delle formule non esegue i controlli per gli overflow numerici.  
  
**Le funzioni LOG con spazi vuoti restituiscono risultati diversi**  
SQL Server gestisce i valori Null e gli spazi vuoti in modo diverso rispetto al motore xVelocity. Di conseguenza, la formula seguente restituisce un errore nella modalità DirectQuery, ma infinito restituito (-inf) in modalità in memoria.  
  
`EXAMPLE: LOG(blank())`  
  
Le stesse limitazioni si applicano alle altre funzioni logaritmiche: LOG10 e LN.  
  
Per altre informazioni sul tipo di dati **blank** in DAX, vedere [Specifica della sintassi DAX per PowerPivot](https://msdn.microsoft.com/library/ee634217.aspx).  
  
**Divisione per 0 e divisione per spazio vuoto**  
Nella modalità DirectQuery la divisione per zero (0) o per BLANK genera sempre un errore. SQL Server non supporta la nozione di infinito e poiché il risultato naturale di qualsiasi divisione per 0 è un infinito, il risultato è un errore. Tuttavia, SQL Server supporta la divisione per valori Null e il risultato deve sempre essere uguale a Null.  
  
Anziché restituire risultati diversi per queste operazioni, nella modalità DirectQuery entrambi i tipi di operazioni (divisione per zero e divisione per valore Null) restituiscono un errore.  
  
Si noti che anche nei modelli di Excel e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] la divisione per zero restituisce un errore. La divisione per spazio vuoto restituisce uno spazio vuoto.  
  
Le espressioni seguenti sono tutte valide nei modelli in memoria, ma generano un errore nella modalità DirectQuery:  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
L'espressione `BLANK/BLANK` è un caso speciale che restituisce `BLANK` sia per i modelli in memoria sia per quelli in modalità DirectQuery.  
  
### <a name="supported-numeric-and-date-time-ranges"></a>Intervalli numerici e data e ora supportati  
Le formule nei modelli tabulari in memoria sono soggette alle stesse limitazioni di Excel rispetto ai valori massimi consentiti per i numeri reali e le date. Possono tuttavia sorgere delle differenze quando il valore massimo viene restituito da un calcolo o da una query o quando si esegue la conversione, il cast, l'arrotondamento o il troncamento di valori.  
  
-   Se valori dei tipi **Currency** e **Real** vengono moltiplicati e il risultato è maggiore del valore massimo possibile, nella modalità DirectQuery non viene generato alcun errore e viene restituito un valore Null.  
  
-   Nei modelli in memoria non viene generato alcun errore, ma viene restituito il valore massimo.  
  
In generale, poiché gli intervalli di date accettati sono diversi per Excel e SQL Server, i risultati corrisponderanno solo quando le date rientrano nell'intervallo di date comune che include le date seguenti:  
  
-   Data meno recente: 1 marzo 1990  
  
-   Data più recente: 31 dicembre 9999  
  
Se alcune date utilizzate nelle formule non rientrano in questo intervallo, la formula genererà un errore oppure i risultati non corrisponderanno.  
  
**Valori a virgola mobile supportati da CEILING**  
ESEMPIO: `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
L'equivalente Transact-SQL della funzione DAX CEILING supporta unicamente i valori con grandezza pari a 10^19 o inferiore. La regola pratica è che i valori a virgola mobile devono rientrare in **bigint**.  
  
**Funzioni Datepart con date esterne all'intervallo**  
Nella modalità DirectQuery i risultati corrisponderanno a quelli nei modelli in memoria solo quando la data utilizzata come argomento rientra nell'intervallo di date valido. Se queste condizioni non vengono soddisfatte, viene generato un errore oppure la formula restituisce risultati diversi in DirectQuery rispetto alla modalità in memoria.  
  
ESEMPIO: `MONTH(0)` o `YEAR(0)`  
  
Nella modalità DirectQuery le espressioni restituiscono rispettivamente 12 e 1899.  
  
Nei modelli in memoria le espressioni restituiscono rispettivamente 1 e 1900.  
  
ESEMPIO:  `EOMONTH(0.0001, 1)`  
  
I risultati di questa espressione corrisponderanno solo quando i dati forniti come parametri rientrano nell'intervallo di date valido.  
  
ESEMPIO: `EOMONTH(blank(), blank())` o `EDATE(blank(), blank())`  
  
I risultati di questa espressione devono essere gli stessi sia nella modalità DirectQuery sia nella modalità in memoria.  
  
**Troncamento di valori ora**  
ESEMPIO: `SECOND(1231.04097222222)`  
  
Nella modalità DirectQuery il risultato viene troncato in base alle regole di SQL Server e l'espressione restituisce 59.  
  
Nei modelli in memoria i risultati di ogni operazione provvisoria vengono arrotondati. Di conseguenza, l'espressione restituisce 0.  
  
Nell'esempio seguente viene illustrata la modalità di calcolo di questo valore:  
  
1.  La frazione dell'input (0,04097222222) viene moltiplicata per 24.  
  
2.  Il valore ora risultante (0,98333333328) viene moltiplicato per 60.  
  
3.  Il valore minuti risultante è 58,9999999968.  
  
4.  La frazione del valore minuti (0,9999999968) viene moltiplicata per 60.  
  
5.  Il secondo valore risultante (59,999999808) viene arrotondato a 60.  
  
6.  60 equivale a 0.  
  
**Tipo di dati Time di SQL non supportato**  
I modelli in memoria non supportano l'uso del nuovo tipo di dati **Time** di SQL. Nella modalità DirectQuery le formule che fanno riferimento a colonne con questo tipo di dati restituiscono un errore. Le colonne di dati di tipo Time non possono essere importate in un modello in memoria.  
  
Tuttavia, il motore esegue talvolta il cast del valore Time a un tipo di dati accettabile e la formula restituisce un risultato.  
  
Questo comportamento influisce su tutte le funzioni che utilizzano una colonna di tipo date come parametro.  
  
### <a name="bkmk_Currency"></a>Currency  
Nella modalità DirectQuery, se il risultato di un'operazione aritmetica presenta il tipo **Currency**, il valore deve rientrare nell'intervallo seguente:  
  
-   Valore minimo: -922337203685477.5808  
  
-   Massima: 922337203685477.5807  
  
**Combinazione di tipi di dati REAL e currency**  
ESEMPIO: `Currency sample 1`  
  
Se i tipi **Currency** e **Real** vengono moltiplicati e il risultato è maggiore di 9223372036854774784 (0x7ffffffffffffc00), la modalità DirectQuery non genera alcun errore.  
  
In un modello in memoria viene generato un errore se il valore assoluto del risultato è maggiore di 922337203685477.4784.  
  
**L'operazione restituisce un valore non compreso nell'intervallo**  
ESEMPIO: `Currency sample 2`  
  
Se le operazioni eseguite su due valori valuta qualsiasi restituiscono un valore non compreso nell'intervallo specificato, viene generato un errore nei modelli in memoria, ma non nei modelli DirectQuery.  
  
**Combinazione del tipo di dati currency con altri tipi**  
La divisione di valori valuta per valori di altri tipi numerici può generare risultati diversi.  
  
### <a name="bkmk_Aggregations"></a>Funzioni di aggregazione  
Le funzioni statistiche eseguite su una tabella con una riga restituiscono risultati diversi. Le funzioni di aggregazione eseguite su tabelle vuote si comportano anch'esse in modo diverso nei modelli in memoria e nei modelli DirectQuery.  
  
**Funzioni statistiche eseguite su una tabella con una sola riga**  
Se la tabella usata come argomento contiene una sola riga, nella modalità DirectQuery funzioni statistiche quali STDEV e VARx restituiscono valori Null.  
  
In un modello in memoria, una formula che usa STDEV o VARx su una tabella con una sola riga restituisce un errore di divisione per zero.  
  
### <a name="bkmk_Text"></a>Funzioni di testo  
Poiché gli archivi dati relazionali forniscono tipi di dati di testo diversi rispetto a Excel, è possibile ottenere risultati diversi quando si eseguono ricerche nelle stringhe o si utilizzano sottostringhe. Anche la lunghezza delle stringhe può essere diversa.  
  
In generale, qualsiasi funzione di modifica delle stringhe che utilizza come argomenti colonne a dimensione fissa può restituire risultati diversi.  
  
Inoltre, in SQL Server alcune funzioni di testo supportano argomenti aggiuntivi non disponibili in Excel. Se la formula richiede l'argomento mancante, è possibile ottenere risultati o errori diversi nel modello in memoria.  
  
**È possibile che le operazioni che restituiscono un carattere utilizzando LEFT, RIGHT e così via restituiscano il carattere corretto, anche se con maiuscole/minuscole diverse, oppure nessun risultato.**  
ESEMPIO: `LEFT(["text"], 2)`  
  
Nella modalità DirectQuery le maiuscole/minuscole del carattere restituito corrispondono sempre esattamente a quelle della lettera archiviata nel database. Tuttavia, il motore xVelocity utilizza un algoritmo diverso per la compressione e l'indicizzazione di valori per migliorare le prestazioni.  
  
Per impostazione predefinita, vengono utilizzate le regole di confronto Latin1_General che non fanno distinzione tra maiuscole e minuscole, ma distinzione tra caratteri accentati e non. Di conseguenza, se sono presenti più istanze di una stringa di testo in caratteri minuscoli, maiuscoli o entrambi, tutte le istanze saranno considerate la stessa stringa e solo la prima istanza della stringa verrà archiviata nell'indice. Tutte le funzioni di testo eseguite su stringhe archiviate consentono di recuperare la porzione specificata della forma indicizzata. Di conseguenza, la formula di esempio restituisce lo stesso valore per l'intera colonna, utilizzando la prima istanza come input.  
  
Questo comportamento si applica anche ad altre funzioni di testo, incluse RIGHT, MID e così via.  
  
**La lunghezza della stringa influisce sui risultati**  
ESEMPIO: `SEARCH("within string", "sample target  text", 1, 1)`  
  
Se si cerca una stringa utilizzando la funzione SEARCH e la stringa di destinazione è più lunga della stringa che la contiene, viene generato un errore.  
  
In un modello in memoria viene restituita la stringa cercata, ma la sua lunghezza viene troncata alla lunghezza del &lt;testo che la contiene&gt;.  
  
ESEMPIO: `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
Se la lunghezza della stringa di sostituzione è maggiore della lunghezza della stringa originale, nella modalità DirectQuery la formula restituisce Null.  
  
Nei modelli in memoria la formula segue il comportamento di Excel che prevede il concatenamento della stringa di origine e della stringa di sostituzione, con restituzione del risultato CACalifornia.  
  
**Funzione TRIM implicita al centro delle stringhe**  
ESEMPIO: `TRIM(" A sample sentence with leading white space")`  
  
La modalità DirectQuery prevede la conversione della funzione DAX TRIM nell'istruzione SQL `LTRIM(RTRIM(<column>))`. Di conseguenza, vengono rimossi gli spazi vuoti iniziale e finale.  
  
Al contrario, in un modello in memoria la stessa formula prevede la rimozione degli spazi all'interno della stringa, in base al comportamento di Excel.  
  
**Funzione RTRIM implicita con utilizzo della funzione LEN**  
ESEMPIO: `LEN('string_column')`  
  
Analogamente a SQL Server, la modalità DirectQuery rimuove automaticamente lo spazio vuoto dalla fine delle colonne stringa, ovvero esegue una funzione RTRIM implicita. Di conseguenza, le formule che utilizzano la funzione LEN possono restituire valori diversi se la stringa contiene spazi finali.  
  
**In memoria supporta parametri aggiuntivi per SUBSTITUTE**  
ESEMPIO: `SUBSTITUTE([Title],"Doctor","Dr.")`  
  
ESEMPIO: `SUBSTITUTE([Title],"Doctor","Dr.", 2)`  
  
Nella modalità DirectQuery è possibile utilizzare solo la versione di questa funzione che dispone di tre (3) parametri: un riferimento a una colonna, il testo precedente e quello nuovo. Se si utilizza la seconda formula, viene generato un errore.  
  
Nei modelli in memoria è possibile utilizzare un quarto parametro facoltativo per specificare il numero di istanza della stringa da sostituire. Ad esempio, è possibile sostituire solo la seconda istanza e così via.  
  
**Limitazioni sulle lunghezze di stringa per le operazioni REPT**  
Nei modelli in memoria la lunghezza di una stringa risultante da un'operazione che utilizza REPT deve essere minore di 32.767 caratteri.  
  
Questa limitazione non è applicabile alla modalità DirectQuery.  
  
**Le operazioni di sottostringa restituiscono risultati diversi a seconda del tipo di carattere**  
ESEMPIO: `MID([col], 2, 5)`  
  
Se il testo di input è **varchar** o **nvarchar**, il risultato della formula è sempre lo stesso.  
  
Tuttavia, se il testo è un carattere a lunghezza fissa e il valore di *&lt;num_chars&gt;* è maggiore della lunghezza della stringa di destinazione, nella modalità DirectQuery viene aggiunto uno spazio vuoto alla fine della stringa risultato.  
  
In un modello in memoria il risultato termina in corrispondenza dell'ultimo carattere della stringa, senza riempimento.  


## <a name="see-also"></a>Vedere anche  
[Modalità DirectQuery](http://msdn.microsoft.com/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  


