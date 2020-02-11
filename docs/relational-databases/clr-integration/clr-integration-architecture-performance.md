---
title: Prestazioni dell'integrazione con CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
author: rothja
ms.author: jroth
ms.openlocfilehash: d478c9da4455b4c343a323ffa33eb742f50be7bb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70212424"
---
# <a name="clr-integration-architecture----performance"></a>Architettura di integrazione CLR - Prestazioni
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  In questo argomento vengono illustrate alcune delle scelte di progettazione che migliorano le prestazioni dell' [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrazione con il [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR).  
  
## <a name="the-compilation-process"></a>Processo di compilazione  
 Durante la compilazione di espressioni SQL, quando viene rilevato un riferimento a una routine gestita, viene generato uno stub di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language (MSIL). Questo stub include il codice che consente di effettuare il marshalling dei parametri di routine da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a CLR, richiamare la funzione e restituire il risultato. Questo codice di "unione" si basa sul tipo di parametro e sulla direzione del parametro (interna, esterna o di riferimento).  
  
 Il codice di "unione" consente di eseguire ottimizzazioni specifiche del tipo e assicura un'applicazione efficiente della semantica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio il supporto di valori Null, i facet vincolanti e la gestione delle eccezioni standard e in base al valore. La generazione di codice apposito per i tipi degli argomenti consente di evitare i costi legati all'assegnazione forzata o alla creazione di oggetti wrapper, chiamata "boxing", all'interno dei limiti della chiamata.  
  
 Lo stub generato viene quindi compilato nel codice nativo e ottimizzato per l'architettura hardware specifica su cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzando i servizi di compilazione JIT (Just-In-Time) di CLR. I servizi JIT sono richiamati a livello di metodo e consentono all'ambiente host di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di creare una sola unità di compilazione che comprende sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che l'esecuzione di CLR. Dopo aver compilato lo stub, il puntatore a funzione risultante diventa l'implementazione in fase di esecuzione della funzione. Questo approccio che prevede la generazione di codice consente di evitare i costi di chiamata aggiuntivi relativi alla riflessione o all'accesso ai metadati in fase di esecuzione.  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>Transizioni veloci tra SQL Server e CLR  
 Il processo di compilazione restituisce un puntatore a funzione che può essere chiamato in fase di esecuzione dal codice nativo. Nel caso di funzioni definite dall'utente a valori scalari, questa chiamata alla funzione avviene su ogni riga. Per ridurre al minimo il costo della transizione tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e CLR, le istruzioni che contengono chiamate gestite prevedono un passaggio di avvio per identificare il dominio dell'applicazione di destinazione. Questo passaggio di identificazione riduce il costo della transizione per ogni riga.  
  
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni  
 Nelle sezioni che seguono vengono riepilogate le considerazioni relative alle prestazioni specifiche dell'integrazione con CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni più dettagliate, vedere l'argomento relativo all'[uso dell'integrazione con CLR in SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=50332)sul sito Web MSDN. Informazioni generali sulle prestazioni del codice gestito sono disponibili in "[miglioramento delle prestazioni e della scalabilità delle applicazioni .NET](https://go.microsoft.com/fwlink/?LinkId=50333)" sul sito Web MSDN.  
  
### <a name="user-defined-functions"></a>Funzioni definite dall'utente  
 Il percorso di chiamata per le funzioni CLR risulta più veloce di quello delle funzioni definite dall'utente [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il codice gestito dispone inoltre di un vantaggio in termini di prestazioni decisamente superiore rispetto a [!INCLUDE[tsql](../../includes/tsql-md.md)] per quanto riguarda il codice procedurale, il calcolo e la manipolazione delle stringhe. Le funzioni CLR che prevedono intense attività di calcolo e che non eseguono l'accesso ai dati vengono scritte meglio in codice gestito. Le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] tuttavia, eseguono l'accesso ai dati più efficientemente rispetto all'integrazione CLR.  
  
### <a name="user-defined-aggregates"></a>Funzioni di aggregazione definite dall'utente  
 Il codice gestito può determinare prestazioni notevolmente superiori rispetto all'aggregazione basata sul cursore. Il codice gestito generalmente risulta leggermente più lento rispetto alle funzioni di aggregazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incorporate. Se esiste una funzione di aggregazione predefinita nativa, è consigliabile utilizzarla. Nei casi in cui l'aggregazione necessaria non è supportata a livello nativo, è opportuno utilizzare un'aggregazione definita dall'utente CLR su un'implementazione basata sul cursore per migliorare le prestazioni.  
  
### <a name="streaming-table-valued-functions"></a>STVF (Streaming Table-Valued Function, Funzioni di flusso con valori di tabella)  
 Le applicazioni spesso devono restituire una tabella come risultato della chiamata di una funzione. Gli esempi includono la lettura di dati tabulari da un file nell'ambito di un'operazione di importazione e la conversione di valori delimitati da virgole in una rappresentazione relazionale. Per effettuare queste operazioni in genere è necessario materializzare e popolare la tabella dei risultati prima che possa essere utilizzata dal chiamante. L'integrazione di CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] introduce un nuovo meccanismo di extensibility definito tabella di streaming con valori di tabella (STVF, streaming table-valued function). Le funzioni di flusso con valori di tabella offrono prestazioni migliori rispetto alle implementazioni delle stored procedure estese confrontabili.  
  
 Funzioni accedono sono funzioni gestite che restituiscono un'interfaccia **IEnumerable** . **IEnumerable** dispone di metodi per esplorare il set di risultati restituito da STVF. Quando viene richiamato STVF, l'oggetto **IEnumerable** restituito è direttamente connesso al piano di query. Il piano di query chiama i metodi **IEnumerable** quando è necessario recuperare le righe. Questo modello di iterazione consente di utilizzare immediatamente i risultati subito dopo la produzione della prima riga, anziché dover attendere che venga popolata l'intera tabella. Riduce inoltre significativamente la quantità di memoria utilizzata quando si richiama la funzione.  
  
### <a name="arrays-vs-cursors"></a>Confronto tra matrici e cursori  
 Quando i cursori [!INCLUDE[tsql](../../includes/tsql-md.md)] devono attraversare i dati che sono espressi più facilmente come una matrice, è possibile utilizzare il codice gestito per ottenere prestazioni di gran lunga superiori.  
  
### <a name="string-data"></a>Dati di tipo stringa  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i dati di tipo carattere, ad esempio **varchar**, possono essere di tipo SqlString o SqlChars nelle funzioni gestite. Le variabili SqlString creano un'istanza dell'intero valore in memoria. Le variabili SqlChars forniscono un'interfaccia di flusso che può essere utilizzata per ottenere prestazioni migliori e una maggiore scalabilità creando un'istanza dell'intero valore in memoria. Questo diventa particolarmente importante per i dati di tipo LOB. Inoltre, è possibile accedere ai dati XML del server tramite un'interfaccia di flusso restituita da **SQLXML. CreateReader ()**.  
  
### <a name="clr-vs-extended-stored-procedures"></a>Confronto tra CLR e stored procedure estese  
 Le API Microsoft.SqlServer.Server che consentono alle procedure gestite di inviare di nuovo i set di risultati al client offrono prestazioni migliori rispetto alle API ODS (Open Data Services) utilizzate dalle stored procedure estese. Inoltre, le API System. Data. SqlServer supportano tipi di dati quali **XML**, **varchar (max)**, **nvarchar (max)** e **varbinary (max)**, introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], mentre le API ODS non sono state estese per supportare i nuovi tipi di dati.  
  
 Con il codice gestito, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce l'utilizzo di risorse come la memoria, i thread e la sincronizzazione. Questo accade in quanto le API gestite che espongono queste risorse vengono implementate nello strumento di gestione delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Viceversa, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di una vista o di un controllo sull'utilizzo delle risorse della stored procedure estesa. Se, ad esempio, un stored procedure esteso utilizza una quantità eccessiva di risorse di CPU o di memoria, non è possibile rilevare o controllare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]questa operazione con. Il codice gestito consente tuttavia a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di rilevare che un determinato thread non è stato prodotto per un lungo periodo di tempo e quindi imporre l'esecuzione dell'attività in modo da poter pianificare altro lavoro. Di conseguenza, l'utilizzo di codice gestito offre una maggiore scalabilità e un miglior utilizzo delle risorse di sistema.  
  
 Il codice gestito può determinare un overhead aggiuntivo, necessario per gestire l'ambiente di esecuzione ed eseguire controlli di sicurezza. Ciò avviene, ad esempio, qualora siano necessarie l'esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e numerose transizioni da codice gestito a codice nativo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede infatti l'esecuzione di una manutenzione aggiuntiva sulle impostazioni specifiche del thread se si passa dal codice nativo a un altro tipo di codice, quindi si utilizza di nuovo il codice nativo. Di conseguenza, le stored procedure estese possono offrire prestazioni nettamente superiori rispetto al codice gestito in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle situazioni in cui le transizioni tra codice gestito e codice nativo sono frequenti.  
  
> [!NOTE]  
>  È consigliabile non sviluppare nuove stored procedure estese, in quanto questa caratteristica è deprecata.  
  
### <a name="native-serialization-for-user-defined-types"></a>Serializzazione nativa per i tipi definiti dall'utente  
 I tipi definiti dall'utente sono progettati come un meccanismo di extensibility per il sistema di tipo scalare. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementa un formato di serializzazione per i tipi definiti dall'utente denominato **format. native**. Durante la compilazione, la struttura del tipo viene esaminata per generare un codice MSIL personalizzato per la definizione del tipo specifico.  
  
 La serializzazione nativa è l'implementazione predefinita per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La serializzazione definita dall'utente richiama un metodo definito dall'autore del tipo per eseguire la serializzazione. Quando possibile, è consigliabile usare la serializzazione **format. native** per ottenere prestazioni ottimali.  
  
### <a name="normalization-of-comparable-udts"></a>Normalizzazione dei tipi definiti dall'utente confrontabili  
 Le operazioni relazionali, ad esempio l'ordinamento e il confronto dei tipi definiti dall'utente, agiscono direttamente sulla rappresentazione binaria del valore. A tale scopo, è necessario archiviare una rappresentazione normalizzata (con ordinamento binario) dello stato del tipo definito dall'utente su disco.  
  
 La normalizzazione presenta due vantaggi: rende l'operazione di confronto molto meno costosa evitando la costruzione dell'istanza del tipo e l'overhead della chiamata al metodo e crea un dominio binario per il tipo definito dall'utente, consentendo la costruzione di istogrammi, indici e istogrammi per i valori del tipo. Di conseguenza, i tipi definiti dall'utente normalizzati offrono prestazioni molto simili ai tipi predefiniti nativi per operazioni che non comportano chiamate al metodo.  
  
### <a name="scalable-memory-usage"></a>Utilizzo della memoria scalabile  
 Per ottenere prestazioni e scalabilità soddisfacenti del processo di Garbage Collection gestito in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], evitare una singola allocazione di grandi dimensioni. Le allocazioni di dimensioni maggiori di 88 kilobyte (KB) vengono inserite nell'heap oggetti grandi che determina prestazioni e scalabilità nettamente inferiori rispetto ad allocazioni più piccole. Se ad esempio è necessario allocare una matrice multidimensionale di dimensioni elevate, è preferibile allocare una matrice di matrici (a dispersione).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
