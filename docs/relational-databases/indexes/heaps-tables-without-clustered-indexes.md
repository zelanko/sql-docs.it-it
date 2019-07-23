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
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5234820dbf88067aad2ff76b0bd373c7f70cb3e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909781"
---
# <a name="heaps-tables-without-clustered-indexes"></a>Heap (tabelle senza indici cluster)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Un heap è una tabella per cui non è disponibile un indice cluster. Nelle tabelle archiviate come heap è possibile creare uno o più indici non cluster. I dati vengono archiviati nell'heap senza un ordine specificato. In genere i dati vengono inizialmente archiviati nell'ordine in cui le righe vengono inserite nella tabella, tuttavia [!INCLUDE[ssDE](../../includes/ssde-md.md)] può spostare i dati nell'heap in modo da archiviare le righe in modo efficiente, pertanto non è possibile prevedere l'ordine dei dati. Per garantire l'ordine delle righe restituite da un heap, è necessario utilizzare la clausola **ORDER BY** . Per specificare l'ordine di archiviazione delle righe, creare un indice cluster nella tabella, in modo che essa non sia un heap.  
  
> [!NOTE]  
>  Esistono talvolta motivi per i quali è preferibile lasciare una tabella come heap invece di creare un indice cluster, tuttavia l'utilizzo efficiente degli heap richiede competenze avanzate. Alla maggior parte delle tabelle deve essere associato un indice cluster selezionato con attenzione a meno che non sussista un motivo valido per cui la tabella debba rimanere un heap.  
  
## <a name="when-to-use-a-heap"></a>Quando utilizzare un heap  
 Se una tabella è un heap e non dispone di indici non cluster, per individuare qualsiasi riga è necessario esaminare l'intera tabella (analisi della tabella). Ciò può risultare accettabile in caso di tabelle di piccole dimensioni, ad esempio un elenco di 12 sedi locali di una società.  
  
 Quando si archivia una tabella come heap, le singole righe sono identificate mediante il riferimento a un identificatore di riga (RID) costituito dal numero del file, dal numero della pagina di dati e dallo slot nella pagina. L'ID della riga è una struttura piccola ed efficiente. Talvolta gli architetti specializzati utilizzano gli heap quando l'accesso ai dati avviene sempre tramite indici non cluster e il RID risulta più piccolo di una chiave di indice cluster.  
  
## <a name="when-not-to-use-a-heap"></a>Quando non utilizzare un heap  
 Non utilizzare un heap quando i dati vengono restituiti di frequente con un ordinamento. Un indice cluster nella colonna di ordinamento può evitare l'esecuzione dell'operazione di ordinamento.  
  
 Non utilizzare un heap quando i dati vengono spesso raggruppati insieme. I dati devono essere ordinati prima di essere raggruppati, pertanto un indice cluster nella colonna di ordinamento può evitare l'esecuzione dell'operazione di ordinamento.  
  
 Non utilizzare un heap quando si eseguono spesso query su intervalli di dati della tabella.  Un indice cluster nella colonna dell'intervallo evita la necessità di ordinare l'intero heap.  
  
 Non utilizzare un heap quando non sono presenti indici non cluster e la tabella è di grandi dimensioni. Per individuare qualsiasi riga in un heap, è necessario leggerne tutte le righe.  
  
## <a name="managing-heaps"></a>Gestione di heap  
 Per creare un heap, creare una tabella senza un indice cluster. Se la tabella dispone già di un indice cluster, rimuoverlo per restituire la tabella a un heap.  
  
 Per rimuovere un heap, creare un indice cluster nell'heap.  
  
 Per ricompilare un heap in modo da recuperare spazio sprecato, creare un indice cluster nell'heap, quindi rimuovere quell'indice.  
  
> [!WARNING]  
>  Per la creazione o la rimozione di indici cluster è richiesta la riscrittura dell'intera tabella. Se la tabella dispone di indici non cluster, è necessario ricrearli tutti ogni volta che l'indice cluster viene modificato. Pertanto, il passaggio da un heap a una struttura di indice cluster o viceversa può richiedere molto tempo e spazio su disco per riordinare i dati in tempdb.  

## <a name="heap-structures"></a>Struttura degli heap


Un heap è una tabella per cui non è disponibile un indice cluster. Agli heap corrisponde una riga in [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)con `index_id = 0` per ogni partizione usata dall'heap. Per impostazione predefinita, a ogni heap è associata una singola partizione. Se a un heap sono associate più partizioni, ognuna di esse ha una struttura di heap contenente i dati per la partizione specifica. Ad esempio, se a un heap sono associate quattro partizioni, saranno presenti quattro strutture di heap, una per ogni partizione.

A seconda dei tipi di dati dell'heap, ogni struttura di heap conterrà una o più unità di allocazione per l'archiviazione e la gestione dei dati di una partizione specifica. Ogni heap conterrà almeno un'unità di allocazione `IN_ROW_DATA` per partizione e un'unità di allocazione `LOB_DATA` per partizione, se l'heap include colonne LOB (Large Object). Conterrà anche un'unità di allocazione `ROW_OVERFLOW_DATA` per partizione, se include colonne a lunghezza variabile che superano il limite della lunghezza di riga di 8.060.

La colonna `first_iam_page` nella vista di sistema `sys.system_internals_allocation_units` punta alla prima pagina IAM nella catena di pagine IAM che gestiscono lo spazio allocato all'heap in una partizione specifica. SQL Server usa le pagine IAM per spostarsi all'interno dell'heap. Le pagine di dati e le righe in esse incluse non sono disposte in base a un ordine specifico e non sono collegate tra loro. L'unico collegamento logico tra le pagine di dati sono le informazioni registrate nelle pagine IAM.

> [!IMPORTANT]  
> La vista di sistema `sys.system_internals_allocation_units` è riservata per il solo uso interno a Microsoft SQL Server. Non è garantita la compatibilità con le versioni future.
 
Le analisi di tabella o le letture seriali dell'heap possono essere eseguite mediante l'analisi delle pagine IAM allo scopo di individuare gli extent che includono le pagine dell'heap. Poiché le pagine IAM rappresentano gli extent nello stesso ordine in cui sono disposti nel file di dati, le analisi seriali dell'heap vengono eseguite progressivamente in ogni file. Inoltre, se si imposta la sequenza di analisi tramite le pagine IAM, le righe dell'heap non vengono in genere restituite in base all'ordine in cui sono state inserite.

La figura seguente illustra l'uso delle pagine IAM nel motore di database di SQL Server per recuperare le righe di dati di un heap relativo a una singola partizione. 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## <a name="related-content"></a>Contenuto correlato  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)     
[Descrizione di indici cluster e non cluster.](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
  
