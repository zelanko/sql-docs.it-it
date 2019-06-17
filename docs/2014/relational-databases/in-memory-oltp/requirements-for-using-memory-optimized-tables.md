---
title: Requisiti per l'uso di tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b9e442fb97245d32c398602cdfd727de8239cb8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467897"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>Requisiti per l'utilizzo di tabelle con ottimizzazione per la memoria
  Oltre al [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), di seguito sono i requisiti per utilizzare OLTP In memoria:  
  
-   Versioni Developer, Evaluation o Enterprise Edition a 64 bit di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Memoria sufficiente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per poter usare i dati negli indici e nelle tabelle ottimizzate per la memoria. Per tenere conto delle versioni delle righe, è necessario fornire una quantità di memoria che sia il doppio delle dimensioni previste per gli indici e le tabelle ottimizzate per la memoria. La quantità di memoria effettiva necessaria dipende tuttavia dal carico di lavoro. È consigliabile monitorare l'utilizzo della memoria e apportare modifiche in base alle esigenze. Le dimensioni dei dati nelle tabelle ottimizzate per la memoria non devono superare la percentuale consentita del pool. Per conoscere le dimensioni di una tabella con ottimizzazione per la memoria, vedere [DM db_xtp_table_memory_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql).  
  
     Se nel database sono presenti tabelle basate su disco, è necessario fornire la memoria sufficiente per il pool di buffer e l'elaborazione delle query in quelle tabelle.  
  
     È importante conoscere la quantità di memoria richiesta dall'applicazione OLTP in memoria. Per altre informazioni, vedere [Stimare i requisiti di memoria delle tabelle con ottimizzazione per la memoria](memory-optimized-tables.md) .  
  
-   Spazio libero su disco che sia il doppio delle dimensioni delle tabelle ottimizzate per la memoria durevoli.  
  
-   Un processore deve supportare l'istruzione **cmpxchg16b** per l'utilizzo di OLTP in memoria. Tutti i moderni processori a 64 bit supportano **cmpxchg16b**.  
  
     Se si usano un'applicazione host VM e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene visualizzato un errore causato da un processore di generazione precedente, controllare se nell'applicazione è presente un'opzione di configurazione che consenta l'utilizzo di **cmpxchg16b**. In alternativa, è possibile usare Hyper-V, che supporta **cmpxchg16b** senza la necessità di modificare l'opzione di configurazione.  
  
-   Per installare OLTP in memoria, selezionare **Servizi motore di database** quando si installa [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
     Per installare la generazione di report ([determinare se una tabella o una Stored Procedure deve essere trasferita a OLTP In memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) e [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (per gestire OLTP In memoria tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] Esplora oggetti), selezionare **Management Strumenti-Basic** oppure **strumenti di gestione-avanzati** quando si installa [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>Note importanti sull'uso di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]  
  
-   Le dimensioni totali in memoria di tutte le tabelle durevoli di un database non devono superare i 250 GB. Per altre informazioni, vedere [durabilità per tabelle ottimizzate per la memoria](durability-for-memory-optimized-tables.md).  
  
-   Questo rilascio di [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] è mirato per essere usato in modo ottimale con 2 o 4 socket e meno di 60 core.  
  
-   I file di checkpoint non devono essere eliminati manualmente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue automaticamente il processo di Garbage Collection sui file di checkpoint non necessari. Per altre informazioni, vedere la discussione sull'unione di file di dati e differenziali in [durabilità per tabelle ottimizzate per la memoria](durability-for-memory-optimized-tables.md).  
  
-   Nella prima versione di OLTP in memoria (in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), l'unico modo per rimuovere un filegroup ottimizzato per la memoria consiste nell'eliminare il database.  
  
-   Se si tenta di eliminare un batch di grandi dimensioni di righe mentre è presente un carico di lavoro simultaneo di aggiornamento o inserimento che influisce sull'intervallo di righe che si sta tentando di eliminare, l'eliminazione probabilmente avrà esito negativo. La soluzione alternativa consiste nell'arrestare il carico di lavoro di aggiornamento o inserimento prima di eseguire l'eliminazione. In alternativa, è possibile configurare la transazione in transazioni più piccole, che hanno minore probabilità di essere interrotte da un carico di lavoro simultaneo. Come per tutte le operazioni di scrittura nelle tabelle ottimizzate per la memoria, usare la logica di riesecuzione ([Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)).  
  
-   Se si crea uno o più database con tabelle ottimizzate per la memoria, è consigliabile abilitare l'inizializzazione immediata dei file per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per eseguire tale operazione è necessario concedere all'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il diritto utente SE_MANAGE_VOLUME_NAME. Senza l'inizializzazione immediata dei file, i file di archiviazione ottimizzati per la memoria (file di dati e differenziali) vengono inizializzati al momento della creazione. Tale operazione può causare una riduzione delle prestazioni del carico di lavoro. Per altre informazioni sull'inizializzazione immediata dei file, vedere [Inizializzazione di file di database](../databases/database-instant-file-initialization.md). Per informazioni su come abilitare l'inizializzazione immediata dei file, vedere l'argomento relativo ai [motivi e alle modalità di abilitazione dell'inizializzazione immediata dei file](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="did-this-article-help-you-were-listening"></a>Questo articolo è stato utile? Commenti e suggerimenti  
 Quali informazioni si stanno cercando? La ricerca ha restituito i risultati desiderati? Commenti e suggerimenti per commenti e suggerimenti per migliorare il contenuto. Inviare eventuali commenti all'indirizzo [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page).  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
