---
title: Le transazioni nelle tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2cd07d26-a1f1-4034-8d6f-f196eed1b763
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc72eeeb154749b0e889b495fab79bb8bf86db10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843102"
---
# <a name="transactions-in-memory-optimized-tables"></a>Transazioni in tabelle con ottimizzazione per la memoria
  Il controllo delle versioni delle righe nelle tabelle basate su disco (tramite l'isolamento SNAPSHOT o READ_COMMITTED_SNAPSHOT) fornisce una forma di controllo della concorrenza ottimistica. Lettori e writer non si bloccano reciprocamente. Con le tabelle ottimizzate per la memoria i writer non bloccano writer. Nel caso di controllo delle versioni delle righe in tabelle basate su disco, una transazione blocca la riga e il tentativo di aggiornare la riga da parte di transazioni simultanee viene impedito. Per le tabelle ottimizzate per la memoria non vengono attivati blocchi. Al contrario, se due transazioni tentano di aggiornare la stessa riga, si verificherà un conflitto di scrittura/scrittura (errore 41302).  
  
 Diversamente dalle tabelle basate su disco, le tabelle ottimizzate per la memoria prevedono il controllo della concorrenza ottimistica con livelli di isolamento più elevati, REPEATABLE READ e SERIALIZABLE. Non vengono utilizzati blocchi per applicare i livelli di isolamento. Al contrario, alla fine della transazione una convalida garantisce i presupposti di REPEATABLE READ o SERIALIZABLE. Se i presupposti vengono violati, la transazione viene terminata. Per altre informazioni, vedere [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md).  
  
 Di seguito è indicata la semantica delle transazioni importante per le tabelle ottimizzate per la memoria:  
  
-   Controllo di più versioni  
  
-   Isolamento di transazioni basato su snapshot  
  
-   Optimistic  
  
-   Rilevamento dei conflitti  
  
 Nelle sezioni seguenti viene descritto ciascun aspetto di tale semantica.  
  
## <a name="multi-versioning-in-memory-optimized-tables"></a>Controllo di più versioni nelle tabelle con ottimizzazione per la memoria  
 Per le righe delle tabelle ottimizzate per la memoria possono essere presenti diverse versioni. Le transazioni simultanee accedono potenzialmente a diverse versioni della stessa riga.  
  
 I dati delle tabelle con ottimizzazione per la memoria sono basati sulla versione. Possono essere presenti diverse versioni di una riga valide in date e ore specifiche. Le tabelle basate su disco mantengono diverse versioni di riga quando READ_COMMITTED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION è impostato su ON. Le tabelle con ottimizzazione per la memoria mantengono diverse versioni di riga, anche se READ_COMMITTED_SNAPSHOT e ALLOW_SNAPSHOT_ISOLATION sono impostati su OFF. Le versioni di riga delle tabelle ottimizzate per la memoria non vengono mantenute in tempdb, bensì inline, come parte delle strutture dei dati ottimizzate per la memoria in cui sono archiviate le righe.  
  
## <a name="snapshot-based-transaction-isolation-for-memory-optimized-tables"></a>Isolamento delle transazioni basato su snapshot per le tabelle con ottimizzazione per la memoria  
 Tutte le operazioni in una singola transazione utilizzano lo stesso snapshot coerente a livello di transazione delle tabelle ottimizzate per la memoria. Tutto l'isolamento delle transazioni per le tabelle ottimizzate per la memoria è basato su snapshot. Per una transazione che, ad esempio, utilizza il livello di isolamento serializzabile per accedere alle tabelle ottimizzate per la memoria, tutte le operazioni verranno eseguite nello stesso snapshot coerente a livello di transazione.  
  
 Per le transazioni che accedono a tabelle ottimizzate per la memoria viene utilizzato questo controllo delle versioni delle righe per ottenere uno snapshot coerente a livello di transazione delle righe incluse nelle tabelle. I dati letti da qualsiasi istruzione inclusa nella transazione rappresenteranno la versione coerente a livello di transazione dei dati esistenti al momento dell'avvio della transazione. Di conseguenza, eventuali modifiche eseguite da transazioni in esecuzione simultanea non saranno visibili alle istruzioni nella transazione corrente.  
  
## <a name="optimistic-concurrency-control-for-memory-optimized-tables"></a>Controllo della concorrenza ottimistica per le tabelle con ottimizzazione per la memoria  
 Conflitti ed errori sono rari. Nelle transazioni in tabelle ottimizzate per la memoria si presuppone che non siano presenti conflitti con le transazioni simultanee e che le operazioni abbiano esito positivo. Le transazioni non utilizzano blocchi o latch nella tabella ottimizzata per la memoria per garantire l'isolamento delle transazioni. I lettori non vengono bloccati dai writer. I writer non vengono bloccati dai writer. Al contrario, l'esecuzione delle transazioni procede nel presupposto ottimistico che non saranno presenti conflitti con altre transazioni. Il fatto di non utilizzare blocchi e latch e di non attendere che venga completata l'elaborazione delle stesse righe da parte di altre transazioni migliora le prestazioni.  
  
 Se inoltre una transazione (TxA) legge righe che sono state inserito o modificate da un'altra transazione (TxB) che sono in fase di commit, verrà applicato il presupposto ottimistico che l'altra transazione sarà sottoposta a commit, anziché attendere l'esecuzione del commit. In questo caso, la transazione TxA avrà una dipendenza di commit dalla transazione TxB.  
  
## <a name="conflict-detection-validation-and-commit-dependency-checks"></a>Controlli relativi a rilevamento di conflitti, convalida e dipendenza di commit  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono rilevati i conflitti tra le transazioni simultanee, nonché le violazioni del livello di isolamento, e viene eliminata una delle transazioni in conflitto. L'esecuzione di tale transazione dovrà essere tentata di nuovo. (Per altre informazioni, vedere [linee guida per la logica di tentativi per le transazioni nelle tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).)  
  
 Viene applicato automaticamente il presupposto ottimistico che non siano presenti conflitti né violazioni di isolamento delle transazioni. Se si verificano conflitti che possono causare incoerenze nel database o violare l'isolamento delle transazioni, tali conflitti vengono rilevati e la transazione viene terminata.  
  
 Se viene rilevato un conflitto, la transazione viene terminata e il client dovrà ripetere il tentativo.  
  
 Nella tabella seguente vengono riepilogate le condizioni di errore per le transazioni che accedono a tabelle ottimizzate per la memoria.  
  
### <a name="error-conditions-for-transactions-accessing-memory-optimized-tables"></a>Condizioni di errore per le transazioni che accedono a tabelle ottimizzate per la memoria.  
  
|Errore|Scenario|  
|-----------|--------------|  
|Conflitto di scrittura. Tentativo di aggiornare un record che è stato aggiornato dopo l'avvio della transazione.|Istruzione UPDATE o DELETE per una riga che è stata aggiornata o eliminata da una transazione simultanea.|  
|Errore di convalida di lettura ripetibile.|Una riga letta dalla transazione è stata modificata (aggiornata o eliminata) dopo l'avvio della transazione. La convalida di lettura ripetibile si verifica in genere quando si utilizzano i livelli di isolamento delle transazioni REPEATABLE READ e SERIALIZABLE.|  
|Errore di convalida serializzabile.|Dall'avvio della transazione è stata inserita una nuova riga (fantasma) in uno degli intervalli di analisi nella transazione. La riga sarebbe stata rilevata dalla transazione se ne fosse stato eseguito il commit nel database prima dell'avvio della transazione. La convalida SERIALIZABLE si verifica in genere quando si utilizza l'isolamento SERIALIZABLE e la convalida dei vincoli PRIMARY KEY.|  
|Errore di dipendenza di commit.|La transazione ha acquisito una dipendenza da un'altra transazione di cui non è stato eseguito il commit a causa di uno degli errori indicati in questa tabella, di una condizione di memoria insufficiente o dell'impossibilità di eseguire il commit nel log delle transazioni. Questo errore può verificarsi con transazioni di lettura/scrittura e di sola lettura.|  
  
### <a name="transaction-lifetime"></a>Durata della transazione  
 Gli errori indicati nella tabella precedente possono verificarsi in momenti diversi durante una transazione. Nella figura seguente vengono illustrate le fasi di una transazione che accede a tabelle ottimizzate per la memoria.  
  
 ![Durata di una transazione. ](../../2014/database-engine/media/hekaton-transactions.gif "Durata di una transazione.")  
Durata di una transazione che accede a tabelle ottimizzate per la memoria.  
  
#### <a name="regular-processing"></a>Elaborazione regolare  
 Durante questa fase vengono eseguite le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] immesse dall'utente. Le righe vengono lette dalle tabelle e le nuove versioni di riga vengono scritte nel database. La transazione è isolata da tutte le altre transazioni simultanee. La transazione utilizza lo snapshot delle tabelle ottimizzate per la memoria presente all'avvio della transazione.  
  
 Le scritture nelle tabelle in questa fase della transazione non sono ancora visibili ad altre transazioni, con un'eccezione: gli aggiornamenti e le eliminazioni di righe sono visibili alle operazioni di aggiornamento ed eliminazione in altre transazioni, allo scopo di rilevare i conflitti di scrittura.  
  
 Se in un'operazione di aggiornamento o eliminazione viene rilevato che una riga è stata aggiornata o eliminata dopo l'avvio logico della transazione, l'operazione avrà esito negativo con l'errore 41302. Il messaggio relativo all'errore 41302 è analogo al seguente: "Tentativo da parte della transazione corrente di aggiornare un record nella tabella X che è già stato aggiornato dopo l'avvio della transazione. La transazione è stata interrotta".  
  
 Questo errore elimina la transazione, anche se XACT_ABORT è impostata su OFF, pertanto verrà eseguito il rollback della transazione al termine della sessione utente. Non è possibile eseguire il commit delle transazioni eliminate e tali transazioni supportano solo le operazioni di lettura che non scrivono nel log e non accedono alle tabelle ottimizzate per la memoria.  
  
#####  <a name="cd"></a> Dipendenze di commit  
 Durante l'elaborazione regolare, una transazione è in grado di leggere le righe scritte da altre transazioni che si trovano nella fase di convalida o di commit, ma per le quali il commit non è ancora stato eseguito. Le righe sono visibili perché l'ora di fine logica delle transazioni è stata assegnata all'avvio della fase di convalida.  
  
 Se una transazione legge tali righe di cui non è stato eseguito il commit, acquisirà una dipendenza di commit da tale transazione, con due implicazioni principali:  
  
-   Una transazione non può eseguire il commit finché non viene eseguito il commit delle transazioni da cui dipende. In altre parole, non può avviare la fase di commit finché non saranno stato cancellate tutte le dipendenze.  
  
-   Inoltre, i set di risultati non vengono restituiti al client finché tutte le dipendenze non saranno cancellate. In questo modo si impedisce al client di considerare dati di cui non è stato eseguito il commit.  
  
 Se per una delle transazioni dipendenti non viene eseguito il commit, si verifica un errore di dipendenza di commit. Ciò significa che non verrà eseguito il commit della transazione con l'errore 41301 ("Una transazione precedente da cui dipende la transazione corrente è stata interrotta. Impossibile eseguire il commit della transazione corrente").  
  
#### <a name="validation-phase"></a>Fase di convalida  
 Durante la fase di convalida viene verificato automaticamente che i presupposti necessari per il livello di isolamento della transazione richiesto siano soddisfatti per tutta la durata logica della transazione.  
  
 All'inizio della fase di convalida, alla transazione viene assegnata un'ora di fine logica. Le versioni di riga scritte nel database diventano visibili ad altre transazioni all'ora di fine logica. Per altre informazioni, vedere [dipendenze di Commit](#cd).  
  
##### <a name="repeatable-read-validation"></a>Convalida di lettura ripetibile  
 Se il livello di isolamento della transazione è REPEATABLE READ o SERIALIZABLE oppure se le tabelle sono accessibili nel livello di isolamento REPEATABLE READ o SERIALIZABLE (per altre informazioni, vedere la sezione sull'isolamento di singole operazioni in [delle transazioni I livelli di isolamento](../../2014/database-engine/transaction-isolation-levels.md)), il sistema verifica che le letture siano ripetibili. Ciò significa che viene confermato che le versioni delle righe lette dalla transazione sono ancora valide al momento dell'ora di fine logica della transazione.  
  
 Se una qualsiasi delle righe è stata aggiornata o modificata, il commit della transazione non viene eseguito con l'errore 41305 (analogo a "Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida di lettura ripetibile").  
  
 Questo errore può verificarsi anche se una tabella viene eliminata dopo un'operazione di inserimento, aggiornamento o eliminazione e prima del commit della transazione. Si applica solo alle operazioni di inserimento, aggiornamento o eliminazione nelle stored procedure compilate in modo nativo. Tali operazioni di scrittura eseguite tramite [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato causano il blocco dell'istruzione DROP TABLE e l'attesa del completamento del commit della transazione.  
  
##### <a name="serializable-validation"></a>Convalida serializzabile  
 La convalida serializzabile viene eseguita in due casi:  
  
-   Se il livello di isolamento della transazione è SERIALIZABLE o le tabelle sono accessibili nel livello di isolamento SERIALIZABLE.  
  
-   Se le righe vengono inserite in un indice univoco, ad esempio l'indice creato per un vincolo PRIMARY KEY. Viene verificato automaticamente che non siano state inserite simultaneamente righe con la stessa chiave.  
  
 Viene verificato automaticamente che nel database non siano state scritte righe fantasma. Le operazioni di lettura eseguite dalla transazione vengono valutate per determinare che negli intervalli di analisi di tali operazioni di lettura non siano state inserite nuove righe.  
  
 L'inserimento di una chiave in un indice univoco include un'operazione di lettura implicita, per determinare che la chiave non sia un duplicato. La convalida serializzabile per gli indici univoci assicura che tali indici non possano includere duplicati nel caso in cui due transazioni simultanee inseriscano la stessa chiave.  
  
 Se vengono rilevate righe fantasma, il commit della transazione non viene eseguito con l'errore 41325 (analogo a "Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida serializzabile").  
  
#### <a name="commit-processing"></a>Elaborazione del commit  
 Se la convalida ha esito positivo e tutte le dipendenze della transazione sono state cancellate, la transazione passa nella fase di elaborazione del commit. Durante questa fase le modifiche apportate alle tabelle durevoli vengono scritte nel log e questo viene scritto su disco per garantire la durabilità. Una volta effettuata la scrittura su disco del record del log per la transazione, il controllo viene restituito al client.  
  
 Tutte le dipendenze di commit della transazione vengono cancellate e tutte le transazioni in attesa del commit di tale transazione potranno continuare.  
  
## <a name="limitations"></a>Limitazioni  
  
-   Le transazioni tra database non sono supportate con le tabelle ottimizzate per la memoria. Ogni transazione che accede a tabelle ottimizzate per la memoria non può accedere a più di un database, ad eccezione dell'accesso in lettura/scrittura a tempdb e dell'accesso in sola lettura al master del database di sistema.  
  
-   Le transazioni distribuite non sono supportate con le tabelle ottimizzate per la memoria. Le transazioni distribuite avviate con BEGIN DISTRIBUTED TRANSACTION non possono accedere alle tabelle ottimizzate per la memoria.  
  
-   Le tabelle con ottimizzazione per la memoria non supportano alcun blocco. I blocchi espliciti tramite hint di blocco (ad esempio TABLOCK, XLOCK, ROWLOCK) non sono supportati con le tabelle ottimizzate per la memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle transazioni in tabelle con ottimizzazione per la memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
  
