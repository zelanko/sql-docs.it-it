---
title: Migliorare le prestazioni delle query full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a1437f710725df5c87d31f6a80939a5d7869b412
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063221"
---
# <a name="improve-the-performance-of-full-text-queries"></a>Migliorare le prestazioni delle query full-text
  Di seguito viene riportato un elenco di indicazioni che possono favorire il miglioramento delle prestazioni di esecuzione delle query full-text.  
  
 Le prestazioni di esecuzione delle query full-text possono dipendere inoltre da risorse hardware quali memoria, velocità del disco e della CPU, nonché dall'architettura del computer.  
  
-   Deframmentare l'indice della tabella di base tramite [ALTER INDEX REORGANIZE](/sql/t-sql/statements/alter-index-transact-sql).  
  
-   Riorganizzare il catalogo full-text tramite [ALTER FULLTEXT CATALOG REORGANIZE](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql). È necessario eseguire queste operazioni prima del test delle prestazioni poiché l'esecuzione di questa istruzione determina un'unione nell'indice master degli indici full-text in tale catalogo.  
  
-   Limitare la scelta delle colonne chiave full-text a una a colonna di dimensioni ridotte. Benché le colonne a 900 byte siano supportate, è consigliabile utilizzare una colonna chiave di dimensioni inferiori per un indice full-text. `int` e `bigint` forniscono le migliori prestazioni.  
  
-   L'uso di una chiave full-text a numero intero evita la creazione di un join con la tabella di mapping **docid** . Una chiave full-text di tipo integer, pertanto, consente di migliorare le prestazioni di esecuzione delle query di un ordine di grandezza e le prestazioni della ricerca per indicizzazione. Nel caso in cui la chiave full-text corrisponda anche alla chiave di indice cluster, i vantaggi a livello di prestazioni saranno ancora maggiori.  
  
-   Combinare più predicati [CONTAINS](/sql/t-sql/queries/contains-transact-sql) in un unico predicato CONTAINS. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile specificare un elenco di colonne nella query CONTAINS.  
  
-   Se sono necessarie solo informazioni sulla chiave full-text o sulla pertinenza, invece di CONTAINS o FREETEXT usare, rispettivamente, [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) o [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) .  
  
-   Per limitare i risultati e ottimizzare le prestazioni, usare il parametro *top_n_by_rank* delle funzioni FREETEXTTABLE e CONTAINSTABLE. *top_n_by_rank* consente di richiamare solo le occorrenze più attinenti. Usare questo parametro solo se lo scenario aziendale non richiede il richiamo di tutte le occorrenze possibili, ovvero se non richiede il *richiamo totale*.  
  
    > [!NOTE]  
    >  Il richiamo totale è in genere necessario per gli scenari legali, ma potrebbe essere meno importante delle prestazioni per altri scenari, ad esempio il commercio elettronico.  
  
-   Controllare il piano di query full-text per verificare che venga scelto il piano di join appropriato. Se necessario, utilizzare un hint di join o un hint per la query. Se un parametro viene utilizzato nella query full-text, il valore utilizzato per la prima volta per il parametro determina il piano di query. È possibile usare l' [hint per la query](/sql/t-sql/queries/hints-transact-sql-query) OPTIMIZE FOR per forzare la compilazione della query con il valore voluto. In questo modo è possibile ottenere un piano della query deterministico e prestazioni migliori.  
  
-   Un numero eccessivo di frammenti di indice full-text nell'indice full-text può causare una significativa riduzione delle prestazioni di esecuzione delle query. Per ridurre il numero di frammenti, riorganizzare il catalogo full-text tramite l'opzione REORGANIZE dell'istruzione [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] . Questa istruzione consente di unire tutti i frammenti in un singolo frammento più grande e di rimuovere tutte le voci obsolete dall'indice full-text.  
  
-   Nelle ricerche full-text gli operatori logici specificati in CONTAINSTABLE (AND, OR) possono essere implementati come join SQL o all'interno di funzioni di flusso con valori di tabella per l'esecuzione full-text. Le query con un solo tipo di operatori logici vengono in genere implementate dall'esecuzione full-text, mentre le query con operatori logici di più tipi presentano anche join SQL. L'implementazione di un operatore logico all'interno della funzione con valori di tabella per l'esecuzione full-text prevede l'utilizzo di alcune proprietà di indice speciali che ne migliorano la velocità rispetto ai join SQL. Per questo motivo, è consigliabile, se possibile, definire le query utilizzando un solo tipo di operatore logico.  
  
-   Per le applicazioni che contengono affermazioni a relazione selettiva, le prestazioni di esecuzione delle query che utilizzano predicati relazionali selettivi e predicati full-text non selettivi potrebbero risultare migliori se le query sono scritte per l'utilizzo di Query Optimizer. In questo modo, Query Optimizer sarà in grado di stabilire la possibilità o meno di utilizzare l'impostazione di intervalli o di predicati per produrre un piano di query efficace. Questo metodo è più semplice e spesso più efficiente rispetto all'indicizzazione di dati relazionali come dati full-text.  
  
## <a name="related-resources"></a>Risorse correlate  
 [SQL Server 2008 Full-Text Search: Internals and Enhancements](https://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
  
