---
title: Transazioni tra contenitori | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40420db76ee8ce5b1fcf1d085a78d7b17690105d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538588"
---
# <a name="cross-container-transactions"></a>Transazioni tra contenitori
  Le transazioni tra contenitori sono transazioni utente implicite o esplicite che includono chiamate a stored procedure compilate in modo nativo o operazioni in tabelle ottimizzate per la memoria.  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] le chiamate a stored procedure non avviano una transazione. Le esecuzioni di stored procedure compilate in modo nativo in modalità autocommit, non nel contesto di una transazione utente, non vengono considerate transazioni tra contenitori.  
  
 Qualsiasi query interpretata che faccia riferimento a tabelle ottimizzate per la memoria viene considerata parte di una transazione tra contenitori, sia che venga eseguita da una transazione esplicita o implicita sia in modalità autocommit.  
  
##  <a name="isolation"></a> Isolamento di singole operazioni  
 A ogni transazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è associato un livello di isolamento. Il livello di isolamento predefinito è READ COMMITTED. Per usare un livello di isolamento diverso, è possibile impostare il livello di isolamento utilizzando [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 È spesso necessario effettuare operazioni in tabelle ottimizzate per la memoria in un livello di isolamento diverso dalle operazioni in tabelle basate su disco. In una transazione è possibile impostare un livello di isolamento diverso per una raccolta di istruzioni o per una singola operazione di lettura.  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>Specifica del livello di isolamento di singole operazioni  
 Per impostare un livello di isolamento diverso per un set di istruzioni in una transazione, è possibile utilizzare `SET TRANSACTION ISOLATION LEVEL`. Nell'esempio di una transazione riportato di seguito viene utilizzato il livello di isolamento SERIALIZABLE per impostazione predefinita. Le operazioni INSERT e SELECT in t3, t2 e t1 vengono eseguite con livello di isolamento REPEATABLE READ.  
  
```tsql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 Per impostare un livello di isolamento per singole operazioni di lettura diverso da quello predefinito della transazione, è possibile utilizzare un hint di tabella (ad esempio, serializable). Ogni operazione SELECT corrisponde a un'operazione READ e ogni UPDATE e DELETE corrisponde a un'operazione READ, poiché la riga deve sempre essere letta prima che sia possibile aggiornarla o eliminarla. Per le operazioni INSERT non è disponibile un livello di isolamento, perché le scritture vengono sempre isolate in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Nell'esempio seguente il livello di isolamento predefinito per la transazione è READ COMMITTED, ma l'accesso viene effettuato alla tabella t1 con isolamento SERIALIZABLE e alla tabella t2 con isolamento SNAPSHOT.  
  
```tsql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>Semantica di isolamento per singole operazioni  
 Una transazione T serializzabile viene eseguita in isolamento completo. È come se per tutte le altre transazioni fosse stato eseguito il commit prima dell'avvio di T o l'avvio dopo il commit di T. Il comportamento diventa più complesso quando operazioni diverse in una transazione presentano livelli di isolamento diversi.  
  
 La semantica generale dei livelli di isolamento delle transazioni in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], insieme alle implicazioni sul blocco, è illustrato nella [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 Per le transazioni tra contenitori in cui operazioni diverse possono avere livelli di isolamento diversi, è necessario comprendere la semantica di isolamento delle singole operazioni di lettura. Le operazioni di scrittura sono sempre isolate. Le scritture in transazioni diverse non possono avere un'influenza reciproca.  
  
 Un'operazione di lettura dei dati restituisce un numero di righe che soddisfa una condizione di filtro.  
  
 Operazioni di lettura vengono eseguite come parte di una transazione T. dei livelli di isolamento per le operazioni di lettura può essere riconosciute in termini di,  
  
 Stato di commit  
 Lo stato di commit indica se il commit dei dati letti è garantito.  
  
 Coerenza (transazionale)  
 La coerenza transazionale per un set di letture indica se per tutte le versioni delle righe lette è garantita l'inclusione di aggiornamenti esattamente dallo stesso set di transazioni.  
  
 Garanzie di stabilità per i dati letti fornite automaticamente alla transazione T.  
 La stabilità indica se operazioni di lettura della transazione sono ripetibili. ovvero se in caso di ripetizione di tali operazioni verrebbero restituite le stesse righe e le stesse versioni di riga.  
  
 Alcune garanzie fanno riferimento all'ora di fine logica della transazione. L'ora di fine logica è in genere l'ora in cui viene eseguito il commit della transazione nel database. Se la transazione accede a tabelle ottimizzate per la memoria, l'ora di fine logica è tecnicamente l'inizio della fase di convalida. (Per altre informazioni, vedere la discussione su durata delle transazioni nel [transazioni in tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Indipendentemente dal livello di isolamento, in una transazione (T) vengono sempre rilevati i relativi aggiornamenti:  
  
 READ UNCOMMITTED  
 I dati letti non possono essere sottoposti a commit, né possono essere coerenti o stabili. Saranno tuttavia incluse le operazioni di scrittura precedenti eseguite da T.  
  
 READ COMMITTED  
 Per i dati letti verrà eseguito il commit.  
  
 SNAPSHOT  
 Tutte le operazioni di lettura eseguite da T nel livello di isolamento SNAPSHOT hanno la stessa ora di lettura logica, che corrisponde all'inizio della transazione. Vengono garantiti il commit e la coerenza dei dati letti dall'ora di lettura logica. È garantita la restituzione dello stesso risultato dalla ripetizione di una lettura dall'ora di lettura originale.  
  
 REPEATABLE READ  
 Vengono garantiti il commit e la stabilità dei dati letti fino all'ora di fine logica della transazione.  
  
 SERIALIZABLE  
 Tutte le garanzie di REPEATABLE READ oltre a scarto di righe fantasma e coerenza transazionale rispetto a tutte le operazioni di lettura serializzabili eseguite da T. fantasma prevenzione significa che l'operazione di analisi può restituire solo le righe aggiuntive scritte da T, ma nessuna righe scritte da altre transazioni.  
  
 Si consideri la transazione seguente:  
  
```tsql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 In questa transazione vengono eliminate tutte le righe da t3 nel livello di isolamento READ COMMITTED, vengono copiate tutte le righe da t1 a t3 nel livello di isolamento SERIALIZABLE, quindi vengono confrontate t1 e t3. È possibile che alcune righe [non in t1] siano state aggiunte a t3 poiché la tabella è stata svuotata. Nessuna riga è stata aggiunta a t1 in quanto la copia era SERIALIZABLE.  
  
 Sebbene lettura da t1 alla fine della transazione sia sintatticamente READ COMMITTED, è in effetti SERIALIZABLE, perché la stessa lettura è stata eseguita in precedenza nella transazione nel livello di isolamento SERIALIZABLE: la serializzabilità garantisce che se la lettura viene eseguita in qualsiasi momento successivo della transazione, verranno restituite le stesse righe.  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>Transazioni tra contenitori e livelli di isolamento  
 È possibile considerare una transazione tra contenitori come se fosse costituita da due lati: uno basato su disco (per le operazioni nelle tabelle basate su disco) e uno ottimizzato per la memoria (per le operazioni nelle tabelle ottimizzate per la memoria). Questi due lati possono avere livelli di isolamento diversi. Infatti, alle singole operazioni di lettura in ogni lato possono essere assegnati livelli di isolamento diversi.  
  
 Il lato basato su disco di una transazione T specificata raggiunge un determinato livello di isolamento X se viene soddisfatta una delle condizioni indicate di seguito:  
  
-   Inizia in X. Vale a dire l'impostazione predefinita della sessione era X, perché è stata eseguita `SET TRANSACTION ISOLATION LEVEL`, o è il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] predefinito.  
  
-   Durante la transazione il livello di isolamento predefinito viene modificato in X utilizzando `SET TRANSACTION ISOLATION LEVEL`.  
  
-   Un'operazione di lettura in una tabella basata su disco viene eseguita nel livello di isolamento X, utilizzando la sintassi `WITH (X)`.  
  
 Il lato ottimizzato per la memoria di T raggiunge un livello di isolamento Y se durante l'esecuzione di T una qualsiasi operazione di lettura in una tabella ottimizzata per la memoria o una stored procedure compilata in modo nativo viene eseguita nel livello di isolamento Y.  
  
 Si consideri la transazione di esempio riportata di seguito. In questo caso, t1 e t2 sono tabelle basate su disco e t3 e t4 sono tabelle ottimizzate per la memoria.  
  
 Il lato basato su disco della transazione raggiunge il livello di isolamento READ COMMITTED, perché inizia in tale livello. Il lato basato su disco raggiunge inoltre il livello REPEATABLE READ, in quanto la prima operazione di lettura viene eseguita in tale livello di isolamento. L'eliminazione alla fine della transazione viene eseguita nel livello di isolamento READ COMMITTED e pertanto non introduce un nuovo livello di isolamento.  
  
 Il lato ottimizzato per la memoria della transazione può raggiungere uno dei due livelli: se condition1 è true, raggiunge il livello SERIALIZABLE, mentre se è false, raggiunge solo l'isolamento SNAPSHOT.  
  
```tsql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>Livelli di isolamento supportati per le transazioni tra contenitori  
 Sono presenti limitazioni per i livelli di isolamento utilizzati con operazioni in tabelle ottimizzate per la memoria nelle transazioni tra contenitori.  
  
 Le tabelle con ottimizzazione per la memoria supportano i livelli di isolamento SNAPSHOT, REPEATABLE READ e SERIALIZABLE. Per le transazioni in modalità autocommit, nelle tabelle ottimizzate per la memoria è supportato il livello di isolamento READ COMMITTED.  
  
 Sono supportati gli scenari indicati di seguito:  
  
-   Le transazioni tra contenitori READ UNCOMMITTED, READ COMMITTED e READ_COMMITTED_SNAPSHOT possono accedere alle tabelle ottimizzate per la memoria con livello di isolamento SNAPSHOT, REPEATABLE READ e SERIALIZABLE. Viene rispettata la garanzia READ COMMITTED per la transazione; per tutte le righe lette dalla transazione è stato eseguito il commit nel database.  
  
-   Le transazioni tra contenitori REPEATABLE READ e SERIALIZABLE possono accedere a tabelle ottimizzate per la memoria con isolamento SNAPSHOT.  
  
## <a name="read-only-cross-container-transactions"></a>Transazioni tra contenitori di sola lettura  
 Per la maggior parte delle transazioni di sola lettura in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene eseguito il rollback in fase di commit. Poiché non sono presenti modifiche di cui eseguire il commit nel database, le risorse utilizzate dalla transazione vengono semplicemente liberate automaticamente. Per le transazioni di sola lettura basate su disco, gli eventuali blocchi eseguiti dalla transazione vengono rilasciati in questa fase. Per le transazioni ottimizzate per la memoria di sola lettura che interessano l'esecuzione di una singola stored procedure compilata in modo nativo non viene eseguita alcuna convalida.  
  
 Per le transazioni tra contenitori di sola lettura nella modalità autocommit viene eseguito semplicemente il rollback alla fine della transazione. Non viene eseguita alcuna convalida.  
  
 Le transazioni tra contenitori di sola lettura implicite o esplicite eseguono la convalida in fase di commit se la transazione accede alle tabelle ottimizzate per la memoria nell'isolamento REPEATABLE READ o SERIALIZABLE. Per informazioni dettagliate sulla convalida vedere la sezione sul rilevamento dei conflitti, convalida, e dipendenza di Commit consente di archiviare [transazioni in tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle transazioni nelle tabelle ottimizzate per la memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Linee guida per i livelli di isolamento delle transazioni con tabelle ottimizzate per la memoria](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [Linee guida per la logica di riesecuzione per le transazioni in tabelle con ottimizzazione per la memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
