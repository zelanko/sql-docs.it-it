---
title: Tabelle con ottimizzazione per la memoria con codice T-SQL interpretato
ms.custom: seo-dt-2019
ms.date: 05/31/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 402b945c68e68f73ba482c20b158f14aba2c818f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412814"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

 Salvo poche eccezioni, è possibile accedere alle tabelle ottimizzate per la memoria usando qualsiasi query [!INCLUDE[tsql](../../includes/tsql-md.md)] o operazione DML (selezione, inserimento, aggiornamento o eliminazione), batch ad hoc e moduli SQL quali stored procedure, funzioni con valori di tabella, trigger e viste.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato fa riferimento a batch o stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] diverse da stored procedure compilate in modo nativo. L'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato a tabelle ottimizzate per la memoria è denominato accesso di interoperabilità.  

A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], le query in [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato possono analizzare le tabelle ottimizzate per la memoria in parallelo, invece che solo in modalità seriale.

È inoltre possibile accedere alle tabelle con ottimizzazione per la memoria tramite una stored procedure compilata in modo nativo. Le stored procedure compilate in modo nativo sono consigliate in caso di operazioni OLTP critiche per le prestazioni.  
  
L'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato è consigliato per questi scenari:  
  
- Query ad hoc e attività amministrative.  
  
- Query di report che in genere usano costrutti non disponibili nelle stored procedure compilate in modo nativo, come le funzioni *finestra* , anche note come funzioni [OVER](../../t-sql/queries/select-over-clause-transact-sql.md) .  
  
- Per eseguire la migrazione di parti dell'applicazione critiche per le prestazioni a tabelle ottimizzate per la memoria, con modifiche minime al codice dell'applicazione o addirittura nessuna. È possibile che si ottengano dei miglioramenti delle prestazioni dalla migrazione delle tabelle. Se quindi si esegue la migrazione di stored procedure a stored procedure compilate in modo nativo, è possibile che si ottengano miglioramenti ulteriori.  
  
- Quando un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] non è disponibile per stored procedure compilate in modo nativo.  
  
Tuttavia, i costrutti [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti non sono supportati in stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretate mediante le quali si accede ai dati in una tabella ottimizzata per la memoria.  
  
|Area|Non supportato|  
|----------|-----------------|  
|Accesso a tabelle|TRUNCATE TABLE<br /><br /> MERGE (tabella ottimizzata per la memoria come destinazione)<br /><br /> Cursori Dynamic e Keyset (diventano automaticamente Static).<br /><br /> Accesso dai moduli CLR, utilizzando la connessione del contesto.<br /><br /> Riferimento a una tabella ottimizzata per la memoria da una vista indicizzata.|  
|Tra database|Query tra database<br /><br /> Transazioni tra database<br /><br /> Server collegati|  
  
## <a name="table-hints"></a>Hint di tabella

Per ulteriori informazioni sugli hint di tabella, vedere [Hint di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md). È stato aggiunto SNAPSHOT per supportare [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
Gli hint di tabella seguenti non sono supportati quando si accede a una tabella ottimizzata per la memoria utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretato.  

  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  

Quando si accede a una tabella ottimizzata per la memoria da una transazione esplicita o implicita usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretato, è necessario eseguire almeno una delle operazioni seguenti:  
  
- Specificare un [hint di tabella del livello di isolamento](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) come SNAPSHOT, REPEATABLEREAD o SERIALIZABLE.  
  
- Impostare l'opzione di database [MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT](../../t-sql/statements/alter-database-transact-sql-set-options.md) su ON.  
  
Un hint di tabella del livello di isolamento non è necessario per le tabelle ottimizzate per la memoria a cui accedono query in esecuzione in [modalità autocommit](https://msdn.microsoft.com/c8de5b60-d147-492d-b601-2eeae8511d00).  
  
## <a name="see-also"></a>Vedere anche

[Supporto di Transact-SQL per OLTP in memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   

[Migrazione a OLTP in memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

