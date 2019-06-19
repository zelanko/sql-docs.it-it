---
title: Linee guida per i livelli di isolamento delle transazioni con tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26f0193d40a01858bc3fe651a23b389a4ffcb6ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779156"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>Linee guida per i livelli di isolamento delle transazioni con tabelle con ottimizzazione per la memoria
  In molti scenari è necessario specificare il livello di isolamento. L'isolamento delle transazioni per le tabelle ottimizzate per la memoria è diverso dalle tabelle basate su disco.  
  
 Requisiti per specificare il livello di isolamento:  
  
-   TRANSACTION ISOLATION LEVEL è un'opzione obbligatoria per il blocco ATOMIC che include il contenuto di una stored procedure compilata in modo nativo.  
  
-   A causa delle restrizioni sull'utilizzo del livello di isolamento nelle transazioni tra contenitori, l'utilizzo di tabelle ottimizzate per la memoria in codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato deve essere spesso accompagnato da un hint di tabella che specifica il livello di isolamento utilizzato per accedere alla tabella. Per altre informazioni sull'hint del livello di isolamento e transazioni tra contenitori, vedere [livelli di isolamento delle transazioni](../../2014/database-engine/transaction-isolation-levels.md).  
  
-   Il livello di isolamento delle transazioni desiderato deve essere dichiarato in modo esplicito. Non è possibile utilizzare hint di blocco (ad esempio XLOCK) per garantire l'isolamento di determinate righe o tabelle nella transazione.  
  
-   Per l'applicazione che accede al database deve essere implementata la logica di riesecuzione per gestire gli errori risultanti da conflitti alla fine della transazione, gli errori di convalida e gli errori di dipendenza di commit. Si noti che gli errori di dipendenza di commit possono verificarsi anche con transazioni di sola lettura.  
  
-   Con le tabelle ottimizzate per la memoria è opportuno evitare transazioni con esecuzione prolungata. Tali transazioni aumentano la probabilità di conflitti e la conseguente interruzione della transazione. Una transazione con esecuzione prolungata può posticipare il processo di Garbage Collection. Più lunga è l'esecuzione di una transazione, più a lungo OLTP in memoria mantiene le versioni delle righe eliminate di recente; questo può ridurre le prestazioni di ricerca di nuove transazioni.  
  
 Le tabelle basate su disco in genere si basano sul blocco per l'isolamento delle transazioni. Le tabelle con ottimizzazione per la memoria si basano sul controllo di più versioni e sul rilevamento dei conflitti per garantire l'isolamento. Per informazioni dettagliate, vedere la sezione sul rilevamento dei conflitti, convalida e controlli di dipendenza di Commit in [transazioni in tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Le tabelle basate su disco consentono il controllo di più versioni con i livelli di isolamento SNAPSHOT e READ_COMMITTED_SNAPSHOT. Per le tabelle ottimizzate per la memoria tutti i livelli di isolamento sono basati su più versioni, inclusi REPEATABLE READ e SERIALIZABLE.  
  
## <a name="types-of-transactions"></a>Tipi di transazioni  
 Ogni query in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene eseguita nel contesto di una transazione.  
  
 Sono disponibili tre tipi di transazioni in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Transazioni con autocommit. Se non esiste un contesto di transazione attiva e le transazioni implicite non sono impostate su ON nella sessione, ogni query dispone del proprio contesto di transazione. La transazione viene avviata quando l'istruzione avvia l'esecuzione e viene completata quando termina l'istruzione.  
  
-   Transazioni esplicite. L'utente avvia la transazione tramite un'istruzione esplicita BEGIN TRAN o BEGIN ATOMIC. La transazione viene completata in base alle corrispondenti istruzioni COMMIT e ROLLBACK o END (nel caso di un blocco atomic).  
  
-   Transazioni implicite. Quando l'opzione SET IMPLICIT_TRANSACTIONS è impostata su ON, viene avviata implicitamente una transazione ogni volta che l'utente esegue un'istruzione e non è presente alcun contesto di transazione attiva. La transazione viene completata tramite istruzioni COMMIT e ROLLBACK esplicite.  
  
## <a name="baseline-read-committed-isolation"></a>Isolamento READ COMMITTED di base  
 READ COMMITTED è il livello di isolamento predefinito in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Il livello di isolamento READ COMMITTED garantisce che le transazioni non possano visualizzare dati di cui non è stato eseguito il commit a seguito delle modifiche all'esterno della transazione corrente. In altre parole, la transazione legge solo i dati di cui è stato eseguito il commit nel database o che sono stati modificati dalla transazione corrente.  
  
 Tutti i livelli di isolamento supportati per le tabelle ottimizzate per la memoria forniscono Read Committed garantito. Pertanto, se la transazione non richiede garanzie maggiori, è possibile utilizzare uno dei livelli di isolamento supportati per le tabelle ottimizzate per la memoria. SNAPSHOT utilizza la minore quantità delle risorse di sistema, rispetto agli altri livelli di isolamento.  
  
 La garanzia offerta dal livello di isolamento SNAPSHOT (il livello più basso di isolamento supportato per le tabelle ottimizzate per la memoria) include le garanzie di READ COMMITTED. Ogni istruzione della transazione legge la stessa versione coerente del database. Non solo tutte le righe vengono lette dalla transazione di cui è stato eseguito il commit nel database, ma anche tutte le operazioni di lettura rilevano il set di modifiche apportate dallo stesso set di transazioni.  
  
 **Linee guida**: Se solo la garanzia di isolamento READ COMMITTED è necessaria, utilizzare l'isolamento SNAPSHOT con le stored procedure compilate in modo nativo e per l'accesso a tabelle ottimizzate per la memoria tramite interpretato [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
 Per le transazioni in modalità autocommit, viene eseguito il mapping implicito del livello di isolamento READ COMMITTED a SNAPSHOT per le tabelle ottimizzate per la memoria. Pertanto, se il valore della sessione TRANSACTION ISOLATION LEVEL è impostato su READ COMMITTED, non è necessario specificare il livello di isolamento tramite un hint di tabella durante l'accesso alle tabelle ottimizzate per la memoria.  
  
 Nell'esempio di transazione in modalità autocommit seguente viene illustrato un join tra una tabella Customers ottimizzata per la memoria e una tabella normale [Order History], come parte di un batch ad hoc:  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 Nell'esempio di transazioni esplicite o implicite riportato di seguito viene illustrato lo stesso join, ma questa volta a una transazione utente esplicita. L'accesso alla tabella ottimizzata per la memoria Customers viene effettuato nel livello di isolamento SNAPSHOT, come indicato tramite l'hint di tabella WITH (SNAPSHOT), mentre l'accesso alla tabella normale [Order History] viene effettuato con il livello di isolamento READ COMMITTED:  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>Differenze operative  
 Oltre alla garanzia READ COMMITTED, sono inoltre disponibili due dettagli di implementazione chiave che possono essere utilizzati nelle applicazioni utilizzano tabelle basate su disco. Considerare i seguenti fattori durante la conversione di una tabella basata su disco a cui si accede tramite isolamento READ COMMITTED in una tabella ottimizzata per la memoria a cui si accede con l'isolamento SNAPSHOT:  
  
-   Nell'implementazione del livello di isolamento READ COMMITTED per le tabelle basate su disco (presupponendo che READ_COMMITTED_SNAPSHOT sia impostato su OFF) vengono utilizzati blocchi per evitare conflitti tra lettori e writer. Quando un writer avvia l'aggiornamento di una riga, accetta un blocco e non lo rilascia finché non viene eseguito il commit della transazione. Tutte le operazioni di lettura vengono bloccate in attesa che venga eseguito il commit della transazione di scrittura.  
  
     In alcune applicazioni è possibile che venga presupposto che i lettori attendano sempre i writer per eseguire il commit, in particolare in presenza di un'eventuale sincronizzazione tra le due transazioni nel livello applicazione.  
  
     **Linee guida:** Le applicazioni non possono basarsi sul comportamento di blocco. Se un'applicazione richiede la sincronizzazione tra transazioni simultanee, tale logica può essere implementata nel livello applicazione o del livello di database, tramite [sp_getapplock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql).  
  
-   Nelle transazioni che utilizzano l'isolamento READ COMMITTED ogni istruzione rileva la versione più recente delle righe nel database. Pertanto, le istruzioni successive rilevano le modifiche apportate nello stato del database.  
  
     Il polling di una tabella utilizzando un loop WHILE fino a trovare una nuova riga è un esempio di modello applicativo che utilizza questo presupposto. A ogni iterazione del ciclo la query rileverà gli aggiornamenti più recenti nel database.  
  
     **Linee guida:** Se un'applicazione deve eseguire il polling di una tabella con ottimizzazione per la memoria per ottenere le righe più recenti scritte nella tabella, spostare il ciclo di polling all'esterno dell'ambito della transazione.  
  
     Di seguito è riportato un modello di un'applicazione di esempio che utilizza questo presupposto. Eseguire il polling di una tabella utilizzando un ciclo WHILE fino a trovare una nuova riga. In ogni iterazione del ciclo la query accederà agli aggiornamenti più recenti nel database.  
  
 Nel seguente script di esempio viene eseguito il polling di una tabella t1 fino a trovare una riga. Viene quindi rimossa una singola riga dalla tabella per un'ulteriore elaborazione.  
  
 Si noti che la logica di polling deve essere all'esterno dell'ambito della transazione, poiché utilizza l'isolamento Snapshot per accedere alla tabella t1. L'utilizzo della logica di polling all'interno dell'ambito di una transazione crea una transazione con esecuzione prolungata, quindi è sconsigliata.  
  
```sql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>Hint di tabella di blocco  
 Gli hint di blocco ([hint per la tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)) come HOLDLOCK e XLOCK è utilizzabile con le tabelle basate su disco per avere [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengano eseguiti più blocchi di quelli necessari per il livello di isolamento specificato.  
  
 I blocchi non vengono utilizzati per le tabelle con ottimizzazione per la memoria. I livelli di isolamento più elevati quali REPEATABLE READ e SERIALIZABLE possono essere utilizzati per dichiarare le garanzie desiderate.  
  
 Gli hint di blocco non sono supportati. In alternativa, è possibile dichiarare le garanzie necessarie tramite i livelli di isolamento delle transazioni. NOLOCK è supportato poiché [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non accetta blocchi sulle tabelle ottimizzate per la memoria. Si noti che, diversamente dalle tabelle basate su disco, NOLOCK non implica il comportamento READ UNCOMMITTED per le tabelle ottimizzate per la memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle transazioni nelle tabelle ottimizzate per la memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Linee guida per la logica di riesecuzione per le transazioni nelle tabelle ottimizzate per la memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [Livelli di isolamento delle transazioni](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
