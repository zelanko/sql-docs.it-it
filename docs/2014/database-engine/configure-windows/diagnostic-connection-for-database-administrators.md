---
title: Connessione di diagnostica per gli amministratori di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5e8022dd9a7bd4f301ca55f60614e1b13369b804
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810422"
---
# <a name="diagnostic-connection-for-database-administrators"></a>Connessione di diagnostica per gli amministratori di database
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre una speciale connessione di diagnostica a cui possono ricorrere gli amministratori quando non è possibile usare connessioni standard al server. Questa connessione di diagnostica consente a un amministratore di accedere a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire query di diagnostica e risolvere problemi anche quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non risponde alle richieste di connessione standard.  
  
 Questa connessione amministrativa dedicata (DAC, Dedicated Administrator Connection) supporta la crittografia e altre caratteristiche di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La connessione DAC consente solo il cambiamento del contesto utente in un altro utente con privilegi amministrativi.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito ogni possibile tentativo per garantire la connessione DAC, tuttavia in alcune situazioni particolari potrebbe verificarsi un errore.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="connecting-with-dac"></a>Connessione DAC  
 Per impostazione predefinita, la connessione è consentita solo da un client in esecuzione sul server. Le connessioni di rete non sono consentite, a meno che non siano configurate con la stored procedure sp_configure con l'opzione [remote admin connections](remote-admin-connections-server-configuration-option.md).  
  
 Solo i membri del ruolo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin possono stabilire la connessione DAC.  
  
 L'applicazione livello dati è disponibile e supportata con l'utilità del prompt dei comandi **sqlcmd** usando un'opzione di amministrazione speciale ( **-A**). Per altre informazioni sull'uso di **sqlcmd**, vedere [Utilizzo di sqlcmd con variabili di scripting](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md). È anche possibile connessione apponendo il prefisso `admin:`al nome dell'istanza nel formato **sqlcmd - Sadmin:** _< nome_istanza >._ È anche possibile avviare un'applicazione livello dati da un [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor di Query tramite la connessione al `admin:` \< *nome_istanza*>.  
  
## <a name="restrictions"></a>Restrictions  
 Dato che l'applicazione livello dati ha il solo scopo di consentire la diagnosi di problemi del server in rare circostanze, vi sono alcune restrizioni nella connessione:  
  
-   Per garantire che vi siano risorse disponibili per la connessione, per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è consentita un'unica connessione DAC. Se è già attiva una connessione DAC, qualsiasi nuova richiesta di connessione attraverso la connessione DAC viene negata e restituisce l'errore 17810.  
  
-   Per risparmiare risorse, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] non rimane in attesa sulla porta DAC, a meno che non sia avviato con un flag di traccia 7806.  
  
-   La connessione DAC tenta inizialmente di connettersi al database predefinito associato all'account di accesso. Quando la connessione è stata stabilita con esito positivo, è possibile connettersi al database master. Se il database predefinito è offline o altrimenti non disponibile, la connessione restituisce l'errore 4060. Essa avrà comunque esito positivo se si stabilisce la connessione al database master invece che al database predefinito utilizzando il comando seguente:  
  
     **sqlcmd -A -d master**  
  
     È consigliabile connettersi mediante connessione DAC al database master poiché se l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] è avviata, master sarà certamente disponibile.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente l'esecuzione di query parallele o comandi con la connessione DAC. Se, ad esempio, una delle istruzioni seguenti viene eseguita con la connessione DAC, viene generato l'errore 3637:  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   Con la connessione DAC è garantita la disponibilità di risorse limitate. Non utilizzare l'applicazione livello dati per eseguire query che utilizzano un'elevata quantità di risorse (ad esempio un join complesso in una grande tabella) o per eseguire query che possono bloccarsi. Questa misura consente di evitare che la connessione DAC aggravi gli eventuali problemi già esistenti sul server. Per evitare l'insorgere di potenziali scenari di blocco, quando è necessario eseguire query che potrebbero causare blocchi, eseguire la query in livelli di isolamento dello snapshot, se possibile, in caso contrario impostare il livello di isolamento della transazione su READ UNCOMMITTED, impostare il valore LOCK_TIMEOUT su un intervallo di tempo breve, ad esempio 2000 millisecondi, oppure adottare entrambe le misure. In questo modo si eviterà il blocco della sessione della connessione DAC. A seconda dello stato corrente in cui si trova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tuttavia, la sessione della connessione DAC potrebbe bloccarsi su un latch. Potrebbe essere possibile terminare la sessione della connessione DAC utilizzando la combinazione di tasti CTRL-C, ma l'esito dell'operazione non è sicuro. Se l'esito non è positivo, l'unica possibilità potrebbe consistere nel riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per garantire la connettività e la risoluzione dei problemi con la connessione DAC, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riserva risorse limitate all'elaborazione dei comandi eseguiti sulla connessione DAC. Generalmente queste risorse sono sufficienti solo per semplici funzioni di diagnostica e risoluzione dei problemi, quali ad esempio quelle elencate di seguito.  
  
 Sebbene sia teoricamente possibile eseguire qualsiasi istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che non richiede l'esecuzione in parallelo sulla connessione DAC, è consigliabile limitare l'utilizzo ai comandi di diagnostica e di risoluzione dei problemi seguenti:  
  
-   Query di viste a gestione dinamica per diagnostica di base, quali sys.dm_tran_locks per lo stato di blocco, sys.dm_os_memory_cache_counters per verificare l'integrità delle cache e sys.dm_exec_requests e sys.dm_exec_sessions per richieste e sessioni attive. Evitare viste a gestione dinamica che utilizzano una grande quantità di risorse, ad esempio sys.dm_tran_version_store che analizza l'intero archivio delle versioni e può causare un numero elevato di operazioni I/O, oppure join complessi. Per informazioni sulle implicazioni a livello di prestazioni, vedere la documentazione relativa alla [vista a gestione dinamica specifica](../../relational-databases/views/views.md).  
  
-   Query di viste del catalogo.  
  
-   Comandi DBCC di base quali DBCC FREEPROCCACHE, DBCC FREESYSTEMCACHE, DBCC DROPCLEANBUFFERS`,` e DBCC SQLPERF. Non eseguire comandi che usano una grande quantità di risorse, ad esempio **DBCC** CHECKDB, DBCC DBREINDEX o DBCC SHRINKDATABASE.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] comando KILL *\<spid>* . In base allo stato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il comando KILL potrebbe non avere sempre esito positivo. In questo caso, l'unica possibilità potrebbe consistere nel riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Di seguito vengono riportate alcune linee guida generali:  
  
    -   Verificare che lo SPID sia stato effettivamente terminato eseguendo la query `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`. Se non viene restituita alcuna riga, la sessione è stata terminata.  
  
    -   Se la sessione è ancora attiva, verificare l'eventuale presenza di processi assegnati alla sessione eseguendo la query `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`. Se viene visualizzato il processo, è molto probabile che sia in corso la terminazione della sessione. Si noti che l'operazione potrebbe richiedere una notevole quantità di tempo e non riuscire.  
  
    -   Se nella vista sys.dm_os_tasks non vi sono processi associati alla sessione, ma questa è ancora presente nella vista sys.dm_exec_sessions dopo l'esecuzione di un comando KILL, allora non è disponibile un thread di lavoro. Selezionare uno dei processi attualmente in esecuzione (un processo elencato nella vista sys.dm_os_tasks con un `sessions_id <> NULL`) e terminare la sessione ad esso associata per liberare il thread di lavoro. Si noti che la terminazione di una singola sessione potrebbe non essere sufficiente e che potrebbe essere necessario terminare più sessioni.  
  
## <a name="dac-port"></a>Porta della connessione DAC  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa della connessione DAC sulla porta TCP 1434 se disponibile o una porta TCP assegnata dinamicamente all'avvio di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Il log degli errori contiene il numero di porta su cui è in attesa la connessione DAC. Per impostazione predefinita, il listener della connessione DAC accetta connessioni solo sulla porta locale. Per un esempio di codice che attiva le connessioni amministrative remote, vedere [Opzione di configurazione del server remote admin connections](remote-admin-connections-server-configuration-option.md).  
  
 Dopo aver configurato la connessione amministrativa remota, il listener della connessione DAC viene abilitato senza richiedere un riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pertanto da tale istante un client può stabilire una connessione DAC in remoto. È possibile abilitare il listener della connessione DAC per accettare connessioni in remoto anche se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non risponde effettuando prima una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando la connessione DAC locale, quindi eseguendo la store procedure sp_configure per accettare la connessione da connessioni remote.  
  
 Nelle configurazioni cluster la connessione DAC è disattivata per impostazione predefinita. Gli utenti possono utilizzare l'opzione remote admin connection di sp_configure per abilitare il listener della connessione DAC per l'accesso a una connessione remota. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non risponde e il listener della connessione DAC non è abilitato, potrebbe essere necessario riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per poter stabilire la connessione DAC. È pertanto consigliabile abilitare l'opzione di configurazione remote admin connections in sistemi cluster.  
  
 La porta della connessione DAC viene assegnata dinamicamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante l'avvio. Durante la connessione all'istanza predefinita, l'applicazione livello dati evita di usare una richiesta SSRP (Resolution Protocol) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al servizio SQL Server Browser. Essa si connette prima sulla porta TCP 1434. Se questo tentativo di connessione termina con esito negativo, la connessione DAC esegue una chiamata SSRP per ottenere la porta. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser non è in attesa di richieste SSRP, la richiesta di connessione restituisce un errore. Vedere il log degli errori per ottenere il numero di porta su cui è in attesa la connessione DAC. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per accettare connessioni amministrative remote, è necessario inizializzare l'applicazione livello dati con un numero di porta esplicito:  
  
 **sqlcmd-Stcp:** _\<server>,\<port>_  
  
 Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elenca il numero di porta relativo all'applicazione livello dati, che per impostazione predefinita è 1434. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per accettare solo applicazioni livello dati locali, eseguire la connessione utilizzando l'adattatore loopback con il comando seguente:  
  
 **sqlcmd-S127.0.0.1**,`1434`  
  
## <a name="example"></a>Esempio  
 In questo esempio un amministratore si accorge che il server `URAN123` non risponde e desidera diagnosticare il problema. A tale scopo, l'utente attiva l'utilità della riga di comando `sqlcmd` e si connette al server `URAN123` utilizzando `-A` per indicare la connessione DAC.  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 L'amministratore può quindi eseguire query per diagnosticare il problema e, se necessario, terminare le sessioni che non rispondono.  
  
## <a name="related-tasks"></a>Attività correlate  
  
## <a name="related-content"></a>Contenuto correlato  
 [Utilizzo di sqlcmd con variabili di scripting](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)  
  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
 [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)  
  
 [sp_lock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)  
  
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-opentran-transact-sql)  
  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-inputbuffer-transact-sql)  
  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql)  
  
 [Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
