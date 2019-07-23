---
title: Esempio di spazio su disco per gli indici | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: caf70d087a7df27248457df40f6ceb4d3ab9e3d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909722"
---
# <a name="index-disk-space-example"></a>Esempio di spazio su disco per gli indici
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ogni volta che viene creato, ricompilato o eliminato un indice, nei file e nei filegroup appropriati è necessario spazio su disco per le strutture di origine (vecchie) e di destinazione (nuove). La struttura di origine non viene deallocata finché non viene eseguito il commit della transazione di creazione dell'indice. Potrebbe essere necessario spazio su disco temporaneo aggiuntivo per le operazioni di ordinamento. Per altre informazioni, vedere [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
 In questo esempio vengono determinati i requisiti di spazio su disco per la creazione di un indice cluster.  
  
 Viene presupposto che le condizioni seguenti siano vere prima della creazione dell'indice cluster:  
  
-   La tabella esistente (heap) contiene 1 milione di righe. Ogni riga è lunga 200 byte.  
  
-   L'indice non cluster A contiene 1 milione di righe. Ogni riga è lunga 50 byte.  
  
-   L'indice non cluster B contiene 1 milione di righe. Ogni riga è lunga 80 byte.  
  
-   L'opzione "index create memory" è impostata su 2 MB.  
  
-   Per tutti gli indici, esistenti e nuovi, il valore del fattore di riempimento è 80. Questo significa che le pagine sono piene all'80 percento.  
  
    > [!NOTE]  
    >  Dopo aver creato un indice cluster, è necessario ricompilare i due indici non cluster per sostituire l'indicatore di riga con la nuova chiave dell'indice cluster.  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>Calcoli dello spazio su disco per un'operazione sull'indice offline  
 Nei passaggi seguenti vengono calcolati sia lo spazio su disco temporaneo da utilizzare durante l'operazione sull'indice, sia lo spazio su disco permanente necessario per l'archiviazione dei nuovi indici. I calcoli illustrati sono approssimativi, cioè i risultati vengono arrotondati per eccesso e vengono considerate solo le dimensioni del livello foglia dell'indice. Per indicare i calcoli approssimati viene utilizzata la tilde (~).  
  
1.  Determinare le dimensioni delle strutture di origine.  
  
     Heap: 1 milione * 200 byte ~ 200 MB  
  
     Indice non cluster A: 1 milione * 50 byte / 80% ~ 63 MB  
  
     Indice non cluster B: 1 milione * 80 byte / 80% ~ 100 MB  
  
     Dimensioni totali delle strutture esistenti: 363 MB  
  
2.  Determinare le dimensioni delle strutture di destinazione. Si presuppone che la nuova chiave cluster sia lunga 24 byte incluso un uniqueifier. L'indicatore di riga (lungo 8 byte) in entrambi gli indici non cluster verrà sostituito da questa chiave di clustering.  
  
     Indice cluster: 1 milione * 200 byte / 80% ~ 250 MB  
  
     Indice non cluster A: 1 milione * (50 - 8 + 24) byte / 80% ~ 83 MB  
  
     Indice non cluster B: 1 milione * (80 - 8 + 24) byte / 80% ~ 120 MB  
  
     Dimensioni totali delle nuove strutture: 453 MB  
  
     Lo spazio su disco totale necessario per supportare entrambe le strutture di origine e di destinazione per la durata dell'operazione sul'indice è di 816 MB (363 + 453). Lo spazio attualmente allocato alle strutture di origine verrà deallocato dopo il commit dell'operazione sull'indice.  
  
3.  Determinare ulteriore spazio su disco temporaneo per l'ordinamento.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     Space requirements are shown for sorting in **tempdb** (with SORT_IN_TEMPDB set to ON) and sorting in the target location (with SORT_IN_TEMPDB set to OFF).  
  
    1.  Quando SORT_IN_TEMPDB è impostato su ON, in **tempdb** deve essere disponibile spazio su disco sufficiente per contenere l'indice di dimensioni maggiori (1 milione * 200 byte ~ 200 MB). Nell'operazione di ordinamento non è considerato il fattore di riempimento.  
  
         Spazio su disco aggiuntivo (nel percorso di **tempdb** ) uguale al valore dell' [opzione di configurazione del server index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         Dimensioni totali dello spazio su disco temporaneo con SORT_IN_TEMPDB impostata su ON ~ 202 MB.  
  
    2.  Quando SORT_IN_TEMPDB è impostato su OFF (impostazione predefinita), per l'ordinamento vengono utilizzati i 250 MB di spazio su disco già considerati per il nuovo indice nel passaggio 2.  
  
         Spazio su disco aggiuntivo (nel percorso di destinazione) uguale al valore dell' [opzione di configurazione del server index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         Dimensioni totali dello spazio su disco temporaneo con SORT_IN_TEMPDB impostato su OFF = 2 MB.  
  
 Se si usa **tempdb**, per creare gli indici cluster e non cluster sarebbero necessari in totale 1018 MB (816 + 202). Con **tempdb** si aumenta la quantità di spazio su disco temporaneo usata per creare un indice, ma può ridursi il tempo necessario per creare un indice quando **tempdb** si trova in un set di dischi diversi da quello del database utente. Per altre informazioni sull'uso di **tempdb**, vedere [Opzione SORT_IN_TEMPDB per gli indici](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 Se non si usa **tempdb**, per creare gli indici cluster e non cluster sarebbero necessari in totale 818 MB (816+ 2).  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>Calcoli dello spazio su disco per un'operazione sull'indice cluster online  
 Quando si crea, elimina o ricompila un indice cluster online, è necessario spazio su disco aggiuntivo per compilare e gestire un indice di mapping temporaneo. L'indice di mapping temporaneo contiene un record per ogni riga della tabella e il suo contenuto è costituito dall'unione delle colonne di segnalibri vecchie e nuove.  
  
 Per calcolare lo spazio su disco necessario per un'operazione sull'indice cluster online, seguire la procedura illustrata per un'operazione su un indice offline e aggiungere i risultati a quelli ottenuti con il passaggio seguente.  
  
-   Determinare lo spazio per l'indice di mapping temporaneo.  
  
     In questo esempio il vecchio segnalibro è l'ID di riga (RID) dell'heap (8 byte) e il nuovo segnalibro è la chiave di clustering (24 byte incluso un **uniqueifier**). Tra i vecchi e i nuovi segnalibri non vi sono colonne sovrapposte.  
  
     Dimensioni dell'indice di mapping temporaneo = 1 milione * (8 byte + 24 byte) / 80% ~ 40 MB.  
  
     Lo spazio su disco deve essere aggiunto allo spazio su disco necessario nel percorso di destinazione se SORT_IN_TEMPDB è impostato su OFF o in **tempdb** se SORT_IN_TEMPDB è impostato su ON.  
  
 Per altre informazioni sull'indice di mapping temporaneo, vedere [Requisiti di spazio su disco per operazioni DLL sugli indici](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="disk-space-summary"></a>Riepilogo dello spazio su disco  
 Nella tabella seguente sono riportati i risultati dei calcoli dello spazio su disco.  
  
|Operazione sull'indice|Requisiti di spazio su disco per i percorsi delle strutture seguenti|  
|---------------------|---------------------------------------------------------------------------|  
|Operazione sull'indice offline con SORT_IN_TEMPDB = ON|Spazio totale durante l'operazione: 1018 MB<br /><br /> \- Tabella e indici esistenti: 363 MB\*<br /><br /> -<br />                    **tempdb**: 202 MB*<br /><br /> \- Nuovi indici: 453 MB<br /><br /> Spazio totale necessario dopo l'operazione: 453 MB|  
|Operazione sull'indice offline con SORT_IN_TEMPDB = OFF|Spazio totale durante l'operazione: 816 MB<br /><br /> \- Tabella e indici esistenti: 363 MB*<br /><br /> \- Nuovi indici: 453 MB<br /><br /> Spazio totale necessario dopo l'operazione: 453 MB|  
|Operazione sull'indice online con SORT_IN_TEMPDB = ON|Spazio totale durante l'operazione: 1058 MB<br /><br /> \- Tabella e indici esistenti: 363 MB\*<br /><br /> -<br />                    **tempdb** (include l'indice di mapping): 242 MB*<br /><br /> \- Nuovi indici: 453 MB<br /><br /> Spazio totale necessario dopo l'operazione: 453 MB|  
|Operazione sull'indice online con SORT_IN_TEMPDB = OFF|Spazio totale durante l'operazione: 856 MB<br /><br /> \- Tabella e indici esistenti: 363 MB*<br /><br /> -Indice di mapping temporaneo: 40 MB\*<br /><br /> \- Nuovi indici: 453 MB<br /><br /> Spazio totale necessario dopo l'operazione: 453 MB|  
  
 *Questo spazio viene deallocato dopo il commit dell'operazione sull'indice.  
  
 In questo esempio non viene considerato lo spazio su disco temporaneo aggiuntivo necessario in **tempdb** per i record delle versioni creati dalle operazioni simultanee di aggiornamento ed eliminazione.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Spazio su disco per il log delle transazioni per operazioni sugli indici](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
