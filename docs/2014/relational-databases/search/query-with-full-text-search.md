---
title: Eseguire query con ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 244161359910896533a1d7179f2ce80b5cb03d86
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749425"
---
# <a name="query-with-full-text-search"></a>Esecuzione della query con ricerca Full-Text
  Per definire ricerche full-text, le query full-text in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano i predicati full-text (CONTAINS e FREETEXT) e le funzioni full-text (CONTAINSTABLE e FREETEXTTABLE). Tali predicati e funzioni supportano la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] avanzata che a sua volta supporta vari formati di termini di query. Per scrivere query full-text, è necessario sapere come e quando utilizzare questi predicati e queste funzioni.  
  
##  <a name="OV_ft_predicates"></a> Panoramica di Full-Text di predicati (CONTAINS e FREETEXT)  
 I predicati CONTAINS e FREETEXT restituiscono un valore TRUE o FALSE. Possono essere utilizzati solo per specificare i criteri di selezione per determinare se una determinata riga corrisponde alla query full-text. Le righe corrispondenti vengono restituite nel set di risultati. CONTAINS e FREETEXT vengono specificati nella clausola WHERE o HAVING di un'istruzione SELECT. Possono essere combinati con qualsiasi altro predicato [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio LIKE e BETWEEN.  
  
> [!NOTE]  
>  Per informazioni sulla sintassi e sugli argomenti di questi predicati, vedere [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql) e [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql).  
  
 Quando si utilizza CONTAINS o FREETEXT, è possibile specificare una sola colonna, un elenco di colonne o tutte le colonne della tabella in cui eseguire la ricerca. Facoltativamente, è possibile specificare la lingua le cui risorse verranno utilizzate dalla query full-text specificata per il word breaking e lo stemming, le ricerche nel thesaurus e la rimozione di parole non significative.  
  
 CONTAINS e FREETEXT sono utili per tipi diversi di corrispondenze, come illustrato di seguito:  
  
-   Utilizzare CONTAINS (o CONTAINSTABLE) per corrispondenze precise o fuzzy (meno precise) a singole parole e frasi, la prossimità di parole entro una certa distanza una dall'altra o corrispondenze ponderate. Quando si utilizza CONTAINS, è necessario specificare almeno una condizione di ricerca che specifichi il testo che si desidera cercare e le condizioni che determinano le corrispondenze.  
  
     È possibile utilizzare l'operazione logica tra condizioni di ricerca. Per altre informazioni, vedere [uso degli operatori booleani-AND, OR, AND NOT (in CONTAINS e CONTAINSTABLE)](#Using_Boolean_Operators), più avanti in questo argomento.  
  
-   Usare FREETEXT (o FREETEXTTABLE) per trovare la corrispondenza di significato, ma non l'esatta formulazione, di parole e frasi specificate (stringa *free-text*). Vengono generate corrispondenze se nell'indice full-text di una colonna specificata viene trovato un qualsiasi termine o formato di un qualsiasi termine.  
  
 È possibile utilizzare un nome in quattro parti nel predicato CONTAINS o FREETEXT per eseguire query di colonne con indicizzazione full-text delle tabelle di destinazione in un server collegato. Per preparare un server remoto alla ricezione di query full-text, creare un indice full-text delle tabelle di destinazione e delle colonne nel server remoto, quindi aggiungere il server remoto come server collegato.  
  
> [!NOTE]  
>  I predicati full-text non sono consentiti nella [clausola OUTPUT](/sql/t-sql/queries/output-clause-transact-sql) quando il livello di compatibilità del database è impostato su 100.  
  
 
  
### <a name="examples"></a>Esempi  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. Utilizzo di CONTAINS con <simple_term>  
 Nell'esempio seguente vengono trovati tutti i prodotti il cui prezzo è `$80.99` e contenenti la parola `"Mountain"`.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>b. Utilizzo di FREETEXT per la ricerca di parole contenenti valori di carattere specificati  
 Nell'esempio seguente viene eseguita la ricerca di tutti i documenti contenenti le parole associate a "vital", "safety" e "components".  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> Panoramica delle funzioni (CONTAINSTABLE e FREETEXTTABLE) Full-Text  
 È possibile fare riferimento alle funzioni CONTAINSTABLE e FREETEXTTABLE come un normale nome di tabella nella clausola FROM di un'istruzione SELECT. Restituiscono una tabella di zero, una o più righe corrispondenti alla query full-text. La tabella restituita contiene solo righe della tabella di base che corrispondono ai criteri di selezione specificati nella condizione della ricerca full-text della funzione.  
  
> [!NOTE]  
>  Per informazioni sulla sintassi e sugli argomenti di queste funzioni, vedere [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql) e [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql).  
  
 Le query che utilizzano una di queste funzioni restituiscono un valore di classificazione per pertinenza (RANK) e una chiave full-text (KEY) per ogni riga, come illustrato di seguito:  
  
-   Colonna KEY  
  
     La colonna KEY restituisce valori univoci delle righe restituite. Può essere utilizzata per specificare i criteri di selezione.  
  
-   Colonna RANK  
  
     La colonna RANK restituisce un *valore di pertinenza* per ogni riga che indica il livello di corrispondenza tra la riga e i criteri di selezione. Maggiore è il valore di pertinenza del testo o del documento in una riga, maggiore sarà la pertinenza della riga per una determinata query full-text. Si noti che è possibile classificare in modo identico righe diverse. È possibile limitare il numero di corrispondenze da restituire specificando il parametro *top_n_by_rank* facoltativo. Per altre informazioni, vedere [Limitare i risultati della ricerca con RANK](limit-search-results-with-rank.md).  
  
 Quando si utilizza una di queste funzioni, è necessario specificare la tabella di base in cui eseguire la ricerca full-text. Come con i predicati, è possibile specificare una singola colonna, un elenco di colonne o tutte le colonne della tabella in cui eseguire la ricerca e, facoltativamente, la lingua le cui risorse verranno utilizzate dalla query full-text specificata.  
  
 CONTAINSTABLE è utile per gli stessi tipi di corrispondenze di CONTAINS, mentre FREETEXTTABLE è utile per gli stessi tipi di corrispondenze di FREETEXT. Per altre informazioni, vedere [Cenni preliminari sui predicati full-text CONTAINS e FREETEXT](#OV_ft_predicates)più indietro in questo argomento. Quando si eseguono query che utilizzano le funzioni CONTAINSTABLE e FREETEXTTABLE, è necessario unire in join in modo esplicito le righe restituite alle righe della tabella di base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 In genere, il risultato di CONTAINSTABLE o FREETEXTTABLE deve essere unito in join alla tabella di base. In questi casi, è necessario conoscere il nome della colonna chiave univoca. Questa colonna, presente in ogni tabella abilitata per la funzionalità full-text, viene usata per applicare righe univoche per la tabella (la *colonna chiave**univoca*). Per altre informazioni, vedere [Gestire indici full-text](../indexes/indexes.md).  
  
 
  
### <a name="examples"></a>Esempi  
  
#### <a name="a-using-containstable"></a>A. Utilizzo di CONTAINSTABLE  
 Nell'esempio seguente vengono restituiti l'ID della descrizione e la descrizione di tutti i prodotti per cui la colonna **Description** contiene la parola "aluminum" accanto alla parola "light" o "lightweight". Vengono restituite solo le righe con un valore di pertinenza maggiore o uguale a 2.  
  
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
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>b. Utilizzo di FREETEXTTABLE  
 Nell'esempio seguente viene estesa una query FREETEXTTABLE in modo che vengano restituite per prime le righe con valore di pertinenza maggiore e che la classificazione di ogni riga venga aggiunta all'elenco di selezione. Per specificare la query, è necessario sapere che **ProductDescriptionID** è la colonna chiave univoca per il `ProductDescription` tabella.  
  
```  
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
  
 Di seguito viene riportata un'estensione della stessa query che restituisce solo le righe con valore di pertinenza maggiore o uguale a 10:  
  
```  
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
  
 
  
##  <a name="Using_Boolean_Operators"></a> Utilizzo degli operatori booleani - e, OR e non - in CONTAINS e CONTAINSTABLE  
 Il predicato CONTAINS e la funzione CONTAINSTABLE utilizzano le stesse condizioni di ricerca. Entrambi supportano la combinazione di più termini di ricerca tramite gli operatori booleani-AND, OR e non-per eseguire operazioni logiche. È ad esempio possibile utilizzare AND per trovare righe che contengono sia "latte" sia New York-style bagel". È possibile utilizzare AND NOT, ad esempio, per trovare le righe che contengono "bagel", ma non "cream cheese".  
  
> [!NOTE]  
>  Al contrario, FREETEXT e FREETEXTTABLE considerano i termini booleani come parole da cercare.  
  
 Per informazioni sulla combinazione di CONTAINS con altri predicati che usano gli operatori logici AND, OR e NOT, vedere [Condizione di ricerca &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la tabella ProductDescription del database [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] . Nella query viene utilizzato il predicato CONTAINS per cercare le descrizioni il cui ID sia diverso da 5 e contenenti le parole "Aluminum" e "spindle". Nella condizione di ricerca viene utilizzato l'operatore booleano AND.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> Considerazioni aggiuntive per le query Full-Text  
 Quando si scrivono query full-text, considerare anche gli elementi seguenti:  
  
-   Opzione LANGUAGE  
  
     Molti termini di query dipendono in larga misura dal comportamento del word breaker. Per assicurarsi di utilizzare il word breaker (e lo stemmer) e il thesaurus corretti, è consigliabile specificare l'opzione LANGUAGE. Per altre informazioni, vedere [Scegliere una lingua durante la creazione di un indice full-text](choose-a-language-when-creating-a-full-text-index.md).  
  
-   Parole non significative  
  
     Quando si definisce una query full-text, il motore di ricerca full-text ignora le parole non significative dai criteri di ricerca. Per parole non significative si intendono parole quali "circa", "con", "devo" e "cui" che possono ricorrere di frequente, ma che non hanno alcuna utilità nella ricerca di testo specifico. Le parole non significative vengono riunite in un elenco. Ogni indice full-text è associato a un elenco di parole non significative specifico per determinare quali di queste parole omettere dalla query o dall'indice durante l'indicizzazione. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](full-text-search.md).  
  
-   Thesaurus  
  
     Per impostazione predefinita, le query FREETEXT e FREETEXTTABLE utilizzano il thesaurus. CONTAINS e CONTAINSTABLE supportano un argomento THESAURUS facoltativo.  
  
-   Distinzione maiuscole/minuscole  
  
     Per le query di ricerca full-text non viene fatta distinzione tra maiuscole e minuscole. La lingua giapponese, tuttavia, prevede più forme fonetiche basate sul concetto di normalizzazione ortografica simile alla mancanza di distinzione tra maiuscole e minuscole, ad esempio kana = senza distinzione. Questo tipo di normalizzazione ortografica non è supportato.  
  

  
##  <a name="varbinary"></a> L'esecuzione di query xml le colonne e varbinary (max)  
 Se una colonna `varbinary(max)`, `varbinary` o `xml` viene sottoposta a indicizzazione full-text, le query su questa colonna possono essere eseguite utilizzando predicati (CONTAINS e FREETEXT) e funzioni (CONTAINSTABLE e FREETEXTTABLE) full-text, proprio come su ogni altra colonna indicizzata full-text.  
  
> [!IMPORTANT]  
>  La ricerca full-text può anche essere eseguita con colonne di tipo image. Il tipo di dati `image` verrà comunque rimosso in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarlo nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente lo utilizzano. Usare il tipo di dati `varbinary(max)`.  
  
### <a name="varbinarymax-or-varbinary-data"></a>dati varbinary(max) o varbinary  
 In una singola colonna `varbinary(max)` o `varbinary` possono essere archiviati vari tipi di documenti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta qualsiasi tipo di documento per cui viene installato un filtro e disponibile nel sistema operativo. Il tipo di ogni documento è identificato dall'estensione file relativa. Per un'estensione file doc, ad esempio, la ricerca full-text utilizza il filtro che supporta i documenti di Microsoft Word. Per un elenco dei tipi di documento disponibili, eseguire una query sulla vista del catalogo [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) .  
  
 Si noti che il motore di ricerca full-text può utilizzare i filtri esistenti installati nel sistema operativo. Prima di poter utilizzare i filtri, i word breaker e gli stemmer del sistema operativo, è necessario caricarli nell'istanza del server, come illustrato di seguito:  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 Per creare un indice full-text in una colonna `varbinary(max)`, il motore di ricerca full-text deve accedere alle estensioni file dei documenti nella colonna `varbinary(max)`. Queste informazioni devono essere archiviate in una colonna di tabella, denominata colonna del tipo, che deve essere associata alla colonna `varbinary(max)` nell'indice full-text. Quando si esegue l'indicizzazione di un documento, il motore di ricerca full-text utilizza l'estensione del file nella colonna del tipo per identificare il filtro da utilizzare.  
  
 
  
### <a name="xml-data"></a>dati xml  
 Una colonna del tipo di dati `xml` archivia esclusivamente documenti e frammenti XML, inoltre per i documenti viene utilizzato soltanto il filtro XML. Una colonna del tipo non è pertanto necessaria. Nelle colonne `xml` l'indice full-text indicizza il contenuto degli elementi XML, ma ignora il markup XML. Ai valori di attributo viene applicata l'indicizzazione full-text a meno che non siano valori numerici. I tag elemento sono utilizzati come limiti del token. Sono supportati documenti e frammenti XML o HTML ben formati e contenenti più lingue.  
  
 Per altre informazioni sull'esecuzione di query su un `xml` colonna, vedere [usare la ricerca Full-Text con colonne XML](../xml/use-full-text-search-with-xml-columns.md).  
  
 
  
##  <a name="supported"></a> Forme supportate di termini della Query  
 Questa sezione contiene un riepilogo del supporto fornito per ciascuna forma di query dai predicati full-text e dalle funzioni con valori del set di righe.  
  
> [!NOTE]  
>  Per ottenere la sintassi di un determinato termine di query, fare clic sui collegamenti corrispondenti nella colonna **Supportata da** della tabella seguente.  
  
|Forma del termine di query|Descrizione|Supportata da|  
|----------------------|-----------------|------------------|  
|Una o più parole o frasi specifiche (*termine semplice*)|Nella ricerca full-text, una parola (o *token*) è una stringa i cui limiti vengono identificati da word breaker appropriati, in base alle regole linguistiche della lingua specificata. Una frase valida è costituita da più parole, separate o non separate da segni di punteggiatura.<br /><br /> Ad esempio, "croissant" è una parola e "caf?? "caffè macchiato" è una frase. Le parole e le frasi di questo tipo vengono definite termini semplici.<br /><br /> Per altre informazioni, vedere [Ricerca di parole o frasi specifiche (termine semplice)](#Simple_Term)più avanti in questo argomento.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) consentono di cercare una corrispondenza esatta per la frase.<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) consentono di suddividere la frase in parole separate.|  
|Parola o frase in cui le parole iniziano con il testo specificato (*termine di prefisso*)|Un termine di prefisso fa riferimento a una stringa aggiunta davanti a una parola per produrre una parola derivata o una forma inflessa.<br /><br /> Per un singolo termine di prefisso, qualsiasi parola che inizia con il termine specificato farà parte del set di risultati. Ad esempio, il termine "auto*" corrisponde ad "automatico", "automobile" e così via.<br /><br /> Nel caso di una frase, ogni parola all'interno della frase viene considerata un termine di prefisso. Il termine "tras auto\*", ad esempio, corrisponde a "trasmissione automatica" e a "trasduttore automobile", ma non a "trasmissione motore automatica".<br /><br /> Per altre informazioni, vedere [Esecuzione di ricerche di prefissi (termine di prefisso)](#Prefix_Term)più avanti in questo argomento.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Forme flessive di una parola specifica (*generazione di forme flessive termine*)|Le forme flessive sono costituite dai diversi tempi e coniugazioni di un verbo oppure dalle forme singolare e plurale di un sostantivo. È possibile cercare, ad esempio, la forma flessiva della parola "guida". Se diverse righe della tabella contengono le parole "guida", "guide", "guidò", "guidando" e "guidato", tali parole vengono tutte incluse nel set di risultati, in quanto ognuna può essere generata in modo flessivo da "guida".<br /><br /> Per altre informazioni, vedere [Ricerca di forme flessive di una parola specifica (termine di generazione)](#Inflectional_Generation_Term)più avanti in questo argomento.|Per impostazione predefinita,[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) consentono di cercare le forme flessive di tutte le parole specificate.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) supportano un argomento INFLECTIONAL facoltativo.|  
|Sinonimi di una parola specifica (*termine di generazione-thesaurus*)|Un thesaurus definisce i sinonimi specificati dall'utente per i termini. Se viene aggiunta, ad esempio, una voce quale "{macchina, automobile, camion, furgone}" a un thesaurus, è possibile cercare la forma del thesaurus della parola "macchina". Il set di risultati includerà tutte le righe della tabella in cui viene eseguita la query che contengono le parole "automobile", "camion", "furgone" o "macchina", in quanto ciascuna di queste parole appartiene al set di espansione dei sinonimi relativo alla parola "macchina".<br /><br /> Per informazioni sulla struttura dei file del thesaurus, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](configure-and-manage-thesaurus-files-for-full-text-search.md).|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) il thesaurus per impostazione predefinita.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) supportano un argomento THESAURUS facoltativo.|  
|Una parola o frase vicina a un'altra parola o frase (*termine di prossimità*)|Un termine di prossimità indica parole o frasi vicine le une alle altre. È inoltre possibile specificare il numero massimo di termini non di ricerca che separano il primo e l'ultimo termine della ricerca. È inoltre possibile cercare parole o frasi in qualsiasi ordine o nell'ordine in cui sono state specificate.<br /><br /> È possibile, ad esempio, trovare le righe in cui la parola "ghiaccio" è vicina alla parola "hockey" o in cui la frase "pattinaggio su ghiaccio" è vicina alla frase "hockey su ghiaccio".<br /><br /> Per altre informazioni, vedere [Cercare parole vicine a un'altra parola con NEAR](search-for-words-close-to-another-word-with-near.md).|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Parole o frasi che usano valori ponderati (*termine ponderato*)|Valore ponderato che indica il grado di importanza di ogni parola e frase all'interno di un set di parole e frasi. Il valore 0,0 corrisponde al peso minimo, mentre 1.0 corrisponde al peso massimo.<br /><br /> Ad esempio, in una query in cui vengono cercati più termini, è possibile assegnare a ogni parola un valore ponderato che ne indica l'importanza in relazione alle altre parole della condizione di ricerca. I risultati di questo tipo di query presentano prima le righe più rilevanti, in base al peso relativo assegnato alle parole della ricerca. I set di risultati includono documenti o righe contenenti alcuni dei termini specificati (o contenuto tra di essi). Alcuni risultati, tuttavia, verranno considerati più pertinenti di altri a causa della variazione nei valori ponderati associati a termini cercati diversi.<br /><br /> Per altre informazioni, vedere [Ricerca di parole o frasi tramite valori ponderati (termine ponderato)](#Weighted_Term)più avanti in questo argomento.|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> La ricerca per parola o frase (termine semplice)  
 È possibile usare [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)o [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) per cercare una frase specifica in una tabella. Se, ad esempio, si desidera eseguire una ricerca nella tabella `ProductReview` del database [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] per individuare tutti i commenti su un prodotto utilizzando la frase "learning curve", è possibile utilizzare il predicato CONTAINS nel modo seguente:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 La condizione di ricerca, in questo caso "learning curve", può essere molto complessa ed essere costituita da uno o più termini.  
  
 
  
###  <a name="Prefix_Term"></a> Esecuzione di ricerche con prefisso (termine di prefisso)  
 È possibile usare [CONTAINS](/sql/t-sql/queries/contains-transact-sql) o [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) per cercare parole o frasi con un prefisso specificato. Vengono restituite tutte le voci nella colonna che contengono testo che inizia con il prefisso specificato. È possibile cercare, ad esempio, tutte le righe che contengono il prefisso `top`-, come in `top``ple`, `top``ping`e `top`. La query è la seguente:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 La query restituisce tutto il testo che corrisponde a quello specificato prima dell'asterisco (*). Se il testo e l'asterisco non sono delimitati da virgolette doppie, come in `CONTAINS (DESCRIPTION, 'top*')`, la ricerca full-text non considera l'asterisco un carattere jolly.  
  
 Se il termine di prefisso è una frase, ogni token che la compone viene considerato come un termine di prefisso distinto e vengono restituite tutte le righe contenenti parole che iniziano con tali prefissi. Se viene specificato il termine di prefisso "pennelli gialli*", ad esempio, vengono trovate le righe che contengono il testo "pennelli giallini", "pennellini giallini" o "pennelli gialli", ma non "pennelli sottili gialli".  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> La ricerca di forme Flessive di una parola specifica (termine di generazione)  
 È possibile usare [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)o [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) per cercare tutti i diversi tempi e coniugazioni di un verbo o le forme sia singolare sia plurale di un sostantivo (ricerca di forme flessive) oppure i sinonimi di una parola specifica (ricerca thesaurus).  
  
 Nell'esempio seguente vengono cercate tutte le forme del termine "piede" ("piede", "piedi" e così via) presenti nella colonna `Comments` della tabella `ProductReview` nel database `AdventureWorks` .  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  Nella ricerca full-text vengono utilizzati gli stemmer, che consentono di cercare i diversi tempi e coniugazioni di un verbo o le forme sia singolare sia plurale di un sostantivo. Per altre informazioni sui stemmer, vedere [Configurare e gestire word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  

  
###  <a name="Weighted_Term"></a> Ricerca di parole o frasi tramite valori (termine ponderato) ponderati  
 È possibile usare [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) per cercare parole o frasi e specificare un valore ponderato. Il peso, espresso come numero compreso tra 0,0 e 1,0, indica l'importanza di ogni parola o frase all'interno di un set di parole o frasi. Il valore 0,0 corrisponde al peso minimo, mentre il valore 1,0 corrisponde al peso massimo.  
  
 Nell'esempio seguente viene illustrata una query per la ricerca di tutti gli indirizzi dei clienti, tramite valori di ponderazione, in cui il testo che inizia con la stringa "Bay" contiene anche la parola "Street" o "View". I risultati assegnano un livello di importanza superiore alle righe che contengono il numero maggiore di parole specificate.  
  
```  
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
  

  
##  <a name="tokens"></a> Visualizzazione del risultato della Tokenizzazione di un Word Breaker, Thesaurus ed elenco di parole significative combinazione  
 Dopo aver applicato una determinata combinazione di word breaker, thesaurus ed elenco di parole non significative all'input di una stringa di query, è possibile visualizzare il risultato della tokenizzazione usando la DMV **sys.dm_fts_parser**. Per altre informazioni, vedere [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Creare query di ricerca full-text &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [Migliorare le prestazioni delle query full-text](improve-the-performance-of-full-text-queries.md)  
  
  
