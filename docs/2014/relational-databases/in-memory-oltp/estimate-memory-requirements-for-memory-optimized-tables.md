---
title: Stimare i requisiti di memoria delle tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cbd8a79bf9d881d2d4c9055531bac2e290f202a4
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811014"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>Stimare i requisiti di memoria delle tabelle con ottimizzazione per la memoria
  Se si crea una nuova [!INCLUDE[hek_2](../../includes/hek-2-md.md)] tabella ottimizzata per la memoria o si esegue la migrazione di una tabella basata su disco esistente a una tabella ottimizzata per la memoria, è importante avere una stima ragionevole delle esigenze di memoria di ogni tabella in modo da poter effettuare il provisioning del server con sufficiente memoria. In questa sezione viene descritto come stimare la quantità di memoria necessaria per contenere i dati di una tabella ottimizzata per la memoria.  
  
 Se si prende in considerazione la migrazione da tabelle basate su disco a tabelle ottimizzate per la memoria, prima di procedere con questo argomento, vedere [Determinare se una tabella o una stored procedure deve essere trasferita a OLTP in memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) per informazioni aggiuntive sulle tabelle più appropriate per la migrazione. Tutti gli argomenti disponibili in [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md) offrono informazioni aggiuntive sulla migrazione da tabelle basate su disco a tabelle ottimizzate per la memoria.  
  
## <a name="sections-in-this-topic"></a>Sezioni dell'argomento  
  
-   [Esempio di tabella ottimizzata per la memoria](#bkmk_ExampleTable)  
  
-   [Memoria per la tabella](#bkmk_MemoryForTable)  
  
-   [Memoria per gli indici](#bkmk_IndexMeemory)  
  
-   [Memoria per il controllo delle versioni delle righe](#bkmk_MemoryForRowVersions)  
  
-   [Memoria per le variabili di tabella](#bkmk_TableVariables)  
  
-   [Memoria in caso di aumento delle dimensioni](#bkmk_MemoryForGrowth)  
  
##  <a name="bkmk_ExampleTable"></a> Esempio di tabella ottimizzata per la memoria  
 Si consideri il seguente schema di tabella ottimizzata per la memoria:  
  
```sql  
  
CREATE TABLE t_hk (  
col1 int NOT NULL PRIMARY KEY NONCLUSTERED,  
col2 int NOT NULL INDEX t1c2_index   
     HASH WITH (bucket_count = 5000000),  
col3 int NOT NULL INDEX t1c3_index   
     HASH WITH (bucket_count = 5000000),  
col4 int NOT NULL INDEX t1c4_index   
     HASH WITH (bucket_count = 5000000),  
col5 int NOT NULL INDEX t1c5_index NONCLUSTERED,  
col6 char (50) NOT NULL,  
col7 char (50) NOT NULL,   
col8 char (30) NOT NULL,   
col9 char (50) NOT NULL  
     WITH (memory_optimized = on)  
GO  
  
```  
  
 Utilizzando questo schema sarà possibile stabilire la memoria minima necessaria per questa tabella ottimizzata per la memoria.  
  
##  <a name="bkmk_MemoryForTable"></a> Memoria per la tabella  
 La riga di una tabella ottimizzata per la memoria è costituita da tre parti:  
  
-   **Timestamp**   
    Intestazione di riga/timestamp = 24 byte.  
  
-   **Puntatori dell'indice**   
    Per ogni indice hash nella tabella, a ogni riga è associato un puntatore all'indirizzo di 8 byte alla riga successiva nell'indice.  Poiché sono presenti 4 indici, tramite ogni riga vengono allocati 32 byte per i puntatori dell'indice (un puntatore di 8 byte per ogni indice).  
  
-   **Dati**   
    Le dimensioni della parte di dati della riga vengono determinate sommando le dimensioni di tipo per ogni colonna di dati.  Nella tabella di esempio sono contenuti cinque Integer a 4 byte, tre colonne di tipo carattere di 50 byte e una colonna di tipo carattere di 30 byte.  Pertanto la parte di dati di ogni riga è 4 + 4 + 4 + 4 + 4 + 50 + 50 + 30 + 50, vale a dire 200 byte.  
  
 Di seguito è riportato un calcolo di dimensioni per 5.000.000 (5 milioni) di righe in una tabella ottimizzata per la memoria. La memoria totale utilizzata dalle righe di dati viene stimata come segue:  
  
 **Memoria per le righe della tabella**  
  
 Dai calcoli sopra riportati, le dimensioni di ogni riga della tabella ottimizzata per la memoria sono pari a 24 + 32 + 200, vale a dire 256 byte.  Dal momento che sono presenti 5 milioni di righe, per la tabella verranno utilizzati 5.000.000 * 256 byte, vale a dire 1.280.000.000 di byte, circa 1,28 GB.  
  
##  <a name="bkmk_IndexMeemory"></a> Memoria per gli indici  
 **Memoria per ogni indice hash**  
  
 Ogni indice hash è una matrice di hash di puntatori all'indirizzo di 8 byte.  Le dimensioni della matrice vengono determinata meglio in base al numero di valori di indice univoci per l'indice in questione, ad esempio il numero di valori Col2 univoci è un buon punto di partenza per le dimensioni della matrice per t1c2_index. Una matrice di hash eccessiva comporta uno spreco di memoria.  Una matrice di hash di piccole dimensioni determina un rallentamento delle prestazioni in quanto vi saranno troppe collisioni per i valori di indice con hashing nello stesso indice.  
  
 Tramite gli indici hash è possibile ottenere ricerche di uguaglianza estremamente veloci, ad esempio:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 = 3  
  
```  
  
 Gli indici non cluster sono più veloci per le ricerche in intervalli, ad esempio:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 >= 3  
  
```  
  
 Se si esegue la migrazione di una tabella basata su disco, è possibile utilizzare quando riportato di seguito per determinare il numero di valori univoci per l'indice t1c2_index.  
  
```sql  
  
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk  
  
```  
  
 Se si crea una nuova tabella, sarà necessario stimare le dimensioni della matrice o raccogliere i dati dal test prima di eseguire la distribuzione.  
  
 Per informazioni sul funzionamento degli indici hash in tabelle ottimizzate per la memoria [!INCLUDE[hek_2](../../includes/hek-2-md.md)], vedere [Indici hash](../../database-engine/hash-indexes.md).  
  
 **Nota:** Non è possibile modificare le dimensioni della matrice dell'indice hash in tempo reale. Per modificare queste dimensioni è necessario eliminare la tabella, modificare il valore di bucket_count e ricreare la tabella.  
  
 **Impostazione delle dimensioni della matrice dell'indice hash**  
  
 Le dimensioni della matrice di hash vengono `(bucket_count= <value>)` impostate \<da where value > è un valore intero maggiore di zero. Se \<il valore > non è una potenza di 2, il valore effettivo di bucket_count viene arrotondato per eccesso alla potenza di 2 successiva più vicina.  Nella tabella di esempio, (bucket_count = 5 milioni), poiché 5 milioni non è una potenza di 2, il numero effettivo di bucket viene arrotondato per eccesso a 8.388.608 (2<sup>23</sup>).  È necessario utilizzare questo numero, non 5.000.000, quando si calcola la memoria necessaria per la matrice di hash.  
  
 Pertanto, nell'esempio, la memoria necessaria per ogni matrice di hash è:  
  
 8\.388.608 * 8 = 2<sup>23</sup> \* 8 = 2<sup>23</sup> \* 2<sup>3</sup> = 2<sup>26</sup> = 67.108.864 o circa 64 MB.  
  
 Poiché vi sono tre indici hash, la memoria necessaria per gli indici hash è 3 * 64 MB = 192 MB.  
  
 **Memoria per gli indici non cluster**  
  
 Gli indici non cluster vengono implementati come alberi b con i nodi interni contenenti il valore di indice e i puntatori ai nodi successivi.  Nei nodi foglia sono inclusi il valore di indice e un puntatore alla riga di tabella in memoria.  
  
 A differenza degli indici hash, gli indici non cluster non hanno una dimensione del bucket fissa. Le dimensioni dell'indice aumentano e si riducono dinamicamente in base ai dati.  
  
 La memoria necessaria per gli indici non cluster può essere calcolata nel modo seguente:  
  
-   **Memoria allocata ai nodi non foglia**   
    Per una configurazione tipica, la memoria allocata ai nodi non foglia è una percentuale minima della memoria globale utilizzata dall'indice, che per le sue dimensioni contenute può essere sicuramente ignorata.  
  
-   **Memoria per i nodi foglia**   
    I nodi foglia hanno una riga per ogni chiave univoca della tabella che punta alle righe di dati con questa chiave univoca.  Se si dispone di più righe con la stessa chiave, ovvero se si dispone di un indice non cluster non univoco, è presente una sola riga nel nodo foglia dell'indice che punta a una delle righe con le altre righe collegate tra loro.  Pertanto, la memoria totale necessaria può essere approssimata nel modo seguente:   
    memoryForNonClusteredIndex = (pointerSize + sum (keyColumnDataTypeSizes) * rowsWithUniqueKeys  
  
 Gli indici non cluster sono migliori se usati per le ricerche di intervallo, come esemplificato dalla query seguente:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE c2 > 5  
```  
  
##  <a name="bkmk_MemoryForRowVersions"></a> Memoria per il controllo delle versioni delle righe  
 Per evitare blocchi, tramite OLTP in memoria viene utilizzata la concorrenza ottimistica durante l'aggiornamento o l'eliminazione di righe. Pertanto, quando una riga viene aggiornata, viene creata una versione aggiuntiva della riga. Il sistema mantiene le versioni precedenti disponibili fino a quando non viene completata l'esecuzione di tutte le transazioni che potrebbero eventualmente utilizzare la versione. Quando una riga viene eliminata, il sistema funziona in una modalità simile a un aggiornamento, mantenendo la versione disponibile fino a quando non è più necessaria. Le operazioni di lettura e inserimento non comportano la creazione di versioni di righe aggiuntive.  
  
 Poiché è possibile che vi sia un numero di righe aggiuntive in memoria in qualsiasi momento in attesa del ciclo di Garbage Collection per rilasciare la memoria, è necessario disporre di memoria sufficiente per contenere queste righe aggiuntive.  
  
 Il numero di righe aggiuntive può essere stimato calcolando il numero massimo di aggiornamenti ed eliminazioni di righe al secondo, quindi moltiplicando il risultato per il numero di secondi impiegati dalla transazione più lunga (almeno 1).  
  
 Il valore viene quindi moltiplicato per le dimensioni della riga per ottenere il numero di byte necessari per il controllo delle versioni delle righe.  
  
 `rowVersions = durationOfLongestTransactionInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
 Le esigenze di memoria per le righe non aggiornate vengono quindi stimate moltiplicando il numero di righe non aggiornate per le dimensioni di una riga di tabella ottimizzata per la memoria (vedere [memoria per la tabella](#bkmk_MemoryForTable) precedente).  
  
 `memoryForRowVersions = rowVersions * rowSize`  
  
##  <a name="bkmk_TableVariables"></a> Memoria per le variabili di tabella  
 La memoria utilizzata per una variabile di tabella viene rilasciata solo quando la variabile di tabella abbandona l'ambito. Le righe eliminate, incluse quelle eliminate come parte di un aggiornamento, da una variabile di tabella non vengono sottoposte a Garbage Collection. Finché la variabile di tabella non abbandona l'ambito, la memoria non viene rilasciata.  
  
 Le variabili di tabella definite in un batch SQL di grandi dimensioni, a differenza di un ambito di procedura, utilizzate in molte transazioni, possono richiedere una grande quantità di memoria. Poiché non vengono sottoposte a Garbage Collection, le righe eliminate in una variabile di tabella possono utilizzare una grande quantità di memoria e influire negativamente sulle prestazioni poiché le operazioni di lettura devono eseguire l'analisi delle righe eliminate.  
  
##  <a name="bkmk_MemoryForGrowth"></a> Memoria in caso di aumento delle dimensioni  
 Con i calcoli sopra riportati vengono stimati i requisiti di memoria della tabella attuale. Oltre a questa memoria, è necessario stimare la crescita della tabella e fornire una memoria sufficiente per gestire questa crescita.  Ad esempio, se si prevede una crescita del 10%, sarà necessario moltiplicare i risultati precedenti per 1,1 per ottenere la memoria totale necessaria per la tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)  
  
  
