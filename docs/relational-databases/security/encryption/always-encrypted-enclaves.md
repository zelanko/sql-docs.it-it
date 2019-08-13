---
title: Always Encrypted con enclave sicuri (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 998594a4c0c649a0ad73d36e858cf733fc364aae
ms.sourcegitcommit: 9702dd51410dd610842d3576b24c0ff78cdf65dc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68841566"
---
# <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclave sicuri
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

 
Always Encrypted con enclave sicuri rende disponibili funzionalità aggiuntive per la funzionalità [Always Encrypted](always-encrypted-database-engine.md).

Introdotta in SQL Server 2016, la funzionalità Always Encrypted protegge la riservatezza dei dati sensibili da malware e utenti di SQL Server con privilegi elevati *non autorizzati*. Gli utenti non autorizzati con privilegi elevati sono gli amministratori di database, gli amministratori di computer, gli amministratori di cloud o altri utenti che possono accedere in modo legittimo a istanze del server, hardware e così via, ma che non dovrebbero avere accesso ad alcuni o a tutti i dati effettivi. 

Fino ad ora, Always Encrypted proteggeva i dati crittografandoli sul lato client e non consentendo mai ai dati o alle chiavi di crittografia corrispondenti di essere visualizzati come testo non crittografato all'interno del motore di SQL Server. Di conseguenza, le funzionalità per le colonne crittografate all'interno del database erano soggette a notevoli restrizioni. Le uniche operazioni che SQL Server poteva eseguire sui dati crittografati erano i confronti di uguaglianza e i confronti di uguaglianza erano disponibili solo con la crittografia deterministica. Tutte le altre operazioni, tra cui le operazioni di crittografia (crittografia iniziale dei dati o rotazione delle chiavi) o i calcoli avanzati (ad esempio, criteri di ricerca) non erano supportate all'interno del database. Gli utenti dovevano spostare i dati all'esterno del database per eseguire queste operazioni sul lato client.

Always Encrypted *con enclave sicuri* supera queste limitazioni, consentendo l'esecuzione di calcoli su dati di testo non crittografato all'interno di un enclave sicuro sul lato server. Un enclave sicuro è un'area protetta della memoria all'interno del processo di SQL Server e agisce come un ambiente di esecuzione affidabile per l'elaborazione dei dati sensibili all'interno del motore di SQL Server. Un enclave sicuro viene visualizzato come black box per il resto di SQL Server e altri processi nel computer host. Non vi è alcun modo per visualizzare dati o codice all'interno dell'enclave dall'esterno, anche con un debugger.  


Always Encrypted usa gli enclave sicuri come illustrato nel diagramma seguente:

![flusso di dati](./media/always-encrypted-enclaves/ae-data-flow.png)



Durante l'analisi della query di un'applicazione, il motore di SQL Server determina se la query contiene operazioni su dati crittografati che richiedono l'uso dell'enclave sicuro. Per le query che richiedono l'accesso all'enclave sicuro:

- Il driver del client invia le chiavi di crittografia della colonna necessarie per le operazioni all'enclave sicuro (tramite un canale sicuro). 
- Il driver del client invia quindi la query per l'esecuzione con i parametri di query crittografati.

Durante l'elaborazione della query, i dati o le chiavi di crittografia della colonna non vengono esposte come testo non crittografato nel motore di SQL Server di fuori dell'enclave sicuro. Il motore di SQL Server delega le operazioni di crittografia e i calcoli sulle colonne crittografate all'enclave sicuro. Se necessario, l'enclave sicuro decrittografa i parametri di query e/o i dati archiviati nelle colonne crittografate ed esegue le operazioni richieste.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>Motivi per usare Always Encrypted con enclave sicuri

Con gli enclave sicuri, Always Encrypted protegge la riservatezza dei dati sensibili offrendo al contempo i vantaggi seguenti:

- **Crittografia sul posto** - Le operazioni di crittografia su dati sensibili, ad esempio la crittografia iniziale dei dati o la rotazione di una chiave di crittografia della colonna, vengono eseguite all'interno dell'enclave sicuro e non richiedono lo spostamento di dati all'esterno del database. È possibile eseguire la crittografia sul posto tramite l'istruzione Transact-SQL ALTER TABLE e non è necessario usare strumenti, come la procedura guidata Always Encrypted in SQL Server Management Studio o il cmdlet di PowerShell Set-SqlColumnEncryption.

- **Calcoli avanzati (anteprima)** - Le operazioni su colonne crittografate, tra cui criteri di ricerca (come il predicato LIKE) e i confronti degli intervalli, sono supportate all'interno dell'enclave sicuro, che consente di rendere disponibile Always Encrypted per una vasta gamma di applicazioni e scenari che richiedono l'esecuzione di questo tipo di calcoli all'interno del sistema di database.

> [!IMPORTANT]
> In [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] i calcoli avanzati sono in attesa di ottimizzazioni delle prestazioni e miglioramenti alla gestione degli errori e sono attualmente disabilitati per impostazione predefinita. Per abilitare i calcoli avanzati, vedere [Abilitare i calcoli avanzati](configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

In [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] Always Encrypted con enclave sicuri usa gli enclave di memoria sicuri di tipo [sicurezza basata su virtualizzazione](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) in Windows, noti anche come enclave in modalità protetta virtuale o VSM.

## <a name="secure-enclave-attestation"></a>Attestazione degli enclave sicuri

L'enclave sicuro all'interno del motore di SQL Server può accedere ai dati sensibili archiviati nelle colonne del database crittografate e alle corrispondenti chiavi di crittografia di colonna come testo non crittografato. Prima di inviare una query che comporta calcoli sull'enclave a SQL Server, il driver client all'interno dell'applicazione deve verificare che l'enclave sicuro sia originale in base a una determinata tecnologia (ad esempio la sicurezza basata su virtualizzazione) e che il codice in esecuzione all'interno dell'enclave sia stato firmato per l'esecuzione all'interno dell'enclave. 

Il processo di verifica dell'enclave è chiamato **attestazione dell'enclave** e implica in genere che un driver client all'interno dell'applicazione e SQL Server contattino un servizio di attestazione esterno. I dettagli specifici del processo di attestazione variano a seconda della tecnologia di enclave e del servizio di attestazione.

Il processo di attestazione supportato da SQL Server per gli enclave sicuri di sicurezza basata su virtualizzazione in [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] è l'attestazione di runtime di System Guard di Windows Defender, che usa il servizio Sorveglianza host (HGS) come servizio di attestazione. È necessario configurare il servizio HGS nell'ambiente in uso e registrare il computer che ospita l'istanza di SQL Server nel servizio HGS. È anche necessario configurare le applicazioni client o gli strumenti (ad esempio, SQL Server Management Studio) con un'attestazione di HGS.

## <a name="secure-enclave-providers"></a>Provider di enclave sicuri

Per usare Always Encrypted con enclave sicuri, un'applicazione deve usare un driver client che supporta la funzionalità. In [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] l'applicazione deve usare .NET Framework 4.7.2 e il provider di dati .NET Framework per SQL Server. Inoltre, le applicazioni .NET devono essere configurate con un **provider di enclave sicuri** specifico per il tipo di enclave (ad esempio sicurezza basata su virtualizzazione) e il servizio di attestazione (ad esempio, HGS) in uso. I provider di enclave supportati sono forniti separatamente in un pacchetto NuGet, che è necessario integrare con l'applicazione. Un provider di enclave implementa la logica lato client per il protocollo di attestazione e per stabilire un canale sicuro con un enclave sicuro di un determinato tipo.

## <a name="enclave-enabled-keys"></a>Chiavi abilitate per l'enclave

Always Encrypted con enclave sicuri introduce il concetto di chiavi abilitate per l'enclave:

- **Chiave master di colonna abilitata per l'enclave** - Chiave master della colonna con la proprietà ENCLAVE_COMPUTATIONS specificata nell'oggetto metadati chiave master della colonna all'interno del database. L'oggetto metadati chiave master della colonna deve anche contenere una firma valida delle proprietà dei metadati.
- **Chiave di crittografia di colonna abilitata per l'enclave** - Chiave di crittografia di colonna crittografata con una chiave master della colonna abilitata per l'enclave.

Quando il motore di SQL Server determina che le operazioni, specificate in una query, devono essere eseguite all'interno dell'enclave protetta, il motore di SQL Server richiede al driver client d condividere le chiavi di crittografia di colonna necessarie per i calcoli con l'enclave sicuro. Il driver client condivide le chiavi di crittografia di colonna solo se le chiavi sono abilitate per l'enclave (ovvero, crittografate con chiavi master della colonna abilitate per l'enclave) e sono firmate correttamente. In caso contrario, la query ha esito negativo.

## <a name="enclave-enabled-columns"></a>Colonne abilitate per l'enclave

Una colonna abilitata per l'enclave è una colonna del database crittografata con una chiave di crittografia di colonna abilitata per l'enclave. Le funzionalità disponibili per una colonna abilitata per l'enclave dipendono dal tipo di crittografia usato dalla colonna.

- **Crittografia deterministica** - Le colonne abilitate per l'enclave che usano la crittografia deterministica supportano la crittografia sul posto, ma non altre operazioni all'interno dell'enclave sicuro. Sono supportati confronti di uguaglianza, ma l'operazione viene eseguita confrontando il testo crittografato al di fuori dell'enclave.  
- **Crittografia casuale** - Le colonne abilitate per l'enclave che usano la crittografia causale supportano la crittografia sul posto, oltre a calcoli avanzati all'interno dell'enclave sicuro. I calcoli avanzati supportati sono criteri di ricerca e [operatori di confronto](../../../t-sql/language-elements/comparison-operators-transact-sql.md), incluso il confronto di uguaglianza.

Per altre informazioni sui tipi di crittografia, vedere [Crittografia Always Encrypted](always-encrypted-cryptography.md).

La tabella seguente riepiloga le funzionalità disponibili per le colonne crittografate, a seconda che le colonne usino le chiavi di crittografia di colonna abilitate per l'enclave e un tipo di crittografia.

| **Operazione**| **La colonna NON è abilitata per l'enclave** |**La colonna NON è abilitata per l'enclave**| **La colonna è abilitata per l'enclave**  |**La colonna è abilitata per l'enclave** |
|:---|:---|:---|:---|:---|
| | **Crittografia casuale**  | **Crittografia deterministica**     | **Crittografia casuale**      | **Crittografia deterministica**     |
| **Crittografia sul posto** | Non supportato  | Non supportato   | Supportato         | Supportato    |
| **Confronto di uguaglianza**   | Non supportato | Supportato all'esterno dell'enclave | Supportato all'interno dell'enclave | Supportato all'esterno dell'enclave |
| **Operatori di confronto oltre quello di uguaglianza** | Non supportato  | Non supportato   | Supportato      | Non supportato     |
| **LIKE**    | Non supportato      | Non supportato    | Supportato     | Non supportato    |

La crittografia sul posto include il supporto per le operazioni seguenti all'interno dell'enclave:

- Crittografia iniziale dei dati archiviati in una colonna esistente.
- Riesecuzione della crittografia dei dati esistenti in una colonna, ad esempio:
  
  - Rotazione della chiave di crittografia di colonna (crittografare nuovamente la colonna con una nuova chiave).
  - Modifica del tipo di crittografia.  

- Decrittografia dei dati archiviati in una colonna crittografata (conversione della colonna in colonna di testo non crittografato).

Affinché la crittografia sul posto sia possibile, la chiave (o le chiavi) di crittografia di colonna, coinvolte nelle operazioni di crittografia, devono essere abilitate per l'enclave:

- Crittografia iniziale: la chiave di crittografia di colonna per la colonna da crittografare deve essere abilitata per l'enclave.
- Riesecuzione della crittografia: sia la chiave di crittografia di colonna corrente che quella di destinazione (se diversa da quella corrente) devono essere abilitate per l'enclave.
- Decrittografia: la chiave di crittografia di colonna corrente della colonna deve essere abilitata per l'enclave.

### <a name="indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Indici sulle colonne abilitate per l'enclave tramite la crittografia casuale
È possibile creare indici non cluster sulle colonne abilitate per l'enclave tramite la crittografia casuale per velocizzare l'esecuzione delle query avanzate. Per garantire che un indice su una colonna crittografata tramite la crittografia casuale non determini una perdita di dati sensibili e, allo stesso tempo, sia utile per l'elaborazione delle query all'interno dell'enclave, i valori di chiave nella struttura dei dati di indice (albero B) sono crittografati e ordinati in base ai relativi valori di testo non crittografato. Quando l'utilità di esecuzione query nel motore di SQL Server usa un indice su una colonna crittografata per i calcoli all'interno dell'enclave, esegue una ricerca nell'indice dei valori specifici archiviati nella colonna. Ogni ricerca può implicare più confronti. L'utilità di esecuzione query delega ogni confronto all'enclave, che decrittografa un valore archiviato nella colonna e il valore della chiave di indice crittografata da confrontare, esegue il confronto in testo non crittografato e restituisce il risultato del confronto all'utilità di esecuzione. Per informazioni generali (non specifiche di Always Encrypted) sul funzionamento dell'indicizzazione in SQL Server, vedere [Descrizione di indici cluster e non cluster](../../indexes/clustered-and-nonclustered-indexes-described.md).

Poiché un indice su una colonna abilitata per l'enclave che usa la crittografia casuale archivia i valori della chiave di indice crittografati mentre i valori sono ordinati in base al testo non crittografato, il motore di SQL Server deve usare l'enclave per qualsiasi operazione che comporta la creazione o aggiornamento di un indice, tra cui:
- Creazione o ricompilazione di un indice.
- Inserimento, aggiornamento o eliminazione di una riga nella tabella (contenente una colonna indicizzata/crittografata), che attiva l'inserimento e/o la rimozione di una chiave di indice nell'indice.
- Esecuzione di comandi DBCC che comportano la verifica dell'integrità degli indici, ad esempio [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) oppure [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
- Ripristino del database (ad esempio, dopo il riavvio di SQL Server in seguito a un errore), se SQL Server deve annullare eventuali modifiche all'indice (vedere di seguito).

Tutte le operazioni precedenti richiedono che l'enclave disponga della chiave di crittografia della colonna per la colonna indicizzata, in modo da poter decrittografare le chiavi di indice. In generale, l'enclave può ottenere una chiave di crittografia della colonna in due modi:

- **Direttamente dall'applicazione client** che ha richiamato l'operazione sull'indice, come descritto nella sezione introduttiva precedente. Questo metodo richiede che l'applicazione o l'utente abbia accesso alla chiave master della colonna e alla chiave di crittografia della colonna, che proteggono la colonna indicizzata. L'applicazione deve connettersi al database con Always Encrypted abilitato per la connessione.
- **Dalla cache delle chiavi di crittografia della colonna.** L'enclave archivia le chiavi, usate nelle query precedenti, nella cache all'interno dell'enclave, che pertanto non è accessibile dall'esterno. Se un'applicazione attiva un'operazione su un indice senza specificare direttamente la chiave di crittografia della colonna richiesta, l'enclave cerca la chiave nella cache. Se l'enclave trova la chiave nella cache, la usa per l'operazione. Questo metodo consente agli amministratori di database di gestire gli indici e di eseguire determinate operazioni di pulizia dei dati (ad esempio, la rimozione di una riga da una tabella che contiene un indice su una colonna crittografata), senza dover accedere alle chiavi di crittografia o ai dati in testo non crittografato. Questo metodo richiede che l'applicazione si connetta al database senza Always Encrypted abilitato per la connessione.

La creazione di indici su colonne che usano la crittografia casuale e non sono abilitate per l'enclave non è supportata.

#### <a name="database-recovery"></a>Ripristino del database

Se si verifica un errore in un'istanza di SQL Server, i relativi database possono rimanere in uno stato in cui i file di dati possono contenere alcune modifiche da transazioni incomplete. Quando l'istanza viene avviata, viene eseguito un processo denominato [ripristino del database](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started), che implica il rollback di tutte le transazioni incomplete rilevate nel log delle transazioni per salvaguardare l'integrità del database. Se una transazione incompleta ha apportato modifiche a un indice, anche tali modifiche devono essere annullate. Ad esempio, potrebbe essere necessario rimuovere o reinserire alcuni valori di chiave nell'indice.

> [!IMPORTANT]
> Microsoft consiglia di abilitare il [ripristino accelerato del database](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) nel database **prima** di creare il primo indice su una colonna abilitata per l'enclave crittografata con la crittografia casuale.

Con il [tradizionale processo di ripristino del database](https://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (che segue il modello di ripristino [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)), per annullare una modifica a un indice, SQL Server deve attendere che un'applicazione fornisca all'enclave la chiave di crittografia della colonna, operazione che può richiedere molto tempo. Il ripristino accelerato del database riduce notevolmente il numero di operazioni di annullamento che devono essere rinviate perché una chiave di crittografia della colonna non è disponibile nella cache all'interno dell'enclave. Di conseguenza, incrementa notevolmente la disponibilità del database, riducendo al minimo la possibilità che una nuova transazione resti bloccata. Con il ripristino accelerato del database abilitato, SQL Server potrebbe comunque richiedere una chiave di crittografia della colonna per completare la pulizia delle versioni precedenti dei dati, ma esegue tale operazione come un'attività in background che non influisce sulla disponibilità delle transazioni del database o degli utenti. Potrebbero tuttavia essere visualizzati messaggi di errore nel log degli errori, che indicano operazioni di pulizia non riuscite a causa di una chiave di crittografia della colonna mancante.

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>Indici sulle colonne abilitate per l'enclave tramite la crittografia deterministica

Un indice su una colonna con crittografia deterministica è ordinato in base al testo crittografato (non al testo non crittografato), indipendentemente dal fatto che la colonna sia abilitata per l'enclave o meno.

## <a name="security-considerations"></a>Considerazioni sulla sicurezza

Le considerazioni sulla sicurezza seguenti si applicano ad Always Encrypted con enclave sicuri.

- La sicurezza dei dati all'interno dell'enclave dipende da un protocollo di attestazione e un servizio di attestazione. È pertanto necessario assicurarsi che il servizio di attestazione e i criteri di attestazione applicati da tale servizio vengano gestiti da un amministratore attendibile. Inoltre, i servizi di attestazione in genere supportano diversi criteri e protocolli di attestazione, alcuni dei quali eseguono una verifica minima dell'enclave e del relativo ambiente e sono progettati per il test e lo sviluppo. Seguire attentamente le linee guida specifiche per il servizio di attestazione in uso, in modo da assicurarsi di usare le configurazioni e i criteri consigliati per le distribuzioni di produzione. 
- La crittografia di una colonna tramite la crittografia casuale con una chiave CEK abilitata per l'enclave può comportare la divulgazione dell'ordine dei dati archiviati nella colonna, in quanto tali colonne supportano i confronti degli intervalli. Ad esempio, se una colonna crittografata che contiene gli stipendi dei dipendenti dispone di un indice, un amministratore di database malintenzionato potrebbe analizzare l'indice per trovare il valore crittografato dello stipendio massimo e identificare la persona con lo stipendio massimo (presupponendo che il nome della persona non sia crittografato). 
- Se si usa Always Encrypted per proteggere i dati sensibili dall'accesso non autorizzato da parte degli amministratori di database, non condividere le chiavi master della colonna o le chiavi di crittografia della colonna con gli amministratori di database. Un amministratore di database può gestire gli indici nelle colonne crittografate senza avere accesso diretto alle chiavi, sfruttando la cache delle chiavi di crittografia di colonna all'interno dell'enclave.

## <a name="anchorname-1-considerations-availability-groups-db-migration"></a> Considerazioni sui gruppi di disponibilità e sulla migrazione dei database

Quando si configura un gruppo di disponibilità Always On che è richiesto per supportare le query che usano gli enclave, è necessario assicurarsi che tutte le istanze di SQL Server che ospitano i database nel gruppo di disponibilità supportino Always Encrypted con enclave sicuri e che sia stato configurato un enclave. Se gli enclave sono supportati dal database primario, ma non da una replica secondaria, qualsiasi query che tenta di usare la funzionalità Always Encrypted con enclave sicuri avrà esito negativo.

Quando si ripristina un file di backup di un database che usa la funzionalità Always Encrypted con enclave sicuri in un'istanza di SQL Server in cui non è configurato l'enclave, l'operazione di ripristino avrà esito positivo e tutte le funzionalità che non usano l'enclave saranno disponibili. Tuttavia, tutte le query successive che usano la funzionalità dell'enclave avranno esito negativo e gli indici sulle colonne abilitate per l'enclave che usano la crittografia casuale non saranno più validi. Lo stesso vale quando si collega un database con Always Encrypted con enclave sicuri nell'istanza in cui non è configurato l'enclave.

Se il database include indici sulle colonne abilitate per l'enclave con crittografia casuale, assicurarsi di abilitare il [ripristino accelerato del database](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) nel database prima di creare un backup del database. Il ripristino accelerato del database garantirà che il database, inclusi gli indici, sarà immediatamente disponibile dopo il ripristino del database. Per altre informazioni, vedere [Ripristino del database](#database-recovery).

Quando si esegue la migrazione del database tramite un file bacpac, è necessario accertarsi di eliminare tutti gli indici sulle colonne abilitate per l'enclave con crittografia casuale prima di creare il file bacpac.

## <a name="known-limitations"></a>Limitazioni note

Gli enclave sicuri migliorano le funzionalità di Always Encrypted. Le funzionalità seguenti **ora sono supportate per le colonne abilitate per l'enclave**:

- Operazioni di crittografia sul posto.
- Criteri di ricerca (LIKE) e operatori di confronto nella colonna crittografata con la crittografia casuale.
    > [!NOTE]
    > Le operazioni precedenti sono supportate per le colonne di tipo stringa di caratteri che usano le regole di confronto con un ordinamento binary2 (regole di confronto BIN2). Le colonne di tipo stringa di caratteri che usano regole di confronto non BIN2 possono essere crittografate tramite crittografia casuale e chiavi di crittografia di colonna abilitate per l'enclave. Tuttavia, l'unica nuova funzionalità abilitata per questo tipo di colonne è la crittografia sul posto.
- Creazione di indici non cluster sulle colonne con crittografia casuale.

Tutte le altre limitazioni (non interessate dai miglioramenti precedenti) elencate per Always Encrypted (senza enclave sicuri) in [Informazioni sulle funzionalità](always-encrypted-database-engine.md#feature-details) si applicano anche ad Always Encrypted con enclave sicuri.

Le limitazioni seguenti sono specifiche per Always Encrypted con enclave sicuri:

- Non è possibile creare indici cluster sulle colonne abilitate per l'enclave che usano la crittografia casuale.
- Le colonne abilitate per l'enclave che usano la crittografia casuale non possono essere colonne chiave primaria e non è possibile farvi riferimento da vincoli di chiave esterna o vincoli di chiave univoca.
- Gli hash join e i merge join nelle colonne abilitate per l'enclave che usano la crittografia casuale non sono supportati. Sono supportati solo i join a cicli annidati (che usano indici, se disponibili).
- Le query con l'operatore LIKE o un operatore di confronto con un parametro di query che usa uno dei seguenti tipi di dati (che dopo la crittografia, diventano oggetti di grandi dimensioni) ignorano gli indici ed eseguono scansioni di tabella.
    - nchar[n] e nvarchar[n], se n è maggiore di 3967.
    - char[n], varchar[n], binary[n], varbinary[n], se n è maggiore di 7935.
- Non è possibile combinare le operazioni di crittografia sul posto con qualsiasi altra modifica dei metadati di colonna, ad eccezione della modifica delle regole di confronto all'interno della stessa tabella codici e del supporto dei valori Null. Ad esempio, non è possibile crittografare, crittografare di nuovo, o decrittografare, una colonna E modificare un tipo di dati della colonna in un'unica istruzione Transact-SQL ALTER TABLE o ALTER COLUMN. Usare due istruzioni separate.
- L'uso di chiavi abilitate per l'enclave per le colonne in tabelle in memoria non è supportato.
- Le espressioni che definiscono le colonne calcolate non possono eseguire alcun calcolo sulle colonne abilitate per gli enclave usando la crittografia casuale (anche se i calcoli sono confronti tra intervalli e di tipo LIKE).
- Gli unici archivi di chiavi supportati per l'archiviazione di chiavi master della colonna abilitate per l'enclave sono Archivio certificati Windows e Azure Key Vault.

Le limitazioni seguenti si applicano a [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], ma è previsto che vengano rimosse:

- La creazione di statistiche per le colonne abilitate per l'enclave che usano la crittografia casuale non è supportata.
- Il solo driver client che supporta Always Encrypted con enclave sicuri è il provider di dati .NET Framework per SQL Server (ADO.NET) in .NET Framework 4.7.2. ODBC/JDBC non è supportato.
- Il supporto di strumenti per Always Encrypted con enclave sicuri è attualmente incompleto. In particolare:
  - L'importazione e l'esportazione di database che contengono chiavi abilitate per l'enclave non sono supportate.
  - Per attivare un'operazione di crittografia sul posto tramite un'istruzione Transact-SQL ALTER TABLE, è necessario eseguire l'istruzione tramite una finestra Query in SQL Server Management Studio oppure è possibile scrivere un programma personalizzato che esegue l'istruzione. Il cmdlet Set-SqlColumnEncryption nel modulo SqlServer PowerShell e la procedura guidata Always Encrypted in SQL Server Management Studio non supportano ancora la crittografia sul posto. Entrambi gli strumenti attualmente spostano i dati fuori dal database per le operazioni di crittografia, anche se le chiavi di crittografia di colonna usate per le operazioni sono abilitate per l'enclave.
- I comandi DBCC che verificano l'integrità degli indici o l'aggiornamento degli indici non sono supportati.
- Creazione di indici sulle colonne crittografate al momento della creazione della tabella (tramite CREATE TABLE). È necessario creare un indice su una colonna crittografata separatamente tramite CREATE INDEX.

## <a name="next-steps"></a>Passaggi successivi

- Configurare l'ambiente di test e provare le funzionalità di Always Encrypted con enclave sicuri in SSMS. Vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).
- Per informazioni su come usare Always Encrypted con enclave sicuri, vedere [Configurare Always Encrypted con enclave sicuri](configure-always-encrypted-enclaves.md).
