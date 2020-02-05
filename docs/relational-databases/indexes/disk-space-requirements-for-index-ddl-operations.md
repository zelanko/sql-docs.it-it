---
title: Requisiti di spazio su disco per operazioni DLL sugli indici | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e49ef1ad379f675ca457f8cd9c82a5e4ecc3fd04
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68107129"
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>Requisiti di spazio su disco per operazioni DLL sugli indici
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Lo spazio su disco è un fattore che richiede particolare considerazione in fase di creazione, ricompilazione o eliminazione di indici. Uno spazio su disco non adeguato può comportare una riduzione delle prestazioni o provocare un errore dell'operazione sull'indice. In questo argomento vengono fornite informazioni generali utili per determinare la quantità di spazio su disco necessaria per operazioni DLL (Data Definition Language) sugli indici.  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>Operazioni sugli indici che non richiedono spazio su disco aggiuntivo  
 Le operazioni seguenti non richiedono spazio su disco aggiuntivo:  
  
-   ALTER INDEX REORGANIZE. È tuttavia richiesto spazio nel log.  
  
-   DROP INDEX quando si elimina un indice non cluster.  
  
-   DROP INDEX quando si elimina un indice cluster offline senza specificare la clausola MOVE TO e non sono presenti indici non cluster.  
  
-   CREATE TABLE (vincoli PRIMARY KEY o UNIQUE)  
  
## <a name="index-operations-that-require-additional-disk-space"></a>Operazioni sugli indici che richiedono spazio su disco aggiuntivo  
 Tutte le altre operazioni DLL sugli indici richiedono spazio su disco aggiuntivo temporaneo da utilizzare durante l'operazione e spazio su disco permanente per l'archiviazione della nuova o delle nuove strutture dell'indice.  
  
 Quando viene creata una nuova struttura dell'indice, è necessario spazio su disco per la struttura vecchia (origine) e per quella nuova (destinazione) nei file e filegroup appropriati. La struttura di origine non viene deallocata finché non viene eseguito il commit della transazione di creazione dell'indice.  
  
 Le operazioni DLL sugli indici seguenti comportano la creazione di nuove strutture dell'indice e richiedono spazio su disco aggiuntivo:  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT (PRIMARY KEY o UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT (PRIMARY KEY o UNIQUE) quando il vincolo è basato su un indice cluster  
  
-   DROP INDEX MOVE TO (solo per indici cluster)  
  
## <a name="temporary-disk-space-for-sorting"></a>Spazio su disco temporaneo per l'ordinamento  
 Oltre allo spazio su disco necessario per le strutture di origine e di destinazione, è necessario spazio su disco temporaneo per l'ordinamento, a meno che tramite Query Optimizer non venga individuato un piano di esecuzione che non richiede l'ordinamento.  
  
 L'ordinamento, se necessario, viene eseguito in un nuovo indice per volta. Quando, ad esempio, si ricompilano un indice cluster e gli indici non cluster associati in una singola istruzione, gli indici vengono ordinati uno dopo l'altro. Lo spazio su disco aggiuntivo temporaneo necessario per l'ordinamento corrisponde pertanto alle dimensioni dell'indice di dimensioni maggiori coinvolto nell'operazione, che è solitamente l'indice cluster.  
  
 Se l'opzione SORT_IN_TEMPDB è impostata su ON, l'indice di dimensioni maggiori deve poter essere contenuto in **tempdb**. Sebbene questa opzione comporti l'aumento della quantità di spazio su disco temporaneo necessario per creare un indice, potrebbe consentire di ridurre il tempo necessario per questa operazione quando **tempdb** si trova in un set di dischi diverso da quello in cui si trova il database utente.  
  
 Se l'opzione SORT_IN_TEMPDB è impostata su OFF, ovvero il valore predefinito, ogni indice, inclusi gli indici partizionati, viene archiviato nel relativo spazio su disco di destinazione ed è necessario solo lo spazio su disco per le nuove strutture dell'indice.  
  
 Per un esempio di calcolo dello spazio su disco, vedere [Esempio di spazio su disco per gli indici](../../relational-databases/indexes/index-disk-space-example.md).  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>Spazio su disco temporaneo per operazioni sugli indici online  
 Quando si eseguono operazioni sugli indici online, è necessario spazio su disco aggiuntivo temporaneo.  
  
 Quando viene creato, ricompilato o eliminato un indice cluster online, viene creato un indice non cluster temporaneo per l'esecuzione del mapping tra vecchi segnalibri e nuovi segnalibri. Se l'opzione SORT_IN_TEMPDB è impostata su ON, questo indice temporaneo viene creato in **tempdb**. Se l'opzione SORT_IN_TEMPDB è impostata su OFF, viene utilizzato lo stesso filegroup o schema di partizione dell'indice di destinazione. L'indice di mapping temporaneo contiene un record per ogni riga della tabella e i contenuti sono costituiti dall'unione delle colonne di segnalibri vecchi e nuovi, inclusi uniqueifier e identificatori di record e includono una singola copia di ogni colonna utilizzata in entrambi i segnalibri. Per altre informazioni sulle operazioni online sugli indici, vedere [Eseguire operazioni online sugli indici](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  Non è possibile impostare l'opzione SORT_IN_TEMPDB per le istruzioni DROP INDEX. L'indice di mapping temporaneo viene sempre creato nello stesso filegroup o schema di partizione dell'indice di destinazione.  
  
 Nelle operazioni sugli indici online viene utilizzato il controllo delle versioni delle righe per isolare le operazioni dagli effetti delle modifiche apportate da altre transazioni. In questo modo, non è necessario richiedere blocchi di condivisione sulle righe lette. Le operazioni utente simultanee di aggiornamento ed eliminazione durante le operazioni sugli indici online richiedono spazio per i record di versione in **tempdb**. Per altre informazioni, vedere [Eseguire operazioni online sugli indici](../../relational-databases/indexes/perform-index-operations-online.md) .  
  
## <a name="related-tasks"></a>Attività correlate  
 [Esempio di spazio su disco per gli indici](../../relational-databases/indexes/index-disk-space-example.md)  
  
 [Spazio su disco per il log delle transazioni per operazioni sugli indici](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
 [Stimare le dimensioni di una tabella](../../relational-databases/databases/estimate-the-size-of-a-table.md)  
  
 [Stima delle dimensioni di un indice cluster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)  
  
 [Stima delle dimensioni di un indice non cluster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [Stimare le dimensioni di un heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [Specificare un fattore di riempimento per un indice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
 [Riorganizzare e ricompilare gli indici](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
  
