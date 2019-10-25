---
title: Isolamento dello snapshot in SQL Server
description: Viene descritto il supporto per l'isolamento dello snapshot, un meccanismo di controllo delle versioni delle righe progettato per ridurre il blocco nelle applicazioni transazionali.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8ef462246d35694ba9bf38954ca8c58635e44e7f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452084"
---
# <a name="snapshot-isolation-in-sql-server"></a>Isolamento dello snapshot in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L'isolamento dello snapshot migliora la concorrenza per le applicazioni OLTP.  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>Informazioni sull'isolamento dello snapshot e sul controllo delle versioni delle righe  
Una volta abilitato l'isolamento dello snapshot, le versioni delle righe aggiornate per ciascuna transazione vengono conservate nel database temporaneo **tempdb**. Un numero di sequenza di transazioni univoco identifica ogni transazione e questi numeri univoci vengono registrati per ogni versione di riga. La transazione funziona con le versioni di riga più recenti con un numero di sequenza prima del numero di sequenza della transazione. Le versioni di riga più recenti create dopo l'inizio della transazione vengono ignorate dalla transazione.  
  
Il termine "snapshot" riflette il fatto che tutte le query nella transazione visualizzano la stessa versione, o snapshot, del database, in base allo stato del database nel momento in cui viene avviata la transazione. Non vengono acquisiti blocchi nelle righe di dati o nelle pagine di dati sottostanti in una transazione snapshot, che consente l'esecuzione di altre transazioni senza essere bloccate da una transazione non completata. Le transazioni che modificano i dati non bloccano le transazioni che leggono i dati e le transazioni che leggono i dati non bloccano le transazioni che scrivono i dati, come normalmente nel livello di isolamento READ COMMITTED predefinito in SQL Server. Questo comportamento, oltre a non causare blocchi, riduce anche in modo significativo la probabilità di deadlock per le transazioni complesse.  
  
L'isolamento dello snapshot usa un modello di concorrenza ottimistica. Se una transazione snapshot tenta di eseguire il commit delle modifiche apportate ai dati modificati dall'inizio della transazione, verrà eseguito il rollback della transazione e verrà generato un errore. È possibile evitare questo problema utilizzando hint UPDLOCK per le istruzioni SELECT che accedono ai dati da modificare. Per ulteriori informazioni, vedere "hint di blocco" in documentazione online di SQL Server.  
  
Per abilitare l'isolamento dello snapshot, è necessario impostare l'opzione ALLOW_SNAPSHOT_ISOLATION ON database prima di utilizzarla nelle transazioni. Questa operazione consente di attivare il meccanismo di archiviazione delle versioni delle righe nel database temporaneo (**tempdb**). È necessario abilitare l'isolamento dello snapshot in ogni database che lo utilizza con l'istruzione Transact-SQL ALTER DATABASE. In questo senso, l'isolamento dello snapshot è diverso dai livelli di isolamento tradizionali di READ COMMITTED, REPEATable READ, SERIALIZABLE e READ UNCOMMITTED, che non richiedono alcuna configurazione. Le istruzioni seguenti attivano l'isolamento dello snapshot e sostituiscono il comportamento di READ COMMITTED predefinito con lo SNAPSHOT:  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
L'impostazione dell'opzione READ_COMMITTED_SNAPSHOT ON consente l'accesso alle righe con controllo delle versioni sotto il livello di isolamento READ COMMITTED predefinito. Se l'opzione READ_COMMITTED_SNAPSHOT è impostata su OFF, è necessario impostare in modo esplicito il livello di isolamento dello snapshot per ogni sessione per accedere alle righe con versione.  
  
## <a name="managing-concurrency-with-isolation-levels"></a>Gestione della concorrenza con i livelli di isolamento  
Il livello di isolamento in cui viene eseguita un'istruzione Transact-SQL determina il comportamento di blocco e di controllo delle versioni delle righe. Un livello di isolamento ha un ambito a livello di connessione e, una volta impostato per una connessione con l'istruzione SET TRANSACTION ISOLAtion LEVEL, rimane attivo fino a quando la connessione non viene chiusa o viene impostato un altro livello di isolamento. Quando una connessione viene chiusa e restituita al pool, viene mantenuto il livello di isolamento dell'ultima istruzione SET TRANSACTION ISOLAtion LEVEL. Le connessioni successive che riutilizzano una connessione in pool utilizzano il livello di isolamento che era attivo al momento in cui la connessione è in pool.  
  
Le singole query eseguite in una connessione possono contenere hint di blocco che modificano l'isolamento per una singola istruzione o transazione, ma non influiscono sul livello di isolamento della connessione. I livelli di isolamento o gli hint di blocco impostati in stored procedure o funzioni non modificano il livello di isolamento della connessione che li chiama e sono attivi solo per la durata del stored procedure o della chiamata di funzione.  
  
I quattro livelli di isolamento definiti nello standard SQL-92 sono supportati nelle prime versioni di SQL Server:  
  
- READ UNCOMMITTED è il livello di isolamento meno restrittivo perché ignora i blocchi posizionati da altre transazioni. Le transazioni in esecuzione con READ UNCOMMITTED possono leggere i valori dei dati modificati non ancora sottoposti a commit da altre transazioni. Queste letture sono denominate "Dirty".  
  
- READ COMMITTED è il livello di isolamento predefinito per SQL Server. Impedisce le letture dirty specificando che le istruzioni non possono leggere i valori dei dati modificati ma non ancora sottoposte a commit da altre transazioni. Altre transazioni possono comunque modificare, inserire o eliminare dati tra le esecuzioni di singole istruzioni all'interno della transazione corrente, ottenendo letture non ripetibili o dati "fantasma".  
  
- REPEATable READ è un livello di isolamento più restrittivo rispetto a READ COMMITTED. Include READ COMMITTED, inoltre specifica che nessun'altra transazione può modificare o eliminare i dati letti dalla transazione corrente fino al commit della transazione corrente. La concorrenza è inferiore a per READ COMMITTED perché i blocchi condivisi sui dati letti vengono mantenuti per la durata della transazione anziché essere rilasciati alla fine di ogni istruzione.  
  
- SERIALIZABLE è il livello di isolamento più restrittivo, perché blocca interi intervalli di chiavi e mantiene attivi tali blocchi fino al completamento della transazione. Include la lettura RIPETIbile e aggiunge la restrizione che altre transazioni non possono inserire nuove righe negli intervalli letti dalla transazione fino al completamento della transazione.  
  
Per altre informazioni vedere [Guida per il controllo delle versioni delle righe e il blocco della transazione](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md).  
  
### <a name="snapshot-isolation-level-extensions"></a>Estensioni del livello di isolamento dello snapshot  
In SQL Server sono state introdotte estensioni ai livelli di isolamento SQL-92 sotto forma del livello di isolamento SNAPSHOT e un'implementazione aggiuntiva di READ COMMITTED. Il livello di isolamento READ_COMMITTED_SNAPSHOT può sostituire READ COMMITTED per tutte le transazioni.  
  
- Isolamento dello SNAPSHOT specifica che i dati letti all'interno di una transazione non rifletteranno mai le modifiche apportate da altre transazioni simultanee. La transazione utilizza le versioni delle righe di dati esistenti all'inizio della transazione. Nessun blocco viene inserito nei dati quando viene letto, quindi le transazioni SNAPSHOT non impediscono la scrittura di dati da parte di altre transazioni. Viceversa, le transazioni che eseguono scritture di dati non impediscono la lettura di dati da transazioni snapshot. È necessario abilitare l'isolamento dello snapshot impostando l'opzione di database ALLOW_SNAPSHOT_ISOLATION per usarla.  
  
- L'opzione di database READ_COMMITTED_SNAPSHOT determina il comportamento del livello di isolamento READ COMMITTED predefinito quando l'isolamento dello snapshot è abilitato in un database. Se non si specifica in modo esplicito READ_COMMITTED_SNAPSHOT su, READ COMMITTED viene applicato a tutte le transazioni implicite. Questo comportamento produce lo stesso comportamento di setting READ_COMMITTED_SNAPSHOT OFF (impostazione predefinita). Quando READ_COMMITTED_SNAPSHOT OFF è attivo, il motore di database utilizza i blocchi condivisi per applicare il livello di isolamento predefinito. Se si imposta l'opzione di database READ_COMMITTED_SNAPSHOT su ON, il motore di database utilizza il controllo delle versioni delle righe e l'isolamento dello snapshot come impostazione predefinita, anziché utilizzare i blocchi per proteggere i dati.  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>Funzionamento dell'isolamento dello snapshot e del controllo delle versioni delle righe  
Quando viene abilitato il livello di isolamento SNAPSHOT, ogni volta che una riga viene aggiornata, il motore di database di SQL Server archivia una copia della riga originale in **tempdb** e aggiunge un numero di sequenza della transazione alla riga. Di seguito è riportata la sequenza di eventi che si verifica:  
  
1. Viene avviata una nuova transazione a cui viene assegnato un numero di sequenza della transazione.  
  
2. Il motore di database legge una riga all'interno della transazione e recupera da **tempdb** la versione della riga il cui numero di sequenza è il più vicino e inferiore al numero di sequenza della transazione.  
  
3. Il motore di database verifica se il numero di sequenza della transazione non è presente nell'elenco dei numeri di sequenza delle transazioni di cui non è stato eseguito il commit attivo al momento dell'avvio della transazione snapshot.  
  
4. La transazione legge da **tempdb** la versione della riga disponibile all'inizio della transazione. Non verranno visualizzate le nuove righe inserite dopo l'avvio della transazione, perché i valori dei numeri di sequenza saranno superiori al valore del numero di sequenza della transazione.  
  
5. La transazione corrente rileverà le righe eliminate dopo l'inizio della transazione, in quanto in **tempdb** sarà disponibile una versione della riga che presenta un valore del numero di sequenza minore.  
  
L'effetto finale dell'isolamento dello snapshot è che la transazione Visualizza tutti i dati esistenti all'inizio della transazione, senza rispettare o inserire blocchi sulle tabelle sottostanti. Ciò può comportare un miglioramento delle prestazioni in situazioni in cui si verificano contese.  
  
Una transazione snapshot utilizza sempre il controllo della concorrenza ottimistica, riportando i blocchi che impediscono alle altre transazioni di aggiornare le righe. Se una transazione snapshot tenta di eseguire il commit di un aggiornamento in una riga che è stata modificata dopo l'inizio della transazione, viene eseguito il rollback della transazione e viene generato un errore.  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>Utilizzo dell'isolamento dello snapshot in ADO.NET  
L'isolamento dello snapshot è supportato in ADO.NET dalla classe <xref:Microsoft.Data.SqlClient.SqlTransaction>. Se un database è abilitato per l'isolamento dello snapshot ma non è configurato per READ_COMMITTED_SNAPSHOT ON, è necessario avviare una <xref:Microsoft.Data.SqlClient.SqlTransaction> usando il valore di enumerazione **IsolationLevel.Snapshot** quando viene chiamato il metodo <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A>. Questo frammento di codice presuppone che la connessione sia un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> aperto.  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>Esempio  
Nell'esempio seguente viene illustrato come i diversi livelli di isolamento si comportano tentando di accedere ai dati bloccati e non devono essere utilizzati nel codice di produzione.  
  
Il codice esegue la connessione al database di esempio **AdventureWorks** in SQL Server, crea una tabella denominata **TestSnapshot** e inserisce una riga di dati. Il codice utilizza l'istruzione Transact-SQL ALTER DATABASE per attivare l'isolamento dello snapshot per il database, ma non imposta l'opzione READ_COMMITTED_SNAPSHOT, lasciando attivo il comportamento predefinito a livello di isolamento READ COMMITTED. Il codice esegue quindi le azioni seguenti:  
  
1. Inizia, ma non completa, sqlTransaction1, che usa il livello di isolamento SERIALIZABLE per avviare una transazione di aggiornamento. Questo ha l'effetto di bloccare la tabella.  
  
2. Apre una seconda connessione e avvia una seconda transazione usando il livello di isolamento SNAPSHOT per leggere i dati nella tabella **TestSnapshot**. Poiché l'isolamento dello snapshot è abilitato, questa transazione può leggere i dati esistenti prima dell'avvio di sqlTransaction1.  
  
3. Viene aperta una terza connessione e viene avviata una transazione utilizzando il livello di isolamento READ COMMITTED per tentare di leggere i dati nella tabella. In tal caso, il codice non può leggere i dati perché non è in grado di leggere oltre i blocchi sulla tabella nella prima transazione e pertanto si verifica il timeout. Lo stesso risultato si ottiene con i livelli di isolamento REPEATABLE READ e SERIALIZABLE poiché questi non possono leggere oltre i blocchi posizionati nella prima transazione.  
  
4. Apre una quarta connessione e avvia una transazione usando il livello di isolamento READ UNCOMMITTED, che esegue una lettura dirty del valore di cui non è stato eseguito il commit in sqlTransaction1. Questo valore potrebbe non esistere mai nel database se non viene eseguito il commit della prima transazione.  
  
5. Esegue il rollback della prima transazione, elimina la tabella **TestSnapshot** e disattiva l'isolamento dello snapshot per il database **AdventureWorks**.  
  
> [!NOTE]
>  Negli esempi seguenti viene usata la stessa stringa di connessione con il pool di connessioni disattivato. Se una connessione è in pool, la reimpostazione del livello di isolamento non comporta la reimpostazione del livello di isolamento nel server. Di conseguenza, le connessioni successive che usano la stessa connessione interna in pool iniziano con i livelli di isolamento impostati su quello della connessione in pool. Un'alternativa alla disattivazione del pool di connessioni consiste nell'impostare il livello di isolamento in modo esplicito per ogni connessione.  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>Esempio  
Nell'esempio seguente viene illustrato il comportamento dell'isolamento dello snapshot quando i dati vengono modificati. Il codice esegue le azioni seguenti:  
  
1. Si connette al database di esempio **AdventureWorks** e abilita l'isolamento SNAPSHOT.  
  
2. Crea una tabella denominata **TestSnapshotUpdate** e inserisce tre righe di dati di esempio.  
  
3. Inizia, ma non viene completato, sqlTransaction1 usando l'isolamento dello SNAPSHOT. Nella transazione vengono selezionate tre righe di dati.  
  
4. Crea una seconda **SqlConnection** ad **AdventureWorks** e crea una seconda transazione usando il livello di isolamento READ COMMITTED che aggiorna un valore in una delle righe selezionate in sqlTransaction1.  
  
5. Commit sqlTransaction2.  
  
6. Torna a sqlTransaction1 e tenta di aggiornare la stessa riga di cui sqlTransaction1 è già stato eseguito il commit. Viene generato l'errore 3960 e viene eseguito il rollback automatico di sqlTransaction1. **SqlException.Number** e **SqlException.Message** sono visualizzati nella finestra della console.  
  
7. Esegue il codice di pulizia per disattivare l'isolamento dello snapshot in **AdventureWorks** ed elimina la tabella **TestSnapshotUpdate**.  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>Utilizzo degli hint di blocco con isolamento dello snapshot  
Nell'esempio precedente, la prima transazione seleziona i dati e una seconda transazione aggiorna i dati prima che la prima transazione possa essere completata, causando un conflitto di aggiornamento quando la prima transazione tenta di aggiornare la stessa riga. È possibile ridurre la probabilità di conflitti di aggiornamento nelle transazioni snapshot con esecuzione prolungata fornendo hint di blocco all'inizio della transazione. Nell'istruzione SELECT seguente viene utilizzato l'hint UPDLOCK per bloccare le righe selezionate:  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
L'utilizzo dell'hint di blocco UPDLOCK blocca le righe che tentano di aggiornare le righe prima del completamento della prima transazione. Ciò garantisce che le righe selezionate non abbiano conflitti quando vengono aggiornate in un secondo momento nella transazione. Vedere "hint di blocco" in documentazione online di SQL Server.  
  
Se l'applicazione presenta molti conflitti, l'isolamento dello snapshot potrebbe non essere la scelta migliore. Gli hint devono essere usati solo quando effettivamente necessario. L'applicazione non deve essere progettata in modo che si basi costantemente sugli hint di blocco per il relativo funzionamento.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
- [Guida per il controllo delle versioni delle righe e il blocco della transazione](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
