---
title: Limitare i risultati della ricerca mediante RANK | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ebb1f67a981396f1f7bb2026f66a528052b0e4df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011152"
---
# <a name="limit-search-results-with-rank"></a>Limitazione dei risultati della ricerca mediante RANK
  Le funzioni [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) restituiscono una colonna denominata RANK che contiene valori ordinali compresi tra 0 e 1000 (valori di classificazione). Questi valori vengono utilizzati per classificare le righe restituite in base al grado di corrispondenza con i criteri di selezione. I valori di pertinenza indicano solo un ordine relativo di pertinenza delle righe nel set di risultati, dove un valore inferiore indica una pertinenza inferiore. I valori effettivi sono senza importanza e in genere variano ogni volta che viene eseguita la query.  
  
> [!NOTE]  
>  I predicati CONTAINS e FREETEXT non restituiscono alcun valore di pertinenza.  
  
 Il numero di elementi corrispondenti a una condizione di ricerca è spesso molto elevato. Per evitare che le query CONTAINSTABLE o FREETEXTTABLE restituiscano un numero eccessivo di risultati, usare il parametro facoltativo *top_n_by_rank* che restituisce solo un subset di righe. *top_n_by_rank* è un numero intero, *n*, che specifica che dovranno essere restituite solo le *n* corrispondenze con la pertinenza più alta, in ordine discendente. Se il parametro *top_n_by_rank* viene combinato con altri parametri, la query potrebbe restituire un numero inferiore di righe rispetto al numero di righe effettivamente corrispondenti a tutti i predicati.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ordina le corrispondenze per pertinenza e restituisce solo il numero specificato di righe. Questa opzione può comportare un miglioramento significativo delle prestazioni. Una query che normalmente restituisce 100.000 righe di una tabella che contiene un milione di righe, ad esempio, viene elaborata più rapidamente se vengono richieste solo le prime 100 righe.  
  
##  <a name="examples"></a> Esempi di utilizzo di RANK per limitare i risultati della ricerca  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>Esempio A: Ricerca delle prime tre corrispondenze  
 Nell'esempio seguente viene utilizzato CONTAINSTABLE per restituire solo le prime tre corrispondenze.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>Esempio B: Ricerca delle prime dieci corrispondenze  
 Nell'esempio seguente viene utilizzato CONTAINSTABLE per restituire la descrizione dei primi 5 prodotti la cui colonna `Description` include la parola "aluminum" accanto alla parola "light" o "lightweight".  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> Classificazione per pertinenza dei risultati delle query di ricerca  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la ricerca full-text può generare un punteggio facoltativo (o valore di pertinenza) che indica la pertinenza dei dati restituiti da una query full-text. Questo valore di pertinenza viene calcolato in ogni riga e può essere utilizzato come criteri di ordinamento del set di risultati di una query basato sulla pertinenza. Il valore di pertinenza indica solo un ordine di pertinenza relativo delle righe nel set di risultati. I valori effettivi sono senza importanza e in genere variano ogni volta che viene eseguita la query. Il valore di pertinenza non mantiene alcun significato nelle query.  
  
### <a name="statistics-for-ranking"></a>Statistiche per il calcolo della pertinenza  
 Al momento della compilazione di un indice vengono raccolte statistiche per l'utilizzo nei calcolo della pertinenza. Il processo di compilazione di un catalogo full-text non conduce direttamente a una singola struttura di indice. Il motore di ricerca full-text per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , al contrario, crea indici intermedi man mano che i dati vengono indicizzati e successivamente unisce tali indici in un indice di dimensioni maggiori in base alle esigenze. Il processo può essere ripetuto più volte. Il motore di ricerca full-text SQL esegue infine un'unione nell'indice master per associare tutti gli indici intermedi in un indice master di dimensioni elevate.  
  
 Le statistiche vengono raccolte a ogni livello di indice intermedio. L'unione delle statistiche avviene contemporaneamente a quella degli indici. Alcuni valori statistici possono essere generati solo durante il processo di unione nell'indice master.  
  
 Nella classificazione di un set di risultati della query, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono utilizzate statistiche in base all'indice intermedio di dimensioni maggiori. Ciò varia a seconda che gli indici intermedi siano stati uniti o meno. Se gli indici intermedi non sono stati uniti, l'accuratezza delle statistiche per il calcolo della pertinenza può variare. Per questo motivo la stessa query può restituire nel tempo risultati di pertinenza diversi, man mano che i dati con indicizzazione full-text vengono aggiunti, modificati ed eliminati e vengono uniti gli indici più piccoli.  
  
 Per ridurre al minimo le dimensioni dell'indice e la complessità del calcolo, le statistiche vengono spesso arrotondate.  
  
 Nell'elenco seguente sono inclusi alcuni termini e valori statistici utilizzati di frequente e importanti per calcolare il valore di pertinenza:  
  
 Proprietà  
 Una colonna con indicizzazione full-text della riga.  
  
 Document  
 L'entità restituita nelle query. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] corrisponde a una riga. Un documento può disporre di più proprietà, esattamente come una riga può includere più colonne con indicizzazione full-text.  
  
 Indice  
 Un singolo indice invertito di uno o più documenti. Può essere contenuto completamente nella memoria o su disco. Molte statistiche di query riguardano l'indice specifico nel quale si è verificata la corrispondenza.  
  
 Catalogo full-text  
 Una raccolta di indici intermedi gestita come singola entità per le query. I cataloghi rappresentano l'unità di organizzazione visibile all'amministratore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Word, token o item  
 L'unità di corrispondenza del motore full-text. I flussi di testo dai documenti vengono suddivisi in parole o token da word breaker specifici della lingua.  
  
 Occorrenza  
 L'offset delle parole in una proprietà del documento, determinato dal word breaker. La prima parola corrisponde all'occorrenza 1, quella successiva all'occorrenza 2 e così via. Per evitare falsi positivi nelle query su frasi e di prossimità, indicatori di fine frase e indicatori di fine paragrafo introducono gap di occorrenza più grandi.  
  
 TermFrequency  
 Il numero di volte che il valore della chiave è presente in una riga.  
  
 IndexedRowCount  
 Il numero totale di righe indicizzate. Viene calcolato in base ai conteggi gestiti negli indici intermedi. L'accuratezza di questo numero può variare.  
  
 KeyRowCount  
 Il numero totale di righe nel catalogo full-text contenenti una chiave specifica.  
  
 MaxOccurrence  
 Il valore di occorrenza più grande archiviato in un catalogo full-text per una proprietà specifica di una riga.  
  
 MaxQueryRank  
 Il valore di pertinenza massimo, 1000, restituito dal motore di ricerca full-text.  
  
  
### <a name="rank-computation-issues"></a>Problemi nel calcolo della pertinenza  
 Il processo di calcolo della pertinenza dipende da alcuni fattori.  I word breaker delle diverse lingue suddividono il testo in token in modo diverso. La stringa "pick-up", ad esempio, potrebbe essere suddivisa in "pick" "up" da un word breaker e in "pick-up" da un altro. Ciò significa che la corrispondenza e il calcolo della pertinenza variano in base alla lingua specificata, poiché non solo le parole sono diverse, ma lo è anche la lunghezza dei documenti. La differenza di lunghezza dei documenti può influire sul calcolo della pertinenza per tutte le query.  
  
 Statistiche quali `IndexRowCount` possono variare notevolmente. Se, ad esempio, un catalogo presenta 2 miliardi di righe nell'indice master, un nuovo documento viene indicizzato in un indice intermedio in memoria e la pertinenza corrispondente basata sul numero di documenti dell'indice in memoria potrebbe essere asimmetrica rispetto alla pertinenza per i documenti dall'indice master. Per questo motivo, dopo ogni popolamento che determini l'indicizzazione o la reindicizzazione di un grande numero di righe è consigliabile unire gli indici in un indice master utilizzando l'istruzione ALTER FULLTEXT CATALOG ... Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] REORGANIZE. Il motore di ricerca full-text, inoltre, unirà automaticamente gli indici in base a parametri quali il numero e le dimensioni di indici intermedi.  
  
 I valori `MaxOccurrence` vengono normalizzati in 1 di 32 intervalli. Ciò significa, ad esempio, che un documento di 50 parole di lunghezza viene gestito come un documento di 100 parole. Di seguito viene riportata la tabella utilizzata per la normalizzazione. Poiché le lunghezze dei documenti rientrano nell'intervallo tra i valori di tabella adiacenti 32 e 128, vengono trattati in modo efficace con la stessa `docLength` lunghezza, 128 (32 < <= 128).  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>Calcolo della pertinenza di CONTAINSTABLE  
 Per il calcolo della pertinenza di[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) viene usato l'algoritmo seguente:  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 Il calcolo della pertinenza per le corrispondenze di frase è analogo a quello delle chiavi singole, tranne per il fatto che `KeyRowCount` (il numero di righe contenenti la frase) è il risultato di una stima e può essere impreciso e maggiore del numero effettivo.  
  
 **Calcolo della pertinenza di NEAR**  
  
 CONTAINSTABLE supporta l'esecuzione di query per due o più termini di ricerca prossimi l'uno all'altro tramite l'opzione NEAR. Il valore di pertinenza di ogni riga restituita è basato su diversi parametri. Un importante fattore di pertinenza è il numero complessivo di corrispondenze (o *riscontri*) in relazione alla lunghezza del documento. Pertanto se, ad esempio, un documento di 100 parole e un documento 900 parole contengono corrispondenze identiche, il documento di 100 parole avrà un valore di pertinenza più in alto.  
  
 La lunghezza totale di ogni riscontro in una riga contribuirà inoltre al calcolo della pertinenza di tale riga in base alla distanza tra i primo e l'ultimo termine di ricerca di tale riscontro. Minore è la distanza, maggiore sarà il contributo del riscontro al valore di pertinenza della riga. Se in una query full-text non viene specificato un valore intero come distanza massima, un documento che contiene solo riscontri le cui distanze sono maggiori di 100 termini logici avrà un valore di pertinenza pari a 0.  
  
 **Calcolo della pertinenza di ISABOUT**  
  
 CONTAINSTABLE consente di eseguire query per termini ponderati tramite l'opzione ISABOUT. ISABOUT è una query per lo spazio vettoriale nella terminologia tradizionale relativa al recupero delle informazioni. L'algoritmo predefinito per il calcolo della pertinenza è di tipo Jaccard, una formula molto nota. La pertinenza viene calcolata per ogni termine nella query, quindi combinata come descritto di seguito.  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = ??[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( ??[key=1 to n] ContainsRankKey^2 )   
      + ( ??[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>Calcolo della pertinenza di FREETEXTTABLE  
 Il calcolo della pertinenza di[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) si basa sulla formula OKAPI BM25. Le query FREETEXTTABLE aggiungono parole alla query tramite generazione flessiva (forme flesse delle parole della query originale). Queste parole vengono gestite separatamente, senza nessuna relazione particolare con le parole di origine. I sinonimi generati dal thesaurus vengono gestiti come termini separati, con lo stesso valore ponderato. Ogni parola nella query contribuisce alla pertinenza.  
  
```  
Rank = ??[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N - R + r + 0.5 ) ) / ( ( R - r + 0.5 ) * ( n - r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 - b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query con ricerca full-text](query-with-full-text-search.md)  
  
  
