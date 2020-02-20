---
title: Isolamento dello snapshot in SQL Server
description: Descrizione del supporto per l'isolamento dello snapshot, un meccanismo di controllo delle versioni delle righe progettato per ridurre il blocco nelle applicazioni transazionali.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2d2e27fafabc259be6bfbc0137b66e34d310f449
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251154"
---
# <a name="snapshot-isolation-in-sql-server"></a>Isolamento dello snapshot in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L'isolamento dello snapshot migliora la concorrenza per le applicazioni OLTP.  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>Informazioni sull'isolamento dello snapshot e sul controllo delle versioni delle righe  
Una volta abilitato l'isolamento dello snapshot, le versioni delle righe aggiornate per ciascuna transazione vengono conservate nel database temporaneo **tempdb**. Un numero di sequenza di transazioni univoco identifica ogni transazione. Questi numeri univoci vengono registrati per ogni versione di riga. La transazione usa le versioni di riga più recenti con un numero di sequenza precedente al numero di sequenza della transazione. Le versioni di riga più recenti create dopo l'inizio della transazione vengono ignorate dalla transazione.  
  
Il termine "snapshot" riflette il fatto che tutte le query nella transazione visualizzano la stessa versione, o snapshot, del database, in base allo stato del database nel momento in cui viene avviata la transazione. Non vengono acquisiti blocchi nelle righe di dati o nelle pagine di dati sottostanti in una transazione snapshot, il che consente l'esecuzione di altre transazioni senza che vengano bloccate da una transazione non completata. Le transazioni che modificano i dati non bloccano le transazioni che leggono i dati e viceversa, come normalmente accade nel livello di isolamento READ COMMITTED predefinito in SQL Server. Questo comportamento, oltre a non causare blocchi, riduce anche in modo significativo la probabilità di deadlock per le transazioni complesse.  
  
L'isolamento dello snapshot usa un modello di concorrenza ottimistica. Se una transazione snapshot tenta di eseguire il commit delle modifiche apportate ai dati modificati dall'inizio della transazione, verrà eseguito il rollback della transazione e verrà generato un errore. È possibile evitare questo problema usando hint UPDLOCK per le istruzioni SELECT che accedono ai dati da modificare. Per altre informazioni, vedere "Hint di blocco" nella documentazione online di SQL Server.  
  
Per abilitare l'isolamento dello snapshot, è necessario impostare l'opzione del database ALLOW_SNAPSHOT_ISOLATION su ON prima che il database venga usato nelle transazioni. Questa operazione consente di attivare il meccanismo di archiviazione delle versioni delle righe nel database temporaneo (**tempdb**). È necessario abilitare l'isolamento dello snapshot in ogni database che lo usa con l'istruzione Transact-SQL ALTER DATABASE. In questo senso l'isolamento dello snapshot è diverso dai livelli di isolamento tradizionali di READ COMMITTED, REPEATABLE READ, SERIALIZABLE e READ UNCOMMITTED, che non richiedono alcuna configurazione. Le istruzioni seguenti attivano l'isolamento dello snapshot e sostituiscono il comportamento di READ COMMITTED predefinito con SNAPSHOT:  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
L'impostazione dell'opzione READ_COMMITTED_SNAPSHOT su ON consente l'accesso alle righe con controllo delle versioni nel livello di isolamento READ COMMITTED predefinito. Se l'opzione READ_COMMITTED_SNAPSHOT è impostata su OFF, è necessario impostare in modo esplicito il livello di isolamento dello snapshot per ogni sessione per accedere alle righe con versione.  
  
## <a name="managing-concurrency-with-isolation-levels"></a>Gestione della concorrenza con i livelli di isolamento  
Il livello di isolamento in cui viene eseguita un'istruzione Transact-SQL determina il comportamento di blocco e di controllo delle versioni delle righe. Il livello di isolamento ha un ambito a livello di connessione e, una volta impostato per una connessione con l'istruzione SET TRANSACTION ISOLATION LEVEL, rimane attivo fino a quando la connessione non viene chiusa o viene impostato un altro livello di isolamento. Quando una connessione viene chiusa e restituita al pool, viene mantenuto il livello di isolamento dell'ultima istruzione SET TRANSACTION ISOLATION LEVEL. Le connessioni successive che riutilizzano una connessione in pool usano il livello di isolamento che era attivo nel momento in cui la connessione è diventata in pool.  
  
Le singole query eseguite in una connessione possono contenere hint di blocco che modificano l'isolamento per una singola istruzione o transazione, ma non influiscono sul livello di isolamento della connessione. I livelli di isolamento o gli hint di blocco impostati in stored procedure o funzioni non modificano il livello di isolamento della connessione che li chiama e sono attivi solo per la durata della chiamata della stored procedure o della funzione.  
  
Nelle versioni precedenti di SQL Server sono supportati quattro livelli di isolamento definiti nello standard SQL-92:  
  
- READ UNCOMMITTED è il livello di isolamento meno restrittivo perché ignora i blocchi inseriti da altre transazioni. Le transazioni in esecuzione in READ UNCOMMITTED possono leggere i valori dei dati modificati non ancora sottoposti a commit da altre transazioni. Queste letture sono denominate "dirty".  
  
- READ COMMITTED è il livello di isolamento predefinito per SQL Server. Evita le letture dirty specificando che le istruzioni non possono leggere i valori dei dati modificati da altre transazioni, ma di cui non è ancora stato eseguito il commit. Altre transazioni possono comunque modificare, inserire o eliminare i dati nell'intervallo tra l'esecuzione delle singole istruzioni nella transazione corrente, con conseguenze come letture irripetibili e la presenza di dati fantasma.  
  
- REPEATABLE READ è un livello di isolamento più restrittivo rispetto a READ COMMITTED. Include READ COMMITTED e specifica anche che nessun'altra transazione può modificare o eliminare i dati letti dalla transazione corrente fino al commit della transazione corrente. Il livello di concorrenza è inferiore rispetto a READ COMMITTED poiché i blocchi condivisi nei dati di lettura vengono mantenuti attivi fino alla fine della transazione, anziché essere rilasciati alla fine di ogni istruzione.  
  
- SERIALIZABLE è il livello di isolamento più restrittivo, perché blocca interi intervalli di chiavi e mantiene attivi tali blocchi fino al completamento della transazione. Include REPEATABLE READ e aggiunge la restrizione per cui le altre transazioni non possono inserire nuove righe negli intervalli letti dalla transazione finché la transazione non è stata completata.  
  
Per altre informazioni vedere [Guida per il controllo delle versioni delle righe e il blocco della transazione](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md).  
  
### <a name="snapshot-isolation-level-extensions"></a>Estensioni del livello di isolamento dello snapshot  
In SQL Server sono state introdotte estensioni ai livelli di isolamento SQL-92 sotto forma del livello di isolamento SNAPSHOT e un'implementazione aggiuntiva di READ COMMITTED. Il livello di isolamento READ_COMMITTED_SNAPSHOT può sostituire READ COMMITTED per tutte le transazioni.  
  
- L'isolamento SNAPSHOT specifica che i dati letti all'interno di una transazione non rifletteranno mai le modifiche apportate da altre transazioni simultanee. La transazione usa le versioni delle righe di dati esistenti all'inizio della transazione. Nessun blocco viene inserito nei dati quando vengono letti, quindi le transazioni SNAPSHOT non impediscono la scrittura di dati da parte di altre transazioni. Viceversa, le transazioni che eseguono scritture di dati non impediscono la lettura di dati da transazioni snapshot. È necessario attivare l'isolamento dello snapshot impostando l'opzione del database ALLOW_SNAPSHOT_ISOLATION su ON.  
  
- L'opzione del database READ_COMMITTED_SNAPSHOT determina il comportamento del livello di isolamento READ COMMITTED predefinito quando l'isolamento dello snapshot viene abilitato in un database. Se non si specifica in modo esplicito READ_COMMITTED_SNAPSHOT ON, READ COMMITTED viene applicato a tutte le transazioni implicite. Questa operazione produce lo stesso comportamento dell'impostazione READ_COMMITTED_SNAPSHOT OFF, che è l'impostazione predefinita. Quando l'opzione è READ_COMMITTED_SNAPSHOT OFF, il motore di database usa i blocchi condivisi per applicare il livello di isolamento predefinito. Se si imposta l'opzione del database READ_COMMITTED_SNAPSHOT su ON, il motore di database usa il controllo delle versioni delle righe e l'isolamento dello snapshot come impostazione predefinita, anziché usare i blocchi per proteggere i dati.  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>Uso di isolamento dello snapshot e controllo delle versioni delle righe  
Quando viene abilitato il livello di isolamento SNAPSHOT, ogni volta che una riga viene aggiornata, il motore di database di SQL Server archivia una copia della riga originale in **tempdb** e aggiunge un numero di sequenza della transazione alla riga. Di seguito è riportata la sequenza di eventi che si verifica:  
  
1. Viene avviata una nuova transazione a cui viene assegnato un numero di sequenza delle transazioni.  
  
2. Il motore di database legge una riga all'interno della transazione e recupera da **tempdb** la versione della riga il cui numero di sequenza è il più vicino e inferiore al numero di sequenza della transazione.  
  
3. Il motore di database verifica se il numero di sequenza delle transazioni non è presente nell'elenco dei numeri di sequenza delle transazioni di cui non è stato eseguito il commit attive al momento dell'avvio della transazione snapshot.  
  
4. La transazione legge da **tempdb** la versione della riga disponibile all'inizio della transazione. Non visualizza le nuove righe inserite dopo l'avvio della transazione, perché queste avranno valori dei numeri di sequenza superiori al valore del numero di sequenza della transazione.  
  
5. La transazione corrente rileverà le righe eliminate dopo l'inizio della transazione, in quanto in **tempdb** sarà disponibile una versione della riga che presenta un valore del numero di sequenza minore.  
  
L'effetto finale dell'isolamento dello snapshot è che la transazione visualizza tutti i dati esistenti all'inizio della transazione, senza rispettare o inserire blocchi nelle tabelle sottostanti. Ciò può comportare un miglioramento delle prestazioni in situazioni in cui si verificano contese.  
  
Una transazione snapshot usa sempre il controllo della concorrenza ottimistica, evitando i blocchi che impediscono alle altre transazioni di aggiornare le righe. Se una transazione snapshot tenta di eseguire il commit di un aggiornamento in una riga che è stata modificata dopo l'inizio della transazione, viene eseguito il rollback della transazione e viene generato un errore.  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>Uso dell'isolamento dello snapshot in ADO.NET  
L'isolamento dello snapshot è supportato in ADO.NET dalla classe <xref:Microsoft.Data.SqlClient.SqlTransaction>. Se un database è abilitato per l'isolamento dello snapshot ma non è configurato per READ_COMMITTED_SNAPSHOT ON, è necessario avviare una <xref:Microsoft.Data.SqlClient.SqlTransaction> usando il valore di enumerazione **IsolationLevel.Snapshot** quando viene chiamato il metodo <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A>. Questo frammento di codice presuppone che la connessione sia un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> aperto.  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>Esempio  
L'esempio seguente illustra come i diversi livelli di isolamento si comportano tentando di accedere ai dati bloccati e non è inteso come da usare nel codice di produzione.  
  
Il codice esegue la connessione al database di esempio **AdventureWorks** in SQL Server, crea una tabella denominata **TestSnapshot** e inserisce una riga di dati. Il codice usa l'istruzione Transact-SQL ALTER DATABASE per attivare l'isolamento dello snapshot per il database, ma non imposta l'opzione READ_COMMITTED_SNAPSHOT, lasciando attivo il comportamento del livello di isolamento READ COMMITTED predefinito. Il codice esegue quindi le azioni seguenti:  
  
1. Avvia, ma non completa, sqlTransaction1, che usa il livello di isolamento SERIALIZABLE per avviare una transazione di aggiornamento. Questo ha l'effetto di bloccare la tabella.  
  
2. Apre una seconda connessione e avvia una seconda transazione usando il livello di isolamento SNAPSHOT per leggere i dati nella tabella **TestSnapshot**. Poiché l'isolamento dello snapshot è abilitato, questa transazione può leggere i dati esistenti prima dell'avvio di sqlTransaction1.  
  
3. Apre una terza connessione e avvia una transazione usando il livello di isolamento READ COMMITTED per tentare di leggere i dati nella tabella. In tal caso, il codice non può leggere i dati perché non è in grado di leggere oltre i blocchi sulla tabella nella prima transazione e pertanto si verifica il timeout. Lo stesso risultato si ottiene con i livelli di isolamento REPEATABLE READ e SERIALIZABLE poiché questi non possono leggere oltre i blocchi posizionati nella prima transazione.  
  
4. Apre una quarta connessione e avvia una transazione usando il livello di isolamento READ UNCOMMITTED, che esegue una lettura dirty del valore di cui non è stato eseguito il commit in sqlTransaction1. Questo valore potrebbe non esistere mai nel database se non viene eseguito il commit della prima transazione.  
  
5. Esegue il rollback della prima transazione, elimina la tabella **TestSnapshot** e disattiva l'isolamento dello snapshot per il database **AdventureWorks**.  
  
> [!NOTE]
>  Negli esempi seguenti viene usata la stessa stringa di connessione con il pooling delle connessioni disattivato. Se una connessione è in pool, la reimpostazione del livello di isolamento non comporta la reimpostazione del livello di isolamento nel server. Di conseguenza, le connessioni successive che usano la stessa connessione interna in pool vengono avviate con i livelli di isolamento impostati su quello della connessione in pool. Un'alternativa alla disattivazione del pooling delle connessioni consiste nell'impostare il livello di isolamento in modo esplicito per ogni connessione.  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>Esempio  
Nell'esempio seguente viene illustrato il comportamento dell'isolamento dello snapshot quando i dati vengono modificati. Il codice esegue le azioni seguenti:  
  
1. Si connette al database di esempio **AdventureWorks** e abilita l'isolamento SNAPSHOT.  
  
2. Crea una tabella denominata **TestSnapshotUpdate** e inserisce tre righe di dati di esempio.  
  
3. Avvia, ma non completa, sqlTransaction1 usando l'isolamento SNAPSHOT. Nella transazione vengono selezionate tre righe di dati.  
  
4. Crea una seconda **SqlConnection** ad **AdventureWorks** e crea una seconda transazione usando il livello di isolamento READ COMMITTED che aggiorna un valore in una delle righe selezionate in sqlTransaction1.  
  
5. Esegue il commit di sqlTransaction2.  
  
6. Torna a sqlTransaction1 e tenta di aggiornare la stessa riga di cui sqlTransaction1 ha già eseguito il commit. Viene generato l'errore 3960 e viene eseguito il rollback automatico di sqlTransaction1. **SqlException.Number** e **SqlException.Message** sono visualizzati nella finestra della console.  
  
7. Esegue il codice di pulizia per disattivare l'isolamento dello snapshot in **AdventureWorks** ed elimina la tabella **TestSnapshotUpdate**.  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>Uso degli hint di blocco con isolamento dello snapshot  
Nell'esempio precedente la prima transazione seleziona i dati e una seconda transazione aggiorna i dati prima che la prima transazione venga completata, causando un conflitto di aggiornamento quando la prima transazione tenta di aggiornare la stessa riga. È possibile ridurre la probabilità di conflitti di aggiornamento nelle transazioni snapshot con esecuzione prolungata specificando hint di blocco all'inizio della transazione. Nell'istruzione SELECT seguente viene usato l'hint UPDLOCK per bloccare le righe selezionate:  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
L'uso dell'hint di blocco UPDLOCK blocca le righe che tentano di aggiornare le righe prima del completamento della prima transazione. Ciò garantisce che le righe selezionate non siano oggetto di conflitti quando vengono aggiornate nella transazione in un secondo momento. Vedere "Hint di blocco" nella documentazione online di SQL Server.  
  
Se l'applicazione presenta molti conflitti, l'isolamento dello snapshot potrebbe non essere la scelta migliore. Gli hint devono essere usati solo quando strettamente necessario. L'applicazione non deve essere progettata in modo che il suo funzionamento si basi costantemente sugli hint di blocco.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
- [Guida per il controllo delle versioni delle righe e il blocco della transazione](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
