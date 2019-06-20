---
title: Risoluzione dei problemi di prestazioni comuni con gli indici Hash ottimizzati per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7ed4098feb8bfd2d156e3de2f81fbf7329915aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62842536"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>Risoluzione dei problemi comuni di prestazioni con gli indici hash con ottimizzazione per la memoria
  In questo argomento verrà presentata la risoluzione di problemi comuni relativi agli indici hash.  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>La ricerca richiede un subset di colonne chiave di indice hash  
 **Problema:** Gli indici hash richiedono valori per tutte le colonne chiave di indice per calcolare il valore hash e individuare le righe corrispondenti nella tabella hash. Pertanto, se una query include i predicati di uguaglianza solo per un subset di chiavi di indice nella clausola WHERE, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non può utilizzare una ricerca nell'indice per individuare le righe che corrispondono ai predicati nella clausola WHERE.  
  
 Al contrario, gli indici ordinati, come gli indici non cluster basati su disco e gli indici non cluster ottimizzati per la memoria supportano la ricerca nell'indice in un subset di colonne chiave di indice, purché siano colonne iniziali nell'indice.  
  
 **Sintomo:** Ciò comporta una riduzione delle prestazioni, come [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deve eseguire scansioni complete delle tabelle anziché una ricerca nell'indice, che in genere è un'operazione più veloce.  
  
 **Come risolvere i problemi:** Oltre alla riduzione delle prestazioni, ispezione dei piani di query mostrerà un'analisi anziché una ricerca nell'indice. Se la query è relativamente semplice, l'analisi del testo della query e della definizione dell'indice indicherà se la ricerca richiede un subset delle colonne chiave di indice.  
  
 Si considerino la tabella e la query seguenti:  
  
```sql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 La tabella ha un indice hash su due colonne (o_id, od_id), mentre la query ha un predicato di uguaglianza su (o_id). Poiché la query ha predicati di uguaglianza solo in un subset di colonne chiave di indice, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non può eseguire un'operazione di ricerca nell'indice utilizzando PK_od; in alternativa, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deve passare a un'analisi completa dell'indice.  
  
 **Soluzioni alternative:** Esistono numerose possibili soluzioni alternative. Ad esempio:  
  
-   Ricreare l'indice come tipo non cluster anziché hash non cluster. L'indice non cluster ottimizzato per la memoria è ordinato e, pertanto, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può eseguire una ricerca nell'indice nelle colonne chiave di indice iniziali. La definizione di chiave primaria risultante per l'esempio sarebbe `constraint PK_od primary key nonclustered`.  
  
-   Modificare la chiave di indice corrente affinché corrisponda alle colonne nella clausola WHERE.  
  
-   Aggiungere un nuovo indice hash corrispondente alle colonne nella clausola WHERE della query. Nell'esempio, la definizione di tabella risultante sarebbe simile a quanto segue:  
  
    ```sql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 Si noti che le prestazioni di un indice hash ottimizzato per la memoria non sono ottimali se sono presenti molte righe duplicate per un determinato valore di chiave di indice: nell'esempio, se il numero di valori univoci per la colonna o_id è molto minore del numero di righe nella tabella, non è ottimale aggiungere un indice su (o_id); in alternativa, la modifica del tipo dell'indice PK_od da hash a non cluster potrebbe essere la soluzione migliore. Per ulteriori informazioni, vedere [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Indici in tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
