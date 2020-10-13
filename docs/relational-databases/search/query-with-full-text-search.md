---
description: Esecuzione della query con ricerca Full-Text
title: Eseguire query con ricerca full-text | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c34b76e3712dceabf407fcece92f223bb97f1563
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867432"
---
# <a name="query-with-full-text-search"></a>Esecuzione della query con ricerca Full-Text
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Per scrivere query full-text, usare i predicati **CONTAINS** e **FREETEXT** e le funzioni valutate a livello dei set di righe **CONTAINSTABLE** e **FREETEXTTABLE** con l'istruzione **SELECT**. In questo articolo vengono presentati alcuni esempi di predicati e funzioni per consente di scegliere quelli più adatti.

-   Per trovare i valori corrispondenti a parole e frasi, usare **CONTAINS** e **CONTAINSTABLE**.
-   Per trovare i valori corrispondenti al significato, ma non all'esatta formulazione delle parole, usare **FREETEXT** e **FREETEXTTABLE** .

## <a name="examples-of-each-predicate-and-function"></a><a name="examples_simple"></a> Esempi di ogni predicato e funzione

Gli esempi seguenti usano il database di esempio AdventureWorks. Per la versione finale di AdventureWorks, vedere [AdventureWorks Databases and Scripts for SQL Server 2016 CTP3](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks) (Database e script di AdventureWorks per SQL Server 2016 CTP3). Per eseguire le query di esempio, è necessario impostare anche la ricerca full-text. Per altre informazioni, vedere [Introduzione alla ricerca full-text](get-started-with-full-text-search.md). 

### <a name="example---contains"></a>Esempio - CONTAINS  
L'esempio seguente trova tutti i prodotti con un prezzo di `$80.99` che contengono la parola `"Mountain"`:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
### <a name="example---freetext"></a>Esempio - FREETEXT 
 L'esempio seguente cerca tutti i documenti che contengono parole correlate a `vital safety components`:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>Esempio - CONTAINSTABLE  
 Nell'esempio seguente vengono restituiti l'ID della descrizione e la descrizione di tutti i prodotti per i quali la colonna **Description** contiene la parola "aluminum" accanto alla parola "light" o "lightweight". Vengono restituite solo le righe con un valore di pertinenza maggiore o uguale a 2.  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="example---freetexttable"></a>Esempio - FREETEXTTABLE  
 Nell'esempio seguente viene estesa una query FREETEXTTABLE in modo che vengano restituite per prime le righe con valore di pertinenza maggiore e che la classificazione di ogni riga venga aggiunta all'elenco di selezione. Per scrivere una query simile, è necessario sapere che **ProductDescriptionID** è la colonna chiave univoca per la tabella **ProductDescription** .  
  
```sql 
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
Di seguito è riportata un'estensione della stessa query che restituisce solo le righe con valore di pertinenza maggiore o uguale a 10:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  

## <a name="match-words-or-match-meaning"></a>Cercare la corrispondenza di parole o significato

`CONTAINS`/`CONTAINSTABLE` e `FREETEXT`/`FREETEXTTABLE` sono utili per vari tipi di corrispondenza. Le informazioni seguenti consentono di scegliere il predicato o la funzione più idonea per la query:

### <a name="containscontainstable"></a>CONTAINS/CONTAINSTABLE

-   Trova i valori corrispondenti di parole e frasi singole con un livello di corrispondenza esatto o fuzzy (meno preciso).
-   È anche possibile eseguire le operazioni seguenti:
    -   Specificare la prossimità delle parole all'interno di una certa distanza una dall'altra.
    -   Restituire corrispondenze ponderate.
    -   Combinare le condizioni di ricerca con gli operatori logici. Per altre informazioni, vedere [Uso di operatori booleani (AND, OR e NOT)](#Using_Boolean_Operators) più avanti in questo articolo.

### <a name="freetextfreetexttable"></a>FREETEXT/FREETEXTTABLE

-   Trova i valori corrispondenti al significato, ma non all'esatta formulazione, di parole, frasi o periodi specificati (*stringa free-text*).
-   Vengono generate corrispondenze se nell'indice full-text di una colonna specificata viene trovato un qualsiasi termine o formato di un qualsiasi termine.

## <a name="compare-predicates-and-functions"></a>Confrontare predicati e funzioni

I predicati `CONTAINS`/`FREETEXT` e le funzioni valutate a livello dei set di righe `CONTAINSTABLE`/`FREETEXTTABLE` hanno sintassi e opzioni diverse. Le informazioni seguenti consentono di scegliere il predicato o la funzione più idonea per la query:

### <a name="predicates-contains-and-freetext"></a>Predicati CONTAINS e FREETEXT

**Utilizzo**. Usare i **predicati** full-text CONTAINS e FREETEXT nella clausola WHERE o HAVING di un'istruzione SELECT.

**Risultati**. I predicati CONTAINS e FREETEXT restituiscono un valore TRUE o FALSE che indica se una determinata riga corrisponde alla query full-text. Le righe corrispondenti vengono restituite nel set di risultati.

**Altre opzioni**. È possibile combinare i predicati con altri predicati [!INCLUDE[tsql](../../includes/tsql-md.md)], ad esempio LIKE e BETWEEN.

È possibile specificare una sola colonna, un elenco di colonne o tutte le colonne della tabella in cui eseguire la ricerca.

Facoltativamente, è possibile specificare la lingua le cui risorse vengono usate dalla query full-text specificata per il word breaking e lo stemming, le ricerche nel thesaurus e la rimozione di parole non significative.

È possibile utilizzare un nome in quattro parti nel predicato CONTAINS o FREETEXT per eseguire query di colonne con indicizzazione full-text delle tabelle di destinazione in un server collegato. Per preparare un server remoto alla ricezione di query full-text, creare un indice full-text delle tabelle di destinazione e delle colonne nel server remoto, quindi aggiungere il server remoto come server collegato.

**Altre informazioni**. Per altre informazioni sulla sintassi e sugli argomenti di questi predicati, vedere [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md).

### <a name="rowset-valued-functions-containstable-and-freetexttable"></a>Funzioni valutate a livello dei set di righe CONTAINSTABLE e FREETEXTTABLE

**Utilizzo**. Usare le **funzioni** full-text CONTAINSTABLE e FREETEXTTABLE come un normale nome di tabella nella clausola FROM di un'istruzione SELECT.

È necessario specificare la tabella di base per la ricerca quando si usa una di queste funzioni. Come con i predicati, è possibile specificare una singola colonna, un elenco di colonne o tutte le colonne della tabella in cui eseguire la ricerca e, facoltativamente, la lingua le cui risorse vengono usate dalla query full-text specificata.

In genere, i risultati del predicato CONTAINSTABLE o FREETEXTTABLE devono essere uniti in join alla tabella di base. Per creare un join tra le tabelle, è necessario conoscere il nome della colonna chiave univoca. Questa colonna, presente in ogni tabella abilitata per la funzionalità full-text, viene usata per applicare righe univoche per la tabella (la *colonna chiave**univoca*). Per altre informazioni sulla colonna chiave, vedere [Creare e gestire indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md).

**Risultati**. Queste funzioni restituiscono una tabella di zero, una o più righe corrispondenti alla query full-text. La tabella restituita contiene solo righe della tabella di base che corrispondono ai criteri di selezione specificati nella condizione della ricerca full-text della funzione.

Le query che usano una di queste funzioni restituiscono un valore di classificazione per pertinenza (RANK) e una chiave full-text (KEY) per ogni riga restituita, come illustrato di seguito:

-   Colonna **KEY**. La colonna KEY restituisce valori univoci delle righe restituite. Può essere utilizzata per specificare i criteri di selezione.
-   Colonna **RANK**. La colonna RANK restituisce un *valore di pertinenza* per ogni riga che indica il livello di corrispondenza tra la riga e i criteri di selezione. Maggiore è il valore di pertinenza del testo o del documento in una riga, maggiore sarà la pertinenza della riga per una determinata query full-text. È possibile classificare in modo identico righe diverse. È possibile limitare il numero di corrispondenze da restituire specificando il parametro *top_n_by_rank* facoltativo. Per altre informazioni, vedere [Limitare i risultati della ricerca con RANK](../../relational-databases/search/limit-search-results-with-rank.md).

**Altre informazioni**. Per altre informazioni sulla sintassi e sugli argomenti di queste funzioni, vedere [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md).

## <a name="specific-types-of-searches"></a><a name="examples_specific"></a> Tipi di ricerca specifici

###  <a name="search-for-a-specific-word-or-phrase-simple-term"></a><a name="Simple_Term"></a> Ricerca di parole o frasi specifiche (termine semplice)  
 È possibile usare [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) per cercare una parola o frase specifica in una tabella. Ad esempio, per eseguire una ricerca nella tabella **ProductReview** del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] per trovare tutti i commenti su un prodotto con la frase "learning curve", è possibile usare il predicato CONTAINS nel modo seguente:  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
La condizione di ricerca, in questo caso "learning curve", può essere complessa ed essere costituita da uno o più termini.

#### <a name="more-info-about-simple-term-searches"></a>Altre informazioni sulle ricerche di termini semplici

Nella ricerca full-text una *parola* (o *token*) è una stringa i cui limiti vengono identificati da word breaker appropriati, in base alle regole linguistiche della lingua specificata. Una *frase* valida è costituita da più parole, separate o non separate da segni di punteggiatura.

Ad esempio, "croissant" è una parola, mentre "caffè macchiato" è una frase. Le parole e le frasi di questo tipo vengono definite termini semplici.

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) consentono di cercare una corrispondenza esatta per la frase. [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) consentono di suddividere la frase in parole separate.

###  <a name="search-for-a-word-with-a-prefix-prefix-term"></a><a name="Prefix_Term"></a> Ricerca di una parola con un prefisso (termine di prefisso)  
 È possibile usare [CONTAINS](../../t-sql/queries/contains-transact-sql.md) o [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) per cercare parole o frasi con un prefisso specificato. Vengono restituite tutte le voci nella colonna che contengono testo che inizia con il prefisso specificato. È possibile cercare, ad esempio, tutte le righe che contengono il prefisso `top`-, come in `top``ple`, `top``ping`e `top`. La query è simile all'esempio seguente:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 La query restituisce tutto il testo che corrisponde a quello specificato prima dell'asterisco (*). Se il testo e l'asterisco non sono delimitati da virgolette doppie, come in `CONTAINS (DESCRIPTION, 'top*')`, la ricerca full-text non considera l'asterisco un carattere jolly.  
  
 Se il termine di prefisso è una frase, ogni token che la compone viene considerato come un termine di prefisso distinto e vengono restituite tutte le righe contenenti parole che iniziano con tali prefissi. Ad esempio, il termine di prefisso "pennelli gialli\*" trova le righe che contengono il testo "pennelli giallini", "pennellini giallini" o "pennelli gialli", ma non "pennelli sottili gialli".

#### <a name="more-info-about-prefix-searches"></a>Altre informazioni sulle ricerche con prefisso

Un *termine di prefisso* fa riferimento a una stringa aggiunta davanti a una parola per produrre una parola derivata o una forma inflessa.

-   Per un singolo termine di prefisso, qualsiasi parola che inizia con il termine specificato farà parte del set di risultati. Ad esempio, il termine "auto*" corrisponde ad "automatico", "automobile" e così via.

-   Nel caso di una frase, ogni parola all'interno della frase viene considerata un termine di prefisso. Ad esempio, il termine "tras auto\*" corrisponde a "trasmissione automatica" e a "trasduttore automobile", ma non a "trasmissione motore automatica".

Le ricerche con prefisso sono supportate da [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md).
  
###  <a name="search-for-inflectional-forms-of-a-specific-word-generation-term"></a><a name="Inflectional_Generation_Term"></a> Ricerca di forme flessive di una parola specifica (termine di generazione)  
È possibile usare [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) per cercare tutti i diversi tempi e coniugazioni di un verbo o le forme sia singolare sia plurale di un sostantivo (ricerca di forme flessive) oppure i sinonimi di una parola specifica (ricerca thesaurus).  
  
Nell'esempio seguente vengono cercate tutte le forme del termine "piede" ("piede", "piedi" e così via) presenti nella colonna `Comments` della tabella `ProductReview` nel database `AdventureWorks`: 
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
Nella ricerca full-text vengono usati gli *stemmer*, che consentono di cercare i diversi tempi e coniugazioni di un verbo o le forme sia singolare sia plurale di un sostantivo. Per altre informazioni sui stemmer, vedere [Configurare e gestire word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  

#### <a name="more-info-about-generation-term-searches"></a>Altre informazioni sulle ricerche di termini di generazione

Le *forme flessive* sono costituite dai diversi tempi e coniugazioni di un verbo oppure dalle forme singolare e plurale di un sostantivo.

È possibile cercare, ad esempio, la forma flessiva della parola "guida". Se diverse righe della tabella contengono le parole "guida", "guide", "guidò", "guidando" e "guidato", tali parole vengono tutte incluse nel set di risultati, in quanto ognuna può essere generata in modo flessivo da "guida".

Per impostazione predefinita,[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) consentono di cercare le forme flessive di tutte le parole specificate. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) supportano un argomento `INFLECTIONAL` facoltativo.

### <a name="search-for-synonyms-of-a-specific-word"></a>Ricercare sinonimi di una parola specifica

Un *thesaurus* definisce i sinonimi specificati dall'utente per i termini. Per altre informazioni sui file del thesaurus, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).

Se viene aggiunta, ad esempio, una voce quale "{macchina, automobile, camion, furgone}" a un thesaurus, è possibile cercare la forma del thesaurus della parola "macchina". Il set di risultati includerà tutte le righe della tabella in cui viene eseguita la query che contengono le parole "automobile", "camion", "furgone" o "macchina", in quanto ognuna di queste parole appartiene al set di espansione dei sinonimi relativo alla parola "macchina".

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) il thesaurus per impostazione predefinita. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) supportano un argomento `THESAURUS` facoltativo.

### <a name="search-for-a-word-near-another-word"></a>Ricercare una parola vicina a un'altra parola

Un *termine di prossimità* indica parole o frasi vicine le une alle altre. È inoltre possibile specificare il numero massimo di termini non di ricerca che separano il primo e l'ultimo termine di ricerca. È inoltre possibile cercare parole o frasi in qualsiasi ordine o nell'ordine in cui sono state specificate.

È possibile, ad esempio, trovare le righe in cui la parola "ghiaccio" è vicina alla parola "hockey" o in cui la frase "pattinaggio su ghiaccio" è vicina alla frase "hockey su ghiaccio". 

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)

Per altre informazioni sulle ricerche di prossimità, vedere [Cercare parole vicine a un'altra parola con NEAR](search-for-words-close-to-another-word-with-near.md).

###  <a name="search-for-words-or-phrases-using-weighted-values-weighted-term"></a><a name="Weighted_Term"></a> Ricerca di parole o frasi tramite valori ponderati (termine ponderato)  
È possibile usare [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) per cercare parole o frasi e specificare un valore ponderato. Il peso, espresso come numero compreso tra 0,0 e 1,0, indica l'importanza di ogni parola o frase all'interno di un set di parole o frasi. Il valore 0,0 corrisponde al peso minimo, mentre il valore 1,0 corrisponde al peso massimo.  
  
Nell'esempio seguente viene illustrata una query per la ricerca di tutti gli indirizzi dei clienti, tramite valori di ponderazione, in cui il testo che inizia con la stringa "Bay" contiene anche la parola "Street" o "View". I risultati assegnano un livello di importanza superiore alle righe che contengono il numero maggiore di parole specificate.  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 È possibile utilizzare un termine ponderato insieme a qualsiasi termine semplice, termine di prefisso, termine di generazione o termine di prossimità.

#### <a name="more-info-about-weighted-term-searches"></a>Altre informazioni sulle ricerche di termini ponderati

In una ricerca d un termine ponderato, un *valore ponderato* indica il grado di importanza di ogni parola e frase all'interno di un set di parole e frasi. Il valore 0,0 corrisponde al peso minimo, mentre 1.0 corrisponde al peso massimo.

Ad esempio, in una query in cui vengono cercati più termini, è possibile assegnare a ogni parola un valore ponderato che ne indica l'importanza in relazione alle altre parole della condizione di ricerca. I risultati di questo tipo di query presentano prima le righe più rilevanti, in base al peso relativo assegnato alle parole della ricerca. I set di risultati includono documenti o righe contenenti alcuni dei termini specificati (o contenuto tra di essi). Alcuni risultati, tuttavia, verranno considerati più pertinenti di altri a causa della variazione nei valori ponderati associati a termini cercati diversi.

Le ricerche di termini ponderati sono supportate da [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md).

##  <a name="use-and-or-and-not-boolean-operators"></a><a name="Using_Boolean_Operators"></a> Usare AND, OR e NOT (operatori booleani)
 
Il predicato CONTAINS e la funzione CONTAINSTABLE utilizzano le stesse condizioni di ricerca. Entrambi supportano la combinazione di più termini di ricerca tramite gli operatori booleani AND, OR e NOT per eseguire operazioni logiche. È ad esempio possibile usare AND per trovare righe che contengono sia "latte" sia "New York-style bagel". È possibile usare AND NOT, ad esempio, per trovare le righe che contengono "bagel", ma non "cream cheese".  
  
Al contrario, FREETEXT e FREETEXTTABLE considerano i termini booleani come parole da cercare.  
  
 Per informazioni sulla combinazione di CONTAINS con altri predicati che usano gli operatori logici AND, OR e NOT, vedere [Condizione di ricerca &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
### <a name="example"></a>Esempio  
 L'esempio seguente usa il predicato CONTAINS per cercare le descrizioni il cui ID sia diverso da 5 e contenenti le parole "Aluminum" e "spindle". Nella condizione di ricerca viene utilizzato l'operatore booleano AND. In questo esempio viene usata la tabella ProductDescription del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
##  <a name="case-stopwords-language-and-thesaurus"></a><a name="Additional_Considerations"></a> Maiuscole e minuscole, parole non significative, lingua e thesaurus

 Quando si scrivono query full-text, è anche possibile specificare le opzioni seguenti:
  
-   **Distinzione maiuscole/minuscole**. Per le query di ricerca full-text non viene fatta distinzione tra maiuscole e minuscole. La lingua giapponese, tuttavia, prevede più forme fonetiche basate sul concetto di normalizzazione ortografica simile alla mancanza di distinzione tra maiuscole e minuscole, ad esempio kana = senza distinzione. Questo tipo di normalizzazione ortografica non è supportato.  

-   **Parole non significative**. Quando si definisce una query full-text, il motore di ricerca full-text ignora le parole non significative dai criteri di ricerca. Per parole non significative si intendono parole quali "circa", "con", "devo" e "cui" che possono ricorrere di frequente, ma che non hanno alcuna utilità nella ricerca di testo specifico. Le parole non significative vengono riunite in un elenco. Ogni indice full-text è associato a un elenco di parole non significative specifico per determinare quali di queste parole omettere dalla query o dall'indice durante l'indicizzazione. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  

-   **Lingua** con l'opzione **LANGUAGE**. Molti termini di query dipendono in larga misura dal comportamento del word breaker. Per assicurarsi di utilizzare il word breaker (e lo stemmer) e il thesaurus corretti, è consigliabile specificare l'opzione LANGUAGE. Per altre informazioni, vedere [Scelta di una lingua durante la creazione di un indice full-text](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
-   **Thesaurus**. Per impostazione predefinita, le query FREETEXT e FREETEXTTABLE utilizzano il thesaurus. CONTAINS e CONTAINSTABLE supportano un argomento THESAURUS facoltativo. Per altre informazioni, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](configure-and-manage-thesaurus-files-for-full-text-search.md).
  
##  <a name="check-the-tokenization-results"></a><a name="tokens"></a> Controllo dei risultati di tokenizzazione

Dopo aver applicato una determinata combinazione di word breaker, thesaurus ed elenco di parole non significative a una query, è possibile visualizzare il risultato della tokenizzazione della ricerca full-text usando la DMV **sys.dm_fts_parser**. Per altre informazioni, vedere [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Creare query di ricerca full-text &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-full-text-search-queries-visual-database-tools.md)   
 [Migliorare le prestazioni delle query full-text](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
