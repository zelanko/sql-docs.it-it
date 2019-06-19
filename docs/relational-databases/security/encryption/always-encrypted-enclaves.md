---
title: Always Encrypted con enclave sicuri (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 377c2d95564e7348bdfb5de9480c7c7f5004c7f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938164"
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
> In [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], i calcoli avanzati sono in attesa di varie ottimizzazioni delle prestazioni, includono funzionalità limitate (nessuna indicizzazione e altro) e sono attualmente disabilitati per impostazione predefinita. Per abilitare i calcoli avanzati, vedere [Abilitare i calcoli avanzati](configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

In [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] Always Encrypted con enclave sicuri usa gli enclave di memoria sicuri di tipo [sicurezza basata su virtualizzazione](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) in Windows, noti anche come enclave in modalità protetta virtuale o VSM.

## <a name="secure-enclave-attestation"></a>Attestazione degli enclave sicuri

L'enclave sicuro all'interno del motore di SQL Server può accedere ai dati sensibili archiviati nelle colonne del database crittografate e alle corrispondenti chiavi di crittografia di colonna come testo non crittografato. Prima di inviare una query che comporta calcoli sull'enclave a SQL Server, il driver client all'interno dell'applicazione deve verificare che l'enclave sicuro sia originale in base a una determinata tecnologia (ad esempio la sicurezza basata su virtualizzazione) e che il codice in esecuzione all'interno dell'enclave sia stato firmato per l'esecuzione all'interno dell'enclave. 

Il processo di verifica dell'enclave è chiamato **attestazione dell'enclave** e implica in genere che un driver client all'interno dell'applicazione (e talvolta anche SQL Server) contatti un servizio di attestazione esterno. I dettagli specifici del processo di attestazione variano a seconda della tecnologia di enclave e del servizio di attestazione.

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

- **Crittografia deterministica** - Le colonne abilitate per l'enclave che usano la crittografia deterministica supportano la crittografia sul posto, ma non altre operazioni all'interno dell'enclave sicuro. Sono supportati confronti di uguaglianza, ma l'operazione viene eseguita al di fuori dell'enclave confrontando il testo crittografato (al di fuori dell'enclave).  
- **Crittografia casuale** - Le colonne abilitate per l'enclave che usano la crittografia causale supportano la crittografia sul posto, oltre a calcoli avanzati all'interno dell'enclave sicuro. I calcoli avanzati supportati sono criteri di ricerca e [operatori di confronto](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql), incluso il confronto di uguaglianza.

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

## <a name="known-limitations"></a>Limitazioni note

Limitazioni generali: 

- Tutte le limitazioni elencate per la versione corrente di Always Encrypted in [informazioni sulle funzionalità](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details) si applicano anche a Always Encrypted con enclave sicuri (per le colonne crittografate con chiavi abilitate per l'enclave), tranne le restrizioni rimosse aggiungendo il supporto per la crittografia sul posto e i calcoli avanzati.

- L'operatore per il confronto di uguaglianza rimane l'unico operatore Transact-SQL supportato con la crittografia deterministica e i confronti di uguaglianza vengono eseguiti tramite il confronto dei valori di testo crittografato al di fuori dell'enclave, indipendentemente dal fatto che la chiave di crittografia delle colonne sia abilitata o meno per l'enclave. Le operazioni di crittografia sul posto sono l'unica nuova funzionalità che diventa disponibile con le chiavi di crittografia di colonna abilitate per l'enclave per la crittografia deterministica. In presenza di una colonna crittografata tramite crittografia deterministica (e una chiave non abilitata per l'enclave), per abilitare i calcoli avanzati (criteri di ricerca, operazioni di confronto), è necessario crittografare nuovamente la colonna con la crittografia casuale.

- La restrizione esistente per l'uso delle regole di confronto si applica alle colonne crittografate con chiavi di crittografia di colonna abilitate per l'enclave: le colonne di tipo stringa di caratteri (char, nchar, varchar, nvarchar) crittografate tramite crittografia deterministica devono usare regole di confronto con ordinamento binario 2 (regole di confronto BIN2). Le colonne di tipo stringa di caratteri che usano regole di confronto diverse da BIN2 possono essere crittografate usando la crittografia casuale, tuttavia l'unica nuova funzionalità abilitata per questo tipo di colonne (se sono crittografate con chiavi di crittografia di colonna abilitate per l'enclave) è la crittografia sul posto. **Per supportare i calcoli avanzati (criteri di ricerca, operazioni di confronto), una colonna deve usare regole di confronto BIN2** e la colonna deve essere crittografata usando la crittografia casuale e una chiave di crittografia di colonna abilitata per l'enclave.

- L'uso di chiavi abilitate per l'enclave per le colonne in tabelle in memoria non è supportato.

- Non è possibile combinare le operazioni di crittografia sul posto con qualsiasi altra modifica dei metadati di colonna, ad eccezione delle modifiche delle regole di confronto e del supporto dei valori Null. Ad esempio, non è possibile crittografare, crittografare di nuovo, o decrittografare, una colonna E modificare un tipo di dati della colonna in un'unica istruzione Transact-SQL ALTER TABLE o ALTER COLUMN. È necessario usare due istruzioni separate.

Le limitazioni seguenti si applicano all'anteprima corrente, ma è previsto che vengano rimosse:

- Le colonne abilitate per l'enclave che usano la crittografia casuale non possono essere indicizzate, il che significa che per le operazioni di confronto o le operazioni LIKE sono richieste scansioni di tabella.

- Il solo driver client che supporta Always Encrypted con enclave sicuri è il provider di dati .NET Framework per SQL Server (ADO.NET) in .NET Framework 4.7.2. Non è disponibile alcun supporto ODBC/JDBC.

- Gli unici archivi di chiavi supportati per l'archiviazione di chiavi master della colonna abilitate per l'enclave sono Archivio certificati Windows e Azure Key Vault.

- Il supporto di strumenti per Always Encrypted con enclave sicuri è attualmente incompleto. Per attivare un'operazione di crittografia sul posto tramite un'istruzione Transact-SQL ALTER TABLE, è necessario eseguire l'istruzione tramite una finestra Query in SQL Server Management Studio oppure è possibile scrivere un programma personalizzato che esegue l'istruzione. Il cmdlet Set-SqlColumnEncryption nel modulo SqlServer PowerShell e la procedura guidata Always Encrypted in SQL Server Management Studio non supportano ancora la crittografia sul posto. Entrambi gli strumenti attualmente spostano i dati fuori dal database per le operazioni di crittografia, anche se le chiavi di crittografia di colonna usate per le operazioni sono abilitate per l'enclave. 

## <a name="known-issues"></a>Problemi noti

- Per i calcoli avanzati sulle colonne di tipo stringa non UNICODE (char, varchar) è necessario impostare le regole di confronto BIN2 a livello di database. Vedere Considerazioni speciali per le colonne di tipo stringa non UNICODE in [Gestire le regole di confronto](configure-always-encrypted-enclaves.md#manage-collations).

## <a name="next-steps"></a>Next Steps

- Configurare l'ambiente di test e provare le funzionalità di Always Encrypted con enclave sicuri in SSMS. Vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).
