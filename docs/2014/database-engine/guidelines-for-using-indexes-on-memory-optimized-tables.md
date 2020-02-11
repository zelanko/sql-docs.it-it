---
title: Linee guida per l'uso di indici nelle tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71d26e3f46034019d51bd69b86686f40eb9ce63e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779225"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>Linee guida per l'utilizzo di indici nelle tabelle con ottimizzazione per la memoria
  Gli indici vengono utilizzati per accedere in modo efficiente ai dati nelle tabelle di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La definizione degli indici corretti può migliorare notevolmente le prestazioni delle query. Si consideri, ad esempio, la query riportata di seguito:  
  
```sql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 Se non è presente alcun indice sulla colonna c1, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dovrà essere analizzata l'intera tabella t, quindi dovranno essere filtrate le righe che soddisfano la condizione c1=1. Se tuttavia t include un indice sulla colonna c1, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può essere eseguita direttamente la ricerca del valore 1 e possono essere recuperate le righe.  
  
 Quando si effettua la ricerca di record con un valore specifico, o un intervallo di valori, per una o più colonne della tabella, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è possibile utilizzare un indice per tali colonne in modo da individuare rapidamente i record corrispondenti. Gli indici costituiscono un vantaggio sia per le tabelle basate su disco che per quelle ottimizzate per la memoria. Esistono tuttavia alcune differenze tra le strutture di indice, che è opportuno considerare quando si utilizzano tabelle ottimizzate per la memoria. Gli indici nelle tabelle ottimizzate per la memoria sono definiti indici ottimizzati per la memoria. Di seguito sono riportate alcune delle differenze principali:  
  
-   Gli indici con ottimizzazione per la memoria devono essere creati con [CREATE TABLE &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-table-transact-sql). Gli indici basati su disco possono essere creati con `CREATE TABLE` e `CREATE INDEX`.  
  
-   Gli indici con ottimizzazione per la memoria esistono solo in memoria. Le strutture di indice non vengono salvate in modo permanente sul disco e le operazioni sugli indici vengono registrate nel log delle transazioni. La struttura di indice viene creata contemporaneamente alla creazione in memoria della tabella ottimizzata per la memoria, sia durante l'esecuzione di CREATE TABLE che durante l'avvio del database.  
  
-   Gli indici con ottimizzazione per la memoria sono implicitamente di copertura, ovvero tutte le colonne sono virtualmente incluse nell'indice e le ricerche tramite segnalibro non sono richieste per le tabelle ottimizzate per la memoria. Anziché un riferimento alla chiave primaria, gli indici ottimizzati per la memoria includono solo un puntatore alla memoria per la riga effettiva nella struttura dei dati della tabella.  
  
-   La frammentazione e il fattore di riempimento non si applicano agli indici ottimizzati per la memoria. Negli indici basati su disco la frammentazione si riferisce alle pagine nell'albero B scritte su disco non in ordine. Gli indici con ottimizzazione per la memoria non vengono scritti sul disco o letti dal disco. Il fattore di riempimento negli indici ad albero B basati su disco indica il livello di riempimento delle strutture fisiche delle pagine con i dati effettivi. Per le strutture di indice ottimizzate per la memoria non sono previste pagine a dimensione fissa.  
  
 Esistono due tipi di indici ottimizzati per la memoria:  
  
-   Indici hash non cluster, concepiti per le ricerche di punti. Per ulteriori informazioni sugli indici hash, vedere [hash Indexes](hash-indexes.md).  
  
-   Indici non cluster, concepiti per le analisi di intervalli e le analisi ordinate.  
  
 Con un indice hash l'accesso ai dati viene eseguito tramite una tabella hash in memoria. Gli indici hash non includono pagine e hanno sempre una dimensione fissa. Possono tuttavia includere bucket di hash vuoti, con la conseguente limitazione dello spazio inutilizzato. I valori restituiti da una query che utilizza un indice hash non vengono ordinati. Gli indici hash sono ottimizzati per le ricerche eseguite negli indici sui predicati di uguaglianza e supportano inoltre le analisi complete degli indici.  
  
 Gli indici non cluster (non indici hash) supportano tutto ciò che è supportato dagli indici hash più le operazioni di ricerca sui predicati di disuguaglianza, come maggiore di o minore di, nonché l'ordinamento. Le righe possono essere recuperate in base all'ordine specificato con la creazione dell'indice. Se l'ordinamento dell'indice corrisponde all'ordinamento richiesto per una determinata query, ad esempio se la chiave di indice corrisponde alla clausola ORDER BY, non è necessario ordinare le righe come parte dell'esecuzione della query. Gli indici non cluster con ottimizzazione per la memoria sono unidirezionali; non supportano il recupero delle righe in un ordinamento che è inverso all'ordinamento dell'indice. Ad esempio, per un indice specificato come (c1 ASC), non è possibile analizzare l'indice in ordine inverso, come (c1 DESC).  
  
 Ogni indice utilizza memoria. Gli indici hash utilizzano una quantità di memoria fissa (una funzione del numero di bucket). Per gli indici non cluster l'utilizzo della memoria è una funzione del conteggio delle righe e della dimensione delle colonne chiave di indice, con un overhead aggiuntivo a seconda del carico di lavoro. La memoria per gli indici ottimizzati per la memoria è in aggiunta ed è separata dalla memoria utilizzata per archiviare le righe nelle tabelle ottimizzate per la memoria.  
  
 I valori di chiave duplicati condividono sempre lo stesso bucket di hash. Se un indice hash contiene molti valori di chiave duplicati, le lunghe catene di hash risultanti influiranno negativamente sulle prestazioni. Le collisioni hash, che si verificano in un qualsiasi indice hash, ridurranno ulteriormente le prestazioni in questo scenario. Per questo motivo, se il numero di chiavi di indice univoche è almeno 100 volte inferiore al numero di righe, è possibile ridurre il rischio di collisioni hash rendendo il numero di bucket molto più grande (almeno otto volte il numero di chiavi di indice univoche. per ulteriori informazioni, vedere [determinare il numero di bucket corretto per gli indici hash](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md) ) oppure eliminare completamente le collisioni hash usando un indice non cluster.  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>Determinazione degli indici da utilizzare per una tabella con ottimizzazione per la memoria  
 Ogni tabella ottimizzata per la memoria deve contenere almeno un indice. Si noti che con ogni vincolo PRIMARY KEY viene creato un indice in modo implicito, pertanto se una tabella dispone di una chiave primaria, include un indice. Una chiave primaria è un requisito per una tabella durevole ottimizzata per la memoria.  
  
 Quando si esegue una query su una tabella ottimizzata per la memoria, gli indici hash offrono prestazioni migliori se la clausola del predicato contiene solo predicati di uguaglianza. Il predicato deve includere tutte le colonne nella chiave di indice hash. Se viene fornito un predicato di disuguaglianza, l'indice hash verrà ripristinato in un'analisi.  
  
 Una colonna di una tabella ottimizzata per la memoria può far parte sia di un indice hash che di un indice non cluster.  
  
 Quando si esegue una query su una tabella ottimizzata per la memoria con predicati di disuguaglianza, gli indici non cluster offriranno prestazioni migliori rispetto agli indici hash non cluster.  
  
 L'indice hash richiede una chiave per eseguire l'hashing ovvero eseguire ricerche nell'indice. Se una chiave di indice è costituita da due colonne e si specifica solo la prima colonna, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non sarà disponibile una chiave completa di cui eseguire l'hashing. Verrà pertanto generato un piano di query per l'analisi di indice. L'utilizzo determina le colonne da indicizzare.  
  
 Quando una colonna in un indice non cluster contiene lo stesso valore in molte righe, ovvero le colonne chiave dell'indice contengono molti valori duplicati, le prestazioni per le operazioni di aggiornamento, inserimento ed eliminazione potrebbero risultare ridotte.  Un modo per migliorare le prestazioni in questa situazione è aggiungere un'altra colonna nell'indice non cluster.  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>Operazioni sugli indici ottimizzati per la memoria e basati su disco.  
  
|Operazione|Indice hash non cluster con ottimizzazione per la memoria|Indice non cluster con ottimizzazione per la memoria|Indice basato su disco|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|Index Scan, recupera tutte le righe della tabella.|Sì|Sì|Sì|  
|Index Seek su predicati di uguaglianza (=).|Sì<br /><br /> (chiave completa necessaria)|Sì <sup>1</sup>|Sì|  
|Index Seek su predicati di disuguaglianza (>, < \<, =, >=, between).|No (risultati in un'analisi di indice)|Sì <sup>1</sup>|Sì|  
|Recupero di righe con un ordinamento corrispondente alla definizione dell'indice.|No|Sì|Sì|  
|Recupero di righe con un ordinamento inverso alla definizione dell'indice.|No|No|Sì|  
  
 Nella tabella, Sì significa che l'indice può soddisfare la richiesta in modo appropriato e No significa che l'indice non può essere usato per soddisfare correttamente la richiesta.  
  
 <sup>1</sup> per un indice non cluster ottimizzato per la memoria, non è necessaria la chiave completa per eseguire una ricerca nell'indice. Tuttavia, se un valore di una colonna segue una colonna mancante, l'analisi verrà eseguita in base all'ordine delle colonne della chiave di indice.  
  
## <a name="index-count"></a>Numero di indici  
 Per una tabella ottimizzata per la memoria possono essere presenti un massimo di 8 indici, incluso quello creato con la chiave primaria.  
  
 Per quanto riguarda il numero degli indici creati in una tabella ottimizzata per la memoria, considerare quanto indicato di seguito:  
  
-   Specificare gli indici necessari quando si crea la tabella. Non è possibile creare un indice per una tabella ottimizzata per la memoria dopo è stata creata. Se si desidera aggiungere un indice per una tabella ottimizzata per la memoria, eliminarla e ricrearla.  
  
-   Evitare di creare un indice utilizzato raramente:  
  
     Il processo di Garbage Collection funziona meglio se tutti gli indici della tabella vengono utilizzati di frequente. Gli indici utilizzati raramente possono causare un funzionamento non ottimale del sistema di Garbage Collection per le versioni di riga precedenti.  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>Creazione di un indice con ottimizzazione per la memoria: esempi di codice  
 Indice hash a livello di colonna:  
  
```sql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Indice hash a livello di tabella:  
  
```sql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Indice hash di chiave primaria a livello di colonna:  
  
```sql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Indice hash di chiave primaria a livello di tabella:  
  
```sql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Indice non cluster a livello di colonna:  
  
```sql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Indice non cluster a livello di tabella:  
  
```sql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Indice non cluster di chiave primaria a livello di colonna:  
  
```sql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Indice non cluster di chiave primaria a livello di tabella:  
  
```sql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Indice multicolonna definito dopo la definizione delle colonne:  
  
```sql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Indici nelle tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Determinazione del numero di bucket corretto per gli indici hash](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [Indici hash](hash-indexes.md)  
  
  
