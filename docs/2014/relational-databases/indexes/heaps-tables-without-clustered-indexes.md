---
title: Heap (tabelle senza indici cluster) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a39bac2e0352f2adc7749e980d5cc91044f8ab2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025327"
---
# <a name="heaps-tables-without-clustered-indexes"></a>Heap (tabelle senza indici cluster)
  Un heap è una tabella per cui non è disponibile un indice cluster. Nelle tabelle archiviate come heap è possibile creare uno o più indici non cluster. I dati vengono archiviati nell'heap senza un ordine specificato. In genere i dati vengono inizialmente archiviati nell'ordine in cui le righe vengono inserite nella tabella, tuttavia [!INCLUDE[ssDE](../../includes/ssde-md.md)] può spostare i dati nell'heap in modo da archiviare le righe in modo efficiente, pertanto non è possibile prevedere l'ordine dei dati. Per garantire l'ordine delle righe restituite da un heap, è necessario utilizzare la clausola `ORDER BY`. Per specificare l'ordine di archiviazione delle righe, creare un indice cluster nella tabella, in modo che essa non sia un heap.  
  
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
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [Descrizione di indici cluster e non cluster.](clustered-and-nonclustered-indexes-described.md)  
  
  
