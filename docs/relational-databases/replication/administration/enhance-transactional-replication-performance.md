---
title: Migliorare le prestazioni della replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ebedefdd7e11f7ff3edcd884674092aeaf3b4f9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939152"
---
# <a name="enhance-transactional-replication-performance"></a>Miglioramento delle prestazioni della replica transazionale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dopo aver considerato i suggerimenti sulle prestazioni generali descritti nella sezione [Miglioramento delle prestazioni generali della replica](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), tenere presente le aree aggiuntive specifiche della replica transazionale riportate di seguito.  
  
## <a name="database-design"></a>Progettazione di database  
  
-   Ridurre al minimo le dimensioni delle transazioni nella progettazione delle applicazioni.  
  
     Per impostazione predefinita, la replica transazionale propaga le modifiche in base ai limiti delle transazioni. Più piccole sono le transazioni, minori saranno le probabilità che l'agente di distribuzione debba rinviare una transazione a causa di problemi di rete. Se è necessario che l'agente rinvii una transazione, la quantità di dati inviati sarà inferiore. 

  
## <a name="distributor-configuration"></a>Configurazione del server di distribuzione  
  
-   Configurare il server di distribuzione in un server dedicato.  
  
     È possibile ridurre l'overhead di elaborazione sul server di pubblicazione configurando un server di distribuzione remoto. Per altre informazioni, vedere [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
-   Ridimensionare in modo appropriato il database di distribuzione.  
  
     Verificare la replica con un carico tipico per il sistema per determinare lo spazio necessario per archiviare i comandi. Verificare che il database sia sufficientemente grande da consentire l'archiviazione dei comandi senza richiedere un aumento automatico delle dimensioni frequente. Per altre informazioni sulla modifica delle dimensioni di un database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="publication-design"></a>Progettazione della pubblicazione  
  
-   Replicare l'esecuzione della stored procedure durante gli aggiornamenti batch delle tabelle pubblicate.  
  
     In caso di aggiornamenti batch che occasionalmente interessano un numero di righe elevato nel Sottoscrittore, è possibile aggiornare la tabella pubblicata utilizzando una stored procedure di cui quindi verrà pubblicata l'esecuzione. Anziché inviare un aggiornamento o un'eliminazione per ogni riga interessata, l'agente di distribuzione esegue la stessa procedura nel Sottoscrittore utilizzando valori dei parametri identici. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Distribuire gli articoli in più pubblicazioni.  
  
     Se non è possibile usare il [parametro **-SubscriptionStreams**](#subscriptionstreams), provare a creare più pubblicazioni. La distribuzione di articoli tra queste pubblicazioni consente alla replica di applicare le modifiche in parallelo con i Sottoscrittori.  
  
## <a name="subscription-considerations"></a>Considerazioni sulle sottoscrizioni  
  
-   Utilizzare agenti indipendenti anziché agenti condivisi se si dispone di più pubblicazioni nello stesso server di pubblicazione, in base all'impostazione predefinita di Creazione guidata nuova pubblicazione.  
  
-   Eseguire gli agenti in modo continuo invece di pianificarne l'esecuzione frequente.  
  
     L'impostazione di un'esecuzione continua degli agenti anziché la creazione di pianificazioni frequenti, ad esempio ogni minuto, consente di migliorare le prestazioni della replica in quanto non richiede l'avvio e l'arresto dell'agente. Quando si imposta l'esecuzione continua dell'agente di distribuzione, le modifiche vengono propagate con una bassa latenza agli altri server connessi nella topologia. Per altre informazioni, vedere:  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Specificare le pianificazioni della sincronizzazione](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>Parametri dell'agente di distribuzione e dell'agente di lettura log  
I parametri del profilo dell'agente vengono spesso modificati per aumentare la velocità effettiva dell'agente di lettura log e dell'agente di distribuzione con i sistemi OLTP a traffico elevato. 

Sono stati eseguiti test per determinare i valori ottimali per migliorare le prestazioni per l'agente di lettura log e l'agente di distribuzione. Dai test risulta che il carico di lavoro è un fattore determinante per stabilire quali valori sono ottimali in quale situazione e pertanto non esiste una singola modifica di un valore che può migliorare le prestazioni in ogni situazione. 

Risultati: 
- Per un *agente di lettura log* con carichi di lavoro di transazioni più ridotte (meno di 500 comandi), la velocità effettiva può trarre vantaggio da un valore più alto per **ReadBatchSize**. Tuttavia, per carichi di lavoro con transazioni di grandi dimensioni, la modifica di questo valore non migliorerà le prestazioni. 
    - Quando sono presenti più agenti di lettura log e più agenti di distribuzione in esecuzione in parallelo nello stesso server, un valore più alto per **ReadBatchSize** causa condizioni di contesa nel database di distribuzione. 
- Per l'*agente di distribuzione*
    - L'aumento di **CommitBatchSize** può migliorare la velocità effettiva. Il compromesso è che, se si verifica un errore, l'agente di distribuzione deve eseguire il rollback e ricominciare per riapplicare un numero maggiore di transazioni. 
    - L'aumento del valore **SubscriptionStreams** è utile per la velocità effettiva complessiva dell'agente di distribuzione, perché più connessioni al Sottoscrittore applicano batch di modifiche in parallelo. Tuttavia, a seconda del numero di processori e di altre condizioni dei metadati (ad esempio una chiave primaria, chiavi esterne, vincoli UNIQUE e indici), un valore più alto di SubscriptionStreams potrebbe avere effetti negativi. Inoltre, in caso di esito negativo dell'esecuzione o del commit di un flusso, l'agente di distribuzione esegue il fallback e torna a usare un singolo flusso per ripetere i batch non riusciti.


Per altre informazioni su questi test, vedere il blog [Optimizing replication agent profile parameters for better performance](https://blogs.msdn.microsoft.com/sql_server_team/optimizing-replication-agent-profile-parameters-for-better-performance/) (Ottimizzazione dei parametri del profilo dell'agente di replica per migliorare le prestazioni).


### <a name="log-reader-agent"></a>Agente di lettura log

#### <a name="readbatchsize"></a>ReadBatchSize
- Aumentare il valore del parametro **-ReadBatchSize** per l'agente di lettura log.  
  
L'agente di lettura log e l'agente di distribuzione supportano le dimensioni di batch per operazioni di lettura e commit delle transazioni. Per impostazione predefinita, le dimensioni del batch sono pari a 500 transazioni. L'agente di lettura log legge il numero specifico di transazioni nel log, indipendentemente dal fatto che siano contrassegnate o meno per la replica. Se in un database di pubblicazione viene scritto un numero elevato di transazioni, ma solo un subset ridotto è contrassegnato per la replica, è necessario usare il parametro **-ReadBatchSize** per aumentare la dimensione del batch di lettura dell'agente di lettura log. Questo parametro non è applicabile ai server di pubblicazione Oracle.  

   - Per i carichi di lavoro di transazioni più piccole (meno di 500 comandi) si assiste a un aumento del numero di comandi elaborati al secondo quando il valore di **ReadBatchSize** viene aumentato fino a 5000. 
   - Per i carichi di lavoro di dimensioni maggiori (transazioni con 500-1000 comandi), l'aumento di **ReadBatchSize** consente di ottenere miglioramenti limitati delle prestazioni. L'aumento di **ReadBatchSize** consente di ottenere un maggior numero di transazioni scritte nel database di distribuzione in un unico roundtrip. In questo modo aumenta il tempo durante il quale le transazioni e i comandi sono visibili per l'agente di distribuzione e si introduce latenza per il processo di replica.  

#### <a name="pollinginterval"></a>PollingInterval
- Ridurre il valore del parametro **-PollingInterval** per l'agente di lettura log.  
  
Il parametro **-PollingInterval** specifica la frequenza con cui viene eseguita la query sulle transazioni da replicare nel log delle transazioni di un database pubblicato. Il valore predefinito è 5 secondi. Se si riduce tale valore, il polling del log viene eseguito più spesso con la possibilità di generare una latenza più bassa per il recapito delle transazioni dal database di pubblicazione nel database di distribuzione. È tuttavia consigliabile valutare la necessità di una latenza più bassa rispetto a un carico maggiore sul server determinato dall'esecuzione più frequente del polling.   
  
#### <a name="maxcmdsintran"></a>MaxCmdsInTran
- Per risolvere i colli di bottiglia accidentali, usare il parametro **–MaxCmdsInTran** per l'agente di lettura log.  
  
Il parametro **–MaxCmdsInTran** specifica il numero massimo di istruzioni raggruppate in una transazione mentre l'agente di lettura log scrive i comandi nel database di distribuzione. L'utilizzo di questo parametro consente all'agente di lettura log e all'agente di distribuzione di dividere le transazioni di grandi dimensioni, ovvero costituite da molti comandi, nel server di pubblicazione in diverse transazioni più piccole quando i comandi vengono applicati al Sottoscrittore. Può inoltre ridurre la possibilità che si verifichino contese nel server di distribuzione e diminuire la latenza tra il server di pubblicazione e il Sottoscrittore. Dal momento che la transazione originale viene applicata in unità più piccole, il Sottoscrittore può accedere alle righe di una vasta transazione logica del server di pubblicazione prima della fine della transazione originale, violando la rigida atomicità transazionale. Il valore predefinito è **0**, che consente di mantenere i limiti delle transazioni del server di pubblicazione. Questo parametro non è applicabile ai server di pubblicazione Oracle.  
  
   > [!WARNING]  
   >  **MaxCmdsInTran** non è stato progettato per essere sempre abilitato. Sono disponibili casi di risoluzione in cui qualcuno ha accidentalmente eseguito un numero elevato di operazioni DML in una singola transazione (causando ritardi nella distribuzione dei comandi fino a che l'intera transazione è in database di distribuzione, blocchi mantenuti e così via). Se periodicamente si verifica questa situazione, esaminare le applicazioni e trovare un modo per ridurre le dimensioni delle transazioni.  
  
### <a name="distribution-agent"></a>Agente di distribuzione

#### <a name="subscriptionstreams"></a>SubscriptionStreams
- Aumentare il parametro **-SubscriptionStreams** per l'agente di distribuzione.  
  
Il parametro **–SubscriptionStreams** può migliorare notevolmente la velocità effettiva della replica aggregata. e consente a più connessioni a un Sottoscrittore l'applicazione di batch di modifiche in parallelo, conservando molte delle caratteristiche transazionali disponibili quando si utilizza un singolo thread. Se si verifica un errore di esecuzione o di commit di una delle connessioni, tutte le connessioni interromperanno il batch corrente e l'agente utilizzerà un singolo flusso per ripetere i batch non riusciti. Prima del completamento di questa fase di tentativi, possono verificarsi inconsistenze temporanee delle transazioni nel Sottoscrittore. Al termine del commit dei batch non riusciti, viene ripristinata la consistenza delle transazioni nel Sottoscrittore.  
  
È possibile specificare un valore per questo parametro di agente usando **@subscriptionstreams** di [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).  

Per altre informazioni sull'implementazione di flussi di sottoscrizione, vedere [Navigating SQL replication subscriptionStream setting](https://blogs.msdn.microsoft.com/repltalk/2010/03/01/navigating-sql-replication-subscriptionstreams-setting) (Informazioni sull'impostazione subscriptionStream per la replica SQL).
  
### <a name="blocking-monitor-thread"></a>Thread di monitoraggio blocco

L'agente di distribuzione mantiene un thread di monitoraggio blocco che rileva gli eventi di blocco tra le sessioni. Se il thread di monitoraggio blocco rileva blocchi tra le sessioni, l'agente di distribuzione attiva l'uso di una sola sessione per riapplicare il batch corrente di comandi che non è stato possibile applicare in precedenza.

Il thread di monitoraggio blocco può rilevare il blocco tra sessioni dell'agente di distribuzione. Tuttavia il thread di monitoraggio blocco non è in grado di rilevare il blocco nelle situazioni seguenti:
- Una delle sessioni in cui si verifica il blocco non è una sessione dell'agente di distribuzione.
- Un deadlock di sessione blocca le attività dell'agente di distribuzione.

In questo caso l'agente di distribuzione coordina tutte le sessioni in modo che eseguano il commit simultaneamente, non appena vengono eseguiti i relativi comandi. Un deadlock tra le sessioni si verifica quando sono vere le condizioni seguenti:

- Il blocco si verifica tra le sessioni dell'agente di distribuzione e una sessione che non è dell'agente di distribuzione.
- L'agente di distribuzione attende che tutte le sessioni completino l'esecuzione dei rispettivi comandi prima di coordinare il commit simultaneo delle sessioni.

Ad esempio si supponga di impostare il parametro *SubscriptionStreams* su 8. Le sessioni dalla 10 alla 17 sono sessioni dell'agente di distribuzione. La sessione 18 non è una sessione dell'agente di distribuzione. La sessione 10 è bloccata dalla sessione 18 e la sessione 18 è bloccata dalla sessione 11. È anche necessario che le sessioni 10 e 11 eseguano il commit contemporaneamente. Tuttavia l'agente di distribuzione non può eseguire insieme il commit delle sessioni 10 e 11 a causa del blocco. Pertanto l'agente di distribuzione non può coordinare il commit simultaneo di queste otto sessioni fino a quando la sessione 10 e la sessione 11 non completano l'esecuzione dei rispettivi comandi.

Il risultato di questo esempio è uno stato in cui nessuna sessione esegue i comandi corrispondenti. Quando viene raggiunto il tempo specificato nella proprietà **QueryTimeout**, l'agente di distribuzione annulla tutte le sessioni.

> [!Note]
> Per impostazione predefinita il valore della proprietà **QueryTimeout** è 5 minuti.

Durante questo periodo di timeout query è possibile rilevare le tendenze seguenti nei contatori delle prestazioni dell'agente di distribuzione: 

- Il valore del contatore delle prestazioni **Dist: Comandi recapitati/sec** è sempre 0.
- Il valore del contatore delle prestazioni **Dist: Transazioni recapitate/sec** è sempre 0.
- Il valore del contatore delle prestazioni **Dist: Latenza recapito** aumenta fino a quando non viene risolto il deadlock del thread.

L'argomento relativo all'agente di distribuzione repliche nella documentazione online di Microsoft SQL Server contiene la descrizione seguente per il parametro *SubscriptionStreams*: "Se si verifica un errore di esecuzione o di commit di una delle connessioni, tutte le connessioni interromperanno il batch corrente e l'agente utilizzerà un singolo flusso per ripetere i batch non riusciti".

L'agente di distribuzione usa una sessione per riprovare l'applicazione del batch che non era riuscita. Dopo aver applicato correttamente il batch, l'agente di distribuzione riprende l'uso di più sessioni senza riavviare il computer.

#### <a name="commitbatchsize"></a>CommitBatchSize
- Aumentare il valore del parametro **-CommitBatchSize** per l'agente di distribuzione.  
  
Il commit di un set di transazioni presenta un overhead fisso. Se si esegue il commit di un numero maggiore di transazioni con una frequenza minore, l'overhead viene distribuito in un volume più ampio di dati.  L'aumento di CommitBatchSize (fino a 200) può migliorare le prestazioni, perché viene eseguito il commit di più transazioni nel Sottoscrittore. Tuttavia, il vantaggio offerto dall'aumento del valore di questo parametro decade in quanto il costo dell'applicazione delle modifiche è controllato da altri fattori, come l'I/O massimo del disco che contiene il log. È anche necessario tenere presente che gli eventuali errori che causano il riavvio delle operazioni dell'agente di distribuzione richiedono l'esecuzione del rollback e la nuova applicazione di un numero maggiore di transazioni. Per le reti non affidabili, un valore più basso può generare meno errori nonché il rollback e la riapplicazione di un numero inferiore di transazioni in caso di errore.  
  

## <a name="see-more"></a>Altre informazioni
  
[Usare i profili agenti di replica](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
[Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
