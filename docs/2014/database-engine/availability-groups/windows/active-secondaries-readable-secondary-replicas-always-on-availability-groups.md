---
title: 'Repliche secondarie attive: Repliche secondarie leggibili (gruppi di disponibilità) Always On | Microsoft Docs'
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 78f3f81a-066a-4fff-b023-7725ff874fdf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86340f1bdb9b178c23295c61378d781e2d4a83cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62789853"
---
# <a name="active-secondaries-readable-secondary-replicas-always-on-availability-groups"></a>Repliche secondarie attive: Repliche secondarie leggibili (gruppi di disponibilità) Always On
  Le funzionalità secondarie attive di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] includono il supporto per l'accesso in sola lettura a una o più repliche secondarie (*repliche secondarie leggibili*). Una replica secondaria leggibile consente l'accesso in sola lettura a tutti i relativi database secondari. Tuttavia, i database secondari leggibili non sono impostati per la sola lettura. Sono dinamici. Un database secondario viene modificato in base ai cambiamenti apportati al database primario corrispondente. Per una replica secondaria tipica, i dati presenti nel database secondario, comprese le tabelle durevoli con ottimizzazione per la memoria, sono quasi in tempo reale. Inoltre, gli indici full-text sono sincronizzati con i database secondari. In molte circostanze, la latenza dei dati tra un database primario e il database secondario corrispondente è in genere solo di pochi secondi.  
  
 Le impostazioni di sicurezza nei database primari vengono rese persistenti nei database secondari. Sono inclusi utenti, ruoli del database e delle applicazioni insieme alle rispettive autorizzazioni, nonché Transparent Data Encryption (TDE), se abilitato nel database primario.  
  
> [!NOTE]  
>  Nonostante non sia possibile scrivere dati nei database secondari, è possibile scrivere nei database di lettura-scrittura dell'istanza del server in cui è ospitata la replica secondaria, inclusi i database utente e quelli di sistema come **tempdb**.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] supporta anche il reindirizzamento delle richieste di connessione con finalità di lettura a una replica secondaria leggibile (*routing di sola lettura*). Per informazioni sul routing di sola lettura, vedere [Uso di un listener per connettersi a una replica secondaria di sola lettura (routing di sola lettura)](../../listeners-client-connectivity-application-failover.md#ConnectToSecondary).  
  
 
  
##  <a name="bkmk_Benefits"></a> Vantaggi  
 L'indirizzamento di connessioni di sola lettura a repliche secondarie leggibili offre i seguenti vantaggi:  
  
-   Consente di scaricare i carichi di lavoro di sola lettura secondari dalla replica primaria, in cui sono conservate le relative risorse per i carichi di lavoro critici. In caso di carico di lavoro di lettura critico o di carico di lavoro per il quale non è possibile tollerare la latenza, si consiglia di effettuare la relativa esecuzione nella replica primaria.  
  
-   Consente di migliorare il rendimento dell'investimento per i sistemi in cui sono ospitate repliche secondarie leggibili.  
  
 Inoltre, le repliche secondarie leggibili forniscono un supporto affidabile per operazioni di sola lettura, come indicato di seguito:  
  
-   Le statistiche temporanee automatiche in un database secondario leggibile consentono di ottimizzare le query di sola lettura sulle tabelle basate su disco. Per le tabelle con ottimizzazione per la memoria, le statistiche mancanti vengono create automaticamente. Tuttavia, non è previsto alcun aggiornamento automatico delle statistiche non aggiornate. Sarà necessario aggiornare manualmente le statistiche nella replica primaria. Per altre informazioni, vedere [Statistiche](#Read-OnlyStats)per i database con accesso di sola lettura più avanti in questo argomento.  
  
-   Nei carichi di lavoro di sola lettura per le tabelle basate su disco viene usato il controllo delle versioni delle righe per rimuovere la contesa di blocco nei database secondari. Viene eseguito automaticamente il mapping a livello di transazioni di isolamento dello snapshot di tutte le query eseguite nei database secondari, anche quando gli altri livelli di isolamento delle transazioni sono impostati in modo esplicito. Tutti gli hint di blocco vengono ignorati. In questo modo si elimina la contesa lettore/writer.  
  
-   I carichi di lavoro di sola lettura per le tabelle ottimizzate per la memoria durevoli accedono ai dati esattamente nello stesso modo in cui si accede nel database primario, tramite le stored procedure native o l'interoperabilità SQL con le stesse limitazioni del livello di isolamento delle transazioni. Il carico di lavoro di report o le query di sola lettura in esecuzione nella replica primaria possono essere eseguiti nella replica secondaria senza richiedere alcuna modifica. Analogamente, un carico di lavoro di report o le query di sola lettura in esecuzione in una replica secondaria possono essere eseguiti nella replica primaria senza richiedere alcuna modifica.  In modo analogo alle tabelle basate su disco, viene eseguito automaticamente il mapping a livello di transazioni di isolamento dello snapshot di tutte le query eseguite nei database secondari, anche quando gli altri livelli di isolamento delle transazioni sono impostati in modo esplicito.  
  
-   Le operazioni DML sono consentite nelle variabili di tabella sia per i tipi di tabella basati su disco che per quelli con ottimizzazione per la memoria nella replica secondaria.  
  
##  <a name="bkmk_Prerequisites"></a> Prerequisiti per il gruppo di disponibilità  
  
-   **Repliche secondarie leggibili (obbligatorio)**  
  
     L'amministratore del database deve configurare una o più repliche in modo tale da consentire tutte le connessioni (solo per l'accesso in lettura) o solo le connessioni con finalità di lettura quando vengono eseguite nel ruolo secondario.  
  
    > [!NOTE]  
    >  Facoltativamente, l'amministratore del database può configurare le repliche di disponibilità per escludere le connessioni in sola lettura quando l'esecuzione avviene nel ruolo primario.  
  
     Per altre informazioni, vedere [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md).  
  
-   **Listener del gruppo di disponibilità**  
  
     Per supportare il routing di sola lettura, un gruppo di disponibilità deve possedere un [listener del gruppo di disponibilità](../../listeners-client-connectivity-application-failover.md). Il client in sola lettura deve indirizzare le richieste di connessione al listener e la stringa di connessione del client deve specificare la finalità dell'applicazione come in sola lettura, ovvero devono essere *richieste di connessione con finalità di lettura*.  
  
-   **Routing di sola lettura**  
  
     Con*routing di sola lettura* si intende la capacità di SQL Server di instradare le richieste di connessione in ingresso con finalità di lettura dirette a un listener del gruppo di disponibilità a una replica secondaria leggibile disponibile. I prerequisiti per il routing di sola lettura sono i seguenti:  
  
    -   Per supportare il routing di sola lettura una replica secondaria leggibile richiede un URL di routing di sola lettura. L'URL viene usato solo quando la replica locale viene eseguita nel ruolo secondario. L'URL di routing di sola lettura deve essere specificato per ogni singola replica in base alle esigenze. Ogni URL di routing di sola lettura viene usato per il routing delle richieste di connessione con finalità di lettura a una replica secondaria leggibile specifica. In genere, a ogni replica secondaria leggibile viene assegnato un URL di routing di sola lettura.  
  
    -   Ogni replica di disponibilità che deve supportare il routing di sola lettura quando viene eseguita come replica primaria richiede un elenco di routing di sola lettura. L'elenco di routing di sola lettura viene usato solo quando la replica locale viene eseguita nel ruolo primario. L'elenco deve essere specificato per ogni singola replica in base alle esigenze. In genere, ciascun elenco di routing di sola lettura deve contenere tutti gli URL di routing di sola lettura, con l'URL della replica locale alla fine dell'elenco.  
  
        > [!NOTE]  
        >  Le richieste di connessione con finalità di lettura vengono instradate alla prima replica secondaria leggibile disponibile nell'elenco di routing di sola lettura della replica primaria corrente. Non viene eseguito alcun bilanciamento del carico.  
  
     Per altre informazioni, vedere [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
> [!NOTE]  
>  Per informazioni sui listener del gruppo di disponibilità e altre informazioni sul routing di sola lettura, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="bkmk_LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Alcune operazioni non sono completamente supportate, come indicato di seguito:  
  
-   Non appena una replica leggibile viene abilitata per la lettura, può iniziare ad accettare connessioni ai relativi database secondari. Tuttavia, se in un database primario è presente una transazione attiva, le versioni di riga non saranno completamente disponibili nel database secondario corrispondente. È necessario eseguire il commit o il rollback di tutte le transazioni attive presenti nella replica primaria al momento della configurazione della replica secondaria. Fino a quando questo processo non viene completato, il mapping del livello di isolamento delle transazioni nel database secondario non è completo e le query sono temporaneamente bloccate.  
  
    > [!WARNING]  
    >  L'esecuzione di transazioni prolungate ha un impatto sul numero di righe con versione mantenute, sia per le tabelle basate su disco che per quelle ottimizzate per la memoria.  
  
-   In un database secondario con tabelle ottimizzate per la memoria, anche se le versioni di riga vengono generate sempre per le tabelle ottimizzate per la memoria, le query vengono bloccate finché non vengono completate tutte le transazioni attive presenti nella replica primaria quando la replica secondaria è stata abilitata per la lettura. In questo modo si garantisce che sia le tabelle basate su disco che quelle ottimizzate per la memoria siano disponibili contemporaneamente per il carico di lavoro di report e per le query di sola lettura.  
  
-   Le funzionalità di rilevamento delle modifiche e Change Data Capture non sono supportate nei database secondari che appartengono a una replica secondaria leggibile:  
  
    -   Il rilevamento delle modifiche è disabilitato in modo esplicito nei database secondari.  
  
    -   La funzionalità Change Data Capture può essere abilitata in un database secondario, ma ciò non è supportato.  
  
-   Dal momento che viene eseguito il mapping delle operazioni di lettura al livello di transazioni di isolamento dello snapshot, la pulizia di record fantasma nella replica primaria può essere bloccata dalle transazioni in una o più repliche secondarie. L'attività di pulizia di record fantasma consentirà di pulire automaticamente i record fantasma per le tabelle basate su disco nella replica primaria se non più necessari per qualsiasi replica secondaria.  Questa operazione è simile a quella che viene effettuata quando si eseguono transazioni nella replica primaria. In caso estremo, nel database secondario sarà necessario terminare una query di lettura a esecuzione prolungata nella replica secondaria tramite cui si blocca la pulizia fantasma. Si noti che la pulizia fantasma può essere bloccata se la replica secondaria è disconnessa o quando lo spostamento dati è sospeso nel database secondario. Questo stato impedisce inoltre il troncamento del log, pertanto se lo stato persiste, si consiglia di rimuovere il database secondario dal gruppo di disponibilità. Non esiste alcun problema di pulizia di record fantasma con le tabelle con ottimizzazione per la memoria perché le versioni di riga vengono mantenute nella memoria e sono indipendenti dalle versioni di riga nella replica primaria.  
  
-   Potrebbe verificarsi un errore durante l'operazione DBCC SHRINKFILE nei file contenenti le tabelle basate su disco nella replica primaria se nel file sono contenuti record fantasma ancora necessari in una replica secondaria.  
  
-   A partire da [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], le repliche secondarie leggibili possono rimanere online anche quando la replica primaria è offline a causa di un errore o di un'azione dell'utente. Tuttavia, il routing di sola lettura non funziona in questa situazione perché il listener del gruppo di disponibilità è offline. I client devono connettersi direttamente alle repliche secondarie di sola lettura per i carichi di lavoro in sola lettura.  
  
> [!NOTE]  
>  Se si esegue una query sulla DMV [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) in un'istanza del server che ospita una replica secondaria leggibile, potrebbe verificarsi un problema di blocco della fase di rollforward. Questa condizione si verifica perché la DMV acquisisce un blocco IS nella vista o nella tabella utente specificata che può bloccare le richieste di una fase di rollforward per un blocco X presente in tale vista o tabella utente.  
  
##  <a name="bkmk_Performance"></a> Considerazioni sulle prestazioni  
 In questa sezione si illustrano le diverse considerazioni sulle prestazioni relative ai database secondari leggibili.  
  
 
  
###  <a name="DataLatency"></a> Latenza dei dati  
 L'implementazione dell'accesso di sola lettura alle repliche secondarie è utile qualora i carichi di lavoro di sola lettura possono tollerare una certa latenza dei dati. Nelle situazioni in cui la latenza dei dati non può essere accettata, si consideri la possibilità di eseguire i carichi di lavoro di sola lettura nella replica primaria.  
  
 I record di log delle modifiche sul database primario vengono inviati dalla replica primaria alle repliche secondarie. In ogni database secondario i record di log vengono applicati tramite un thread della fase di rollforward dedicato. In un database secondario di accesso in lettura, una modifica ai dati specificata non viene visualizzata nei risultati della query fino a quando il record di log, in cui è contenuta la modifica, non sarà stato applicato al database secondario e non è stato eseguito il commit della transazione nel database primario.  
  
 Ciò significa che si verifica della latenza, in genere solo pochi secondi, tra la replica primaria e quella secondaria. In rari casi, tuttavia, ad esempio se problemi di rete compromettono la velocità effettiva, la latenza può diventare significativa. La latenza aumenta quando si verificano colli di bottiglia I/O e quando viene sospeso lo spostamento dati. Per monitorare lo spostamento dati sospeso, è possibile usare il [dashboard AlwaysOn](use-the-always-on-dashboard-sql-server-management-studio.md) o la DMV [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql) .  
  
####  <a name="bkmk_LatencyWithInMemOLTP"></a> Latenza dei dati nei database con tabelle ottimizzate per la memoria  
 Quando si accede alle tabelle ottimizzate per la memoria sulla replica secondaria per il carico di lavoro di lettura, viene usato un *timestamp di sicurezza* per restituire le righe dalle transazioni di cui è stato eseguito il commit prima del *timestamp di sicurezza*. Il timestamp di sicurezza è l'hint per il timestamp meno recente usato dal thread di Garbage Collection per eseguire il processo di Garbage Collection delle righe sulla replica primaria. Il timestamp viene aggiornato quando il numero delle transazioni DML nelle tabelle ottimizzate per la memoria supera una soglia interna dopo l'ultimo aggiornamento. Ogni volta che il timestamp della transazione meno recente viene aggiornato sulla replica primaria, la transazione DML successiva in una tabella ottimizzata per la memoria durevole invia tale timestamp perché venga inviato alla replica secondaria come parte di un record di log speciale. Nel thread della fase di rollforward nella replica secondaria il timestamp di sicurezza viene aggiornato come parte dell'elaborazione del record di log.  
  
#### <a name="the-impact-of-safe-timestamp-on-latency"></a>Impatto del timestamp di sicurezza sulla latenza  
  
-   Per i carichi di lavoro OLTP con velocità effettiva delle transazioni elevata, la latenza deve essere analoga alle tabelle basate su disco. È probabile che questo sia il caso più comune.  
  
-   Una transazione con esecuzione prolungata può determinare un ritardo arbitrario del timestamp di sicurezza.  Lo stesso succede quando si accede alle tabelle basate su disco in quanto il timestamp di isolamento dello snapshot è determinato dal commit della transazione meno recente.  
  
-   Le modifiche apportate dalle transazioni nella replica primaria dopo l'ultimo aggiornamento del timestamp di sicurezza non sono visibili nella replica secondaria fino alla trasmissione e all'aggiornamento successivi di tale timestamp. Se l'attività transazionale nella replica primaria viene arrestata prima che venga superata la soglia interna per l'aggiornamento del timestamp di sicurezza, le modifiche apportate dopo l'ultimo aggiornamento di tale timestamp non saranno visibili nella replica secondaria. Per risolvere questo problema, potrebbe essere necessario eseguire alcune transazioni DML in una tabella ottimizzata per la memoria durevole fittizia nella replica primaria. In alternativa, sebbene non consigliabile, è possibile forzare la spedizione del timestamp di sicurezza eseguendo un checkpoint manuale.  
  
#### <a name="monitoring-and-troubleshooting-data-latency-in-memory-optimized-tables"></a>Monitoraggio e risoluzione di problemi relativi alla latenza dei dati nelle tabelle ottimizzate per la memoria  
 È possibile individuare il timestamp di sicurezza eseguendo la query seguente sulla replica primaria  
  
```  
  
SELECT MAX(base_generation)   
   AS max_base_generation  
   FROM sys.dm_db_xtp_gc_cycle_stats  
GO  
  
```  
  
 È inoltre possibile identificare il timestamp di sicurezza usato nella replica secondaria eseguendo la query seguente contemporaneamente al carico di lavoro di lettura attivo.  
  
```  
  
SELECT begin_tsn   
   FROM sys.dm_db_xtp_transactions  
GO  
  
```  
  
###  <a name="ReadOnlyWorkloadImpact"></a> Impatto sui carichi di lavoro di sola lettura  
 Quando si configura una replica secondaria per l'accesso di sola lettura, nei carichi di lavoro di sola lettura dei database secondari si usano le risorse di sistema, ad esempio CPU e I/O (per le tabella basate su disco) dai thread della fase di rollforward, soprattutto se i carichi di lavoro di sola lettura nelle tabelle basate su disco prevedono l'esecuzione di molte operazioni di I/O. Non esiste alcun impatto I/O quando si accede alle tabelle con ottimizzazione per la memoria perché tutte le righe si trovano in memoria.  
  
 Inoltre, i carichi di lavoro di sola lettura nelle repliche secondarie possono bloccare le modifiche DDL (Data Definition Language) applicate tramite record di log.  
  
-   Anche se nelle operazioni di lettura non si accettano i blocchi condivisi a causa del controllo delle versioni delle righe, in queste operazioni si accettano i blocchi di stabilità dello schema (Sch-S) che possono bloccare le operazioni di rollforward tramite cui si applicano le modifiche DDL. Le operazioni DDL includono operazioni ALTER/DROP di tabelle e viste ma non operazioni DROP o ALTER di stored procedure. Se, quindi, ad esempio si elimina una tabella basata su disco o con ottimizzazione per la memoria nel database primario, quando il thread della fase di rollforward elabora il record del log per eliminare la tabella, deve acquisire un blocco SCH_M nella tabella e può essere bloccato da una query in esecuzione che accede alla tabella.  Si tratta dello stesso comportamento della replica primaria con la differenza che l'eliminazione della tabella viene eseguita come parte di una sessione utente e non di un thread della fase di rollforward.  
  
-   Per le tabelle con ottimizzazione per la memoria sono previsti blocchi aggiuntivi. Eliminare una stored procedure nativa può comportare il blocco del thread della fase di rollforward se avviene l'esecuzione simultanea della stored procedure nativa nella replica secondaria. Si tratta dello stesso comportamento della replica primaria con la differenza che l'eliminazione della stored procedure viene eseguita come parte di una sessione utente e non di un thread della fase di rollforward.  
  
 Valutare le procedure consigliate relative alla compilazione delle query e applicarle ai database secondari. Pianificare, ad esempio, le query a lunga esecuzione come aggregazioni di dati durante i periodi di minore attività.  
  
> [!NOTE]  
>  Se un thread della fase di rollforward è bloccato da query in una replica secondaria, viene generato l'oggetto XEvent **sqlserver.lock_redo_blocked** .  
  
###  <a name="bkmk_Indexing"></a> Indicizzazione  
 Per ottimizzare i carichi di lavoro di sola lettura nelle repliche secondarie leggibili, è possibile creare indici nelle tabelle dei database secondari. Poiché non è possibile apportare modifiche allo schema o ai dati nei database secondari, creare indici nei database primari e consentire il trasferimento delle modifiche al database secondario attraverso il processo di rollforward.  
  
 Per monitorare l'attività di utilizzo dell'indice in una replica secondaria, eseguire una query sulle colonne **user_seeks**, **user_scans**e **user_lookups** della DMV [sys.dm_db_index_usage_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql) .  
  
###  <a name="Read-OnlyStats"></a> Statistiche  
 Le statistiche sulle colonne di tabelle e viste indicizzate vengono usate per ottimizzare i piani di query. Per i gruppi di disponibilità, le statistiche create e gestite nei database primari vengono rese automaticamente persistenti nei database secondari come parte dell'applicazione dei record di log delle transazioni. Tuttavia, è possibile che per il carico di lavoro di sola lettura nei database secondari siano richieste statistiche diverse rispetto a quelle create nei database primari. Ad ogni modo, poiché i database secondari sono limitati all'accesso di sola lettura, non è possibile creare statistiche nei database secondari.  
  
 Per risolvere il problema, le statistiche temporanee per i database secondari vengono create e gestite dalla replica secondaria in **tempdb**. Il suffisso _readonly_database_statistic viene aggiunto al nome delle statistiche temporanee per distinguerle da quelle permanenti rese persistenti dal database primario.  
  
 Solo in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile creare e aggiornare le statistiche temporanee. È tuttavia possibile eliminare le statistiche temporanee e monitorare le relative proprietà usando gli stessi strumenti usati per le statistiche permanenti:  
  
-   Eliminare le statistiche temporanee usando l'istruzione [DROP STATISTICS](/sql/t-sql/statements/drop-statistics-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
-   Monitorare le statistiche usando le viste del catalogo **sys.stats** e **sys.stats_columns** . **sys_stats** include una colonna, **is_temporary**, che indica quali statistiche sono permanenti e quali invece temporanee.  
  
 L'aggiornamento automatico delle statistiche per le tabelle con ottimizzazione per la memoria nella replica primaria o secondaria non è supportato. È necessario monitorare i piani e le prestazioni delle query nella replica secondaria e aggiornare manualmente le statistiche nella replica primaria quando necessario. Tuttavia, le statistiche mancanti vengono create automaticamente sia nella replica primaria che in quella secondaria.  
  
 Per altre informazioni sulle statistiche di SQL Server, vedere [Statistiche](../../../relational-databases/statistics/statistics.md).  
  

  
####  <a name="StalePermStats"></a> Statistiche permanenti non aggiornate nei database secondari  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile rilevare situazioni in cui le statistiche permanenti in un database secondario non sono aggiornate. Tuttavia non è possibile apportare le modifiche alle statistiche permanenti se non modificando il database primario. Per l'ottimizzazione query, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile creare statistiche temporanee per le tabelle basate su disco nel database secondario e usarle al posto di quelle permanenti non aggiornate.  
  
 Quando le statistiche permanenti vengono aggiornate nel database primario, vengono rese automaticamente persistenti nel database secondario. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è quindi possibile usare le statistiche permanenti aggiornate che sono più recenti delle statistiche temporanee.  
  
 Se si esegue il failover del gruppo di disponibilità, le statistiche temporanee vengono eliminate in tutte le repliche secondarie.  
  
####  <a name="StatsLimitationsRestrictions"></a> Limitazioni e restrizioni  
  
-   Poiché le statistiche temporanee sono archiviate in **tempdb**, un riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comporta l'indisponibilità di tutte le statistiche temporanee.  
  
-   Il suffisso _readonly_database_statistic è riservato alle statistiche generate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Non è possibile usare questo suffisso quando si creano statistiche in un database primario. Per altre informazioni, vedere [Statistics](../../../relational-databases/statistics/statistics.md).  
  
##  <a name="bkmk_AccessInMemTables"></a> Accesso alle tabelle ottimizzate per la memoria in una replica secondaria  
 I livelli di isolamento del carico di lavoro di lettura nella replica secondaria sono solo quelli consentiti nella replica primaria. Non viene eseguito alcun mapping dei livelli di isolamento nella replica secondaria. In questo modo, un carico di lavoro di report, che può essere eseguito nella replica primaria, potrà essere eseguito nella replica secondaria senza richiedere alcuna modifica. Ciò semplifica la migrazione di un carico di lavoro di report dalla replica primaria a una secondaria o viceversa quando la replica secondaria non è disponibile.  
  
 L'esecuzione delle query seguenti avrà esito negativo nella replica secondaria, analogamente al modo in cui avviene per la replica primaria.  
  
-   Per le query in esecuzione solo nelle tabelle ottimizzate per la memoria, gli unici livelli di isolamento supportati sono snapshot, repeatable read e serializable. Tutte le query con livello di isolamento read uncommitted o read committed restituiscono un errore a meno che non sia abilitata l'opzione MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT a livello di database.  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL READ_COMMITTED  
    -- This is not allowed  
    BEGIN TRAN  
    SELECT * FROM t_hk  
    COMMIT  
  
    ```  
  
     Messaggio di errore:  
  
    ```  
    Msg 41368, Level 16, State 0, Line 2  
    Accessing memory optimized tables using the CREAD_COMMITTED isolation level is supported only for autocommit transactions. It is not supported for explicit or implicit transactions. Provide a supported isolation level for the memory optimized table using a table hing, such as WITH (SNAPSHOT).  
    ```  
  
-   Nelle tabelle ottimizzate per la memoria non sono supportati hint di blocco. Ad esempio, tutte le query seguenti generano un errore. Solo l'hint NOLOCK è consentito ed è un NOOP quando viene usato con le tabelle ottimizzate per la memoria.  
  
    ```sql  
    SELECT * FROM t_hk WITH (PAGLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (ROWLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (TABLOCK)  
    SELECT * FROM t_hk WITH (XLOCK)  
    SELECT * FROM t_hk WITH (UPDLOCK)  
    ```  
  
-   Per le transazioni tra contenitori, le transazioni con livello di isolamento della sessione "snapshot" che le tabelle ottimizzate per la memoria non è supportato l'accesso. Ad esempio,  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT  
    -- This is not allowed  
    BEGIN TRAN  
       SELECT * FROM t_hk  
    COMMIT  
    ```  
  
     Messaggio di errore:  
  
    ```  
    Msg 41332, Level 16, State 0, Line 5  
    Memory optimized tables and natively compiled stored procedures cannot be accessed or created when the session TRANSACTION ISOLATION LEVEL is set to SNAPSHOT.  
    ```  
  
##  <a name="bkmk_CapacityPlanning"></a> Considerazioni sulla pianificazione della capacità  
  
-   In caso di tabelle basate su disco, le repliche secondarie leggibili possono richiedere spazio in **tempdb** per due motivi:  
  
    -   Le versioni di riga vengono copiate dal livello di isolamento dello snapshot in **tempdb**.  
  
    -   Le statistiche temporanee per i database secondari vengono create e mantenute in **tempdb**. Le statistiche temporanee possono provocare un lieve aumento delle dimensioni di **tempdb**. Per altre informazioni, vedere [Statistiche per i database con accesso di sola lettura](#Read-OnlyStats)più avanti in questa sezione.  
  
-   Quando si configura l'accesso in lettura per una o più repliche secondarie, nei database primari vengono aggiunti 14 byte di overhead sulle righe di dati eliminate, modificate o inserite per archiviare i puntatori alle versioni di riga nei database secondari per le tabelle basate su disco. L'overhead di 14 byte viene trasferito ai database secondari. Poiché l'overhead di 14 byte viene aggiunto alle righe di dati, è possibile che si verifichino divisioni di pagina.  
  
     I dati della versione di riga non sono generati dai database primari. Al contrario, i database secondari generano le versioni di riga. Tuttavia, il controllo delle versioni delle righe aumenta l'archiviazione dei dati nei database primari e secondari.  
  
     L'aggiunta dei dati della versione di riga dipende dall'impostazione del livello di isolamento dello snapshot o di isolamento dello snapshot Read committed sul database primario. Nella tabella seguente viene descritto il comportamento del controllo delle versioni in un database secondario leggibile con impostazioni diverse per le tabelle basate su disco.  
  
    |Replica secondaria leggibile?|L'isolamento dello snapshot o l'isolamento dello snapshot Read Committed è abilitato?|Database primario|Database secondario|  
    |---------------------------------|-----------------------------------------------|----------------------|------------------------|  
    |No|no|Nessuna versione di riga né overhead di 14 byte|Nessuna versione di riga né overhead di 14 byte|  
    |No|Yes|Versioni di riga e overhead di 14 byte|Nessuna versione di riga, ma overhead di 14 byte|  
    |Yes|No|Nessuna versione di riga, ma overhead di 14 byte|Versioni di riga e overhead di 14 byte|  
    |Yes|Yes|Versioni di riga e overhead di 14 byte|Versioni di riga e overhead di 14 byte|  
  
##  <a name="bkmk_RelatedTasks"></a> Attività correlate  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
-   [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [SQL Server AlwaysOn Team Blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Statistiche](../../../relational-databases/statistics/statistics.md)  
  
  
