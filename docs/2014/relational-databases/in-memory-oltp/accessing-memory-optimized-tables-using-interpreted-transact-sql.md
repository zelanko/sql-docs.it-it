---
title: Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c81ac6c0c8dcf7e24c80b426654164c668fcf3a7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62468608"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato
  Salvo poche eccezioni, è possibile accedere alle tabelle ottimizzate per la memoria usando qualsiasi query [!INCLUDE[tsql](../../includes/tsql-md.md)] o operazione DML (SELECT, INSERT, UPDATE o DELETE), batch ad hoc e moduli SQL quali stored procedure, funzioni con valori di tabella, trigger e viste.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato fa riferimento a batch o stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] diverse da stored procedure compilate in modo nativo. L'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato a tabelle ottimizzate per la memoria è denominato accesso di interoperabilità.  
  
 È inoltre possibile accedere alle tabelle con ottimizzazione per la memoria tramite una stored procedure compilata in modo nativo. Le stored procedure compilate in modo nativo sono consigliate in caso di operazioni OLTP critiche per le prestazioni.  
  
 L'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato è consigliato per questi scenari:  
  
-   Query ad hoc e attività amministrative.  
  
-   Query di report in cui in genere vengono utilizzati costrutti non disponibili in stored procedure compilate in modo nativo, ad esempio funzioni finestra.  
  
-   Per eseguire la migrazione di parti dell'applicazione critiche per le prestazioni a tabelle ottimizzate per la memoria, con modifiche minime al codice dell'applicazione o addirittura nessuna. È possibile che si ottengano dei miglioramenti delle prestazioni dalla migrazione delle tabelle. Se quindi si esegue la migrazione di stored procedure a stored procedure compilate in modo nativo, è possibile che si ottengano miglioramenti ulteriori.  
  
-   Quando un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] non è disponibile per stored procedure compilate in modo nativo.  
  
 I costrutti [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti non sono supportati in stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretate mediante le quali si accede ai dati in una tabella ottimizzata per la memoria.  
  
|Area|Non supportato|  
|----------|-----------------|  
|Accesso a tabelle|TRUNCATE TABLE<br /><br /> MERGE (tabella ottimizzata per la memoria come destinazione)<br /><br /> Cursori Dynamic e Keyset (diventano automaticamente Static).<br /><br /> Accesso dai moduli CLR, utilizzando la connessione del contesto.<br /><br /> Riferimento a una tabella ottimizzata per la memoria da una vista indicizzata.|  
|Tra database|Query tra database<br /><br /> Transazioni tra database<br /><br /> Server collegati|  
  
## <a name="table-hints"></a>Hint di tabella  
 Per ulteriori informazioni sugli hint di tabella, vedere Gli [hint di tabella &#40;&#41;Transact-SQL ](/sql/t-sql/queries/hints-transact-sql-table). L'isolamento SNAPSHOT è stato aggiunto per supportare [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
 Gli hint di tabella seguenti non sono supportati quando si accede a una tabella ottimizzata per la memoria utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretato.  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 Quando si accede a una tabella ottimizzata per la memoria da una transazione esplicita o implicita usando [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato, è necessario includere un hint di tabella del livello di isolamento quale SNAPSHOT, REPEATABLEREAD, o SERIALIZABLE oppure usare MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT. Per ulteriori informazioni, vedere [linee guida per i livelli di isolamento delle transazioni con tabelle ottimizzate per la memoria](memory-optimized-tables.md) e [Opzioni ALTER DATABASE set &#40;&#41;Transact-SQL ](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
> [!NOTE]  
>  Un hint del livello di isolamento non è necessario per le tabelle ottimizzate per la memoria accessibili dalle query in esecuzione in modalità autocommit.  
  
## <a name="see-also"></a>Vedi anche  
 [Supporto di Transact-SQL per OLTP in memoria](transact-sql-support-for-in-memory-oltp.md)   
 [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)  
  
  
