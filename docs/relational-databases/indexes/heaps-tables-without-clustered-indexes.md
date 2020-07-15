---
title: Heap (tabelle senza indici cluster) | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
- forward record
- forwarded record
- forwarding pointer
- RID
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e186d1da5ab42b25c120303a545c9164d949ad45
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786480"
---
# <a name="heaps-tables-without-clustered-indexes"></a>Heap (tabelle senza indici cluster)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Un heap è una tabella per cui non è disponibile un indice cluster. Nelle tabelle archiviate come heap è possibile creare uno o più indici non cluster. I dati vengono archiviati nell'heap senza un ordine specificato. In genere i dati vengono inizialmente archiviati nell'ordine in cui le righe vengono inserite nella tabella, tuttavia [!INCLUDE[ssDE](../../includes/ssde-md.md)] può spostare i dati nell'heap in modo da archiviare le righe in modo efficiente, pertanto non è possibile prevedere l'ordine dei dati. Per garantire l'ordine delle righe restituite da un heap, è necessario utilizzare la clausola `ORDER BY`. Per specificare un ordine logico permanente per l'archiviazione delle righe, creare un indice cluster nella tabella, in modo che non sia un heap.  
  
> [!NOTE]  
> Esistono talvolta motivi per i quali è preferibile lasciare una tabella come heap invece di creare un indice cluster, tuttavia l'utilizzo efficiente degli heap richiede competenze avanzate. Alla maggior parte delle tabelle deve essere associato un indice cluster selezionato con attenzione a meno che non sussista un motivo valido per cui la tabella debba rimanere un heap.  
  
## <a name="when-to-use-a-heap"></a>Quando utilizzare un heap  
Quando si archivia una tabella come heap, le singole righe vengono identificate tramite riferimento a un identificatore di riga (RID) di 8 byte costituito da numero del file, numero della pagina di dati e slot nella pagina (FileID:PageID:SlotID). L'ID di riga è una struttura piccola ed efficiente. 

Gli heap possono essere usati come tabelle di staging per operazioni di inserimento di grandi dimensioni e non ordinate. Poiché i dati vengono inseriti senza applicare un ordine rigoroso, l'operazione di inserimento è in genere più veloce rispetto all'inserimento equivalente in un indice cluster. Se i dati dell'heap verranno letti ed elaborati in una destinazione finale, può essere utile creare un indice non cluster narrow che copra il predicato di ricerca usato dalla query di lettura. 

> [!NOTE]  
> I dati vengono recuperati da un heap in ordine di pagine di dati, ma non necessariamente nell'ordine in cui sono stati inseriti i dati. 

A volte i professionisti esperti di elaborazione dati usano gli heap anche quando l'accesso ai dati avviene sempre attraverso indici non cluster e il RID risulta più piccolo di una chiave di indice cluster. 

Se una tabella è un heap e non ha indici non cluster, per individuare qualsiasi riga è necessario leggere l'intera tabella (scansione di tabella). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente di cercare un RID direttamente nell'heap. Questa operazione può essere accettabile quando la tabella è di dimensioni ridotte.  
  
## <a name="when-not-to-use-a-heap"></a>Quando non utilizzare un heap  
 Non utilizzare un heap quando i dati vengono restituiti di frequente con un ordinamento. Un indice cluster nella colonna di ordinamento può evitare l'esecuzione dell'operazione di ordinamento.  
  
 Non utilizzare un heap quando i dati vengono spesso raggruppati insieme. I dati devono essere ordinati prima di essere raggruppati, pertanto un indice cluster nella colonna di ordinamento può evitare l'esecuzione dell'operazione di ordinamento.  
  
 Non utilizzare un heap quando si eseguono spesso query su intervalli di dati della tabella. Un indice cluster nella colonna dell'intervallo evita la necessità di ordinare l'intero heap.  
  
 Non usare un heap quando non sono presenti indici non cluster e la tabella è di grandi dimensioni, a meno che non si intenda restituire l'intero contenuto della tabella senza alcun ordine specificato. Per individuare qualsiasi riga in un heap, è necessario leggerne tutte le righe.  
 
 Non usare un heap se i dati vengono aggiornati di frequente. Se si aggiorna un record e l'aggiornamento usa più spazio nelle pagine di dati rispetto a quello attualmente in uso, è necessario spostare il record in una pagina di dati con spazio libero sufficiente. In questo modo viene creato un **record inoltrato** che punta alla nuova posizione dei dati e il **puntatore di inoltro** deve essere scritto nella pagina che conteneva i dati in precedenza, per indicare la nuova posizione fisica. Questa operazione introduce frammentazione nell'heap. Durante la scansione di un heap, è necessario seguire questi puntatori e ciò limita le prestazioni di read-ahead e può causare I/O aggiuntivo con conseguente riduzione delle prestazioni di analisi. 
  
## <a name="managing-heaps"></a>Gestione di heap  
 Per creare un heap, creare una tabella senza un indice cluster. Se la tabella dispone già di un indice cluster, rimuoverlo per restituire la tabella a un heap.  
  
 Per rimuovere un heap, creare un indice cluster nell'heap.  
  
 Per ricompilare un heap per recuperare lo spazio sprecato:
 -  Creare un indice cluster nell'heap e quindi rimuovere tale indice cluster.  
 -  Usare il comando `ALTER TABLE ... REBUILD` per ricompilare l'heap.
  
> [!WARNING]  
> Per la creazione o la rimozione di indici cluster è richiesta la riscrittura dell'intera tabella. Se la tabella dispone di indici non cluster, è necessario ricrearli tutti ogni volta che l'indice cluster viene modificato. Pertanto, il passaggio da un heap a una struttura di indice cluster o viceversa può richiedere molto tempo e spazio su disco per riordinare i dati in tempdb.  

## <a name="heap-structures"></a>Struttura degli heap
Un heap è una tabella per cui non è disponibile un indice cluster. Agli heap corrisponde una riga in [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)con `index_id = 0` per ogni partizione usata dall'heap. Per impostazione predefinita, a ogni heap è associata una singola partizione. Se a un heap sono associate più partizioni, ognuna di esse ha una struttura di heap contenente i dati per la partizione specifica. Ad esempio, se a un heap sono associate quattro partizioni, saranno presenti quattro strutture di heap, una per ogni partizione.

A seconda dei tipi di dati dell'heap, ogni struttura di heap conterrà una o più unità di allocazione per l'archiviazione e la gestione dei dati di una partizione specifica. Ogni heap conterrà almeno un'unità di allocazione `IN_ROW_DATA` per partizione e un'unità di allocazione `LOB_DATA` per partizione, se l'heap include colonne LOB (Large Object). Conterrà anche un'unità di allocazione `ROW_OVERFLOW_DATA` per partizione, se include colonne a lunghezza variabile che superano il limite della lunghezza di riga di 8.060.

La colonna `first_iam_page` nella vista di sistema `sys.system_internals_allocation_units` punta alla prima pagina IAM nella catena di pagine IAM che gestiscono lo spazio allocato all'heap in una partizione specifica. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa le pagine IAM per spostarsi all'interno dell'heap. Le pagine di dati e le righe in esse incluse non sono disposte in base a un ordine specifico e non sono collegate tra loro. L'unico collegamento logico tra le pagine di dati sono le informazioni registrate nelle pagine IAM.

> [!IMPORTANT]  
> La vista di sistema `sys.system_internals_allocation_units` è riservata solo per uso interno in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è garantita la compatibilità con le versioni future.
 
Le analisi di tabella o le letture seriali dell'heap possono essere eseguite mediante l'analisi delle pagine IAM allo scopo di individuare gli extent che includono le pagine dell'heap. Poiché le pagine IAM rappresentano gli extent nello stesso ordine in cui sono disposti nel file di dati, le analisi seriali dell'heap vengono eseguite progressivamente in ogni file. Inoltre, se si imposta la sequenza di analisi tramite le pagine IAM, le righe dell'heap non vengono in genere restituite in base all'ordine in cui sono state inserite.

Nella figura seguente viene illustrato l'uso delle pagine IAM in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] per recuperare le righe di dati di un heap relativo a una singola partizione. 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)
  
## <a name="related-content"></a>Contenuto correlato  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)     
[Descrizione di indici cluster e non cluster.](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
  
