---
title: Acquisire una traccia nel Database sperimentazione Assistant per gli aggiornamenti di SQL Server
description: Acquisire una traccia nel Database sperimentazione Assistant
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: dc53a9e1d151e07ce7e2eebf1444fd0d0065f8be
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794497"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Acquisire una traccia nel Database sperimentazione Assistant

È possibile utilizzare un'acquisizione di traccia nel Database sperimentazione Assistant DEA () per creare un file di traccia che include un log di eventi del server acquisiti. Un evento del server acquisiti è un evento che si verifica in un server specifico durante un periodo di tempo specifico. Un'acquisizione di traccia deve essere eseguita una sola volta per ogni server.

Prima di avviare un'acquisizione di traccia, assicurarsi di eseguire il backup tutti i database di destinazione.

La memorizzazione nella cache di query in SQL Server potrebbe influenzare i risultati della valutazione. È consigliabile riavviare il servizio SQL Server (MSSQLSERVER) nell'applicazione Servizi per migliorare la coerenza dei risultati della valutazione.

## <a name="create-a-trace-capture"></a>Creare un'acquisizione traccia

1. In DEA, selezionare l'icona di menu nel menu a sinistra. Nel menu espanso, selezionare **acquisire le tracce** accanto all'icona della fotocamera.

    ![Selezionare l'acquisizione di tracce nel menu](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. Sotto **New Capture**immettere o selezionare le informazioni seguenti:

    - **Nome dell'istanza SQL Server**: Immettere un nome per il computer che esegue SQL Server in cui si desidera acquisire una traccia del server.
    - **Nome del database**: Immettere un nome per un database in cui si desidera avviare una traccia di database. Se non si specifica un database, traccia viene acquisita in tutti i database nel server.
    - **Nome file di traccia**: Immettere un nome per il file di traccia per l'acquisizione.
    - **Dimensioni file massime (MB)** : Selezionare la dimensione di rollover dei file. Viene creato un nuovo file in base alle esigenze con le dimensioni di file che scelto. Le dimensioni consigliate di rollover sono 200 MB.
    - **Durata (in min)** : Selezionare il periodo di tempo (in minuti) che si desidera che l'acquisizione di traccia per l'esecuzione.
    - **Percorso in cui archiviare i file di output traccia**: Selezionare il percorso di destinazione per il file di traccia. 

    > [!NOTE]
    > Il percorso del file nel file di traccia deve essere nel computer che esegue SQL Server. Se il servizio SQL Server non è impostato per un account specifico, il servizio potrebbe essere necessarie autorizzazioni di scrittura nella cartella specificata per il file di traccia da scrivere.
    >
    >

    ![Nuova pagina di acquisizione](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Avviare l'acquisizione traccia

Dopo aver immesso o selezionato le informazioni necessarie, selezionare **avviare** avvio dell'acquisizione di tracce. Se le informazioni immesse sono valide, verrà avviato il processo di acquisizione di traccia. In caso contrario, le caselle di testo con le voci non valide sono evidenziate in rosso. 

Assicurarsi che i valori è stato selezionato o immesse siano corretti e quindi selezionare **avviare**.

Al termine dell'acquisizione della traccia in esecuzione, individuare il nuovo file di traccia nel percorso del file specificato nella **percorso per l'archiviazione file di output traccia**. Selezionare l'icona a forma di campana nella parte inferiore del menu a sinistra per monitorare lo stato di avanzamento dell'acquisizione.

![Acquisire lo stato di avanzamento di tracce](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>File di traccia

L'acquisizione di traccia scrive un file con estensione trc nel percorso specificato. Il file di traccia include i risultati della traccia dell'attività di un database di SQL Server. File TRC sono progettati per fornire ulteriori informazioni sugli errori che vengono rilevati e segnalati da SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Domande frequenti sull'acquisizione traccia

Seguenti sono alcune domande frequenti sull'acquisizione di traccia in DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>Gli eventi che vengono acquisiti quando si esegue un'acquisizione della traccia in un database di produzione?

Nella tabella seguente fornisce l'elenco di eventi e i dati della colonna corrispondente che vengono raccolti per le tracce:
  
|Nome evento|Dati di testo (1)|Dati binari (2)|ID del database (3)|Nome host (8)|Nome dell'applicazione (10)|Nome account di accesso (11)|SPID (12)|Ora di inizio (14)|Ora di fine (15)|Nome del database (35)|Sequenza di eventi (51 su)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC:Completed (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC:Starting (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL:BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL:BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Audit Login (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Audit Logout (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Prepare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec preparata SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>È disponibile un effetto sulle prestazioni nella mio server di produzione durante l'esecuzione di acquisizione traccia?
    
Sì, è disponibile un effetto minimo sulle prestazioni durante la raccolta delle tracce. Nei test, è stato rilevato un pressione della memoria di % 3.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>Quale tipo di autorizzazioni sono necessarie per l'acquisizione di tracce in un carico di lavoro di produzione?
    
- L'utente Windows che esegue l'operazione di traccia nell'applicazione DEA deve disporre dei diritti sysadmin nel computer che esegue SQL Server.
- L'account del servizio usato nel computer che esegue SQL Server deve avere accesso in scrittura al percorso del file di traccia specificata.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>È possibile acquisire le tracce per l'intero server o solo su un database singolo?
    
È possibile usare DEA per acquisire le tracce per tutti i database nel server o per un singolo database.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Ho un server collegato configurato nel mio ambiente di produzione. Queste query vengono visualizzati nelle tracce?
    
Se si esegue un'acquisizione di traccia per l'intero server, la traccia acquisisce tutte le query, incluse le query di server collegato. Per eseguire un'acquisizione di traccia per l'intero server, lasciare il **sicurissimo** nella casella **New Capture** vuoto.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>Che cos'è il tempo minimo consigliato per le tracce del carico di lavoro di produzione?
    
È consigliabile scegliere un periodo che meglio rappresenta l'intero del carico di lavoro. In questo modo, l'analisi viene eseguita in tutte le query nel carico di lavoro.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>Quanto è importante eseguire un backup di database corretto prima di iniziare un'acquisizione traccia?
    
Prima di avviare un'acquisizione di traccia, assicurarsi di eseguire il backup tutti i database di destinazione. Riproduzione della traccia acquisita nella destinazione 1 e 2 di destinazione. Se lo stato del database non è lo stesso, non sono sincronizzati i risultati della sperimentazione.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>È possibile raccogliere XEvents anziché le tracce ed è possibile riprodurre XEvents?
    
Sì. DEA supporta XEvents. Scaricare la versione più recente di DEA e fare una prova.

## <a name="troubleshoot-trace-captures"></a>Risolvere i problemi di acquisizioni di traccia

Se viene visualizzato un errore durante l'esecuzione di un'acquisizione di traccia, esaminare i prerequisiti seguenti:

- Verificare che il nome del computer che esegue SQL Server sia valido. Per confermare, provare a connettersi al computer che esegue SQL Server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocca le connessioni al computer che esegue SQL Server.
- Verificare che l'utente disponga delle autorizzazioni elencate nel post di blog [domande frequenti sulla riproduzione](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/).
- Verificare che il nome di traccia non segue la convenzione standard rollover (acquisire\_1). Provare invece i nomi di traccia, ad esempio acquisizione\_1A o Capture1.

Ecco alcune possibili errori che potrebbero verificarsi e soluzioni per risolverli:

|Possibili errori|Soluzione|  
|---|---|  
|Non è possibile avviare la traccia nella destinazione di SQL Server, verificare che si disponga delle autorizzazioni necessarie e che l'account di SQL Server disponga di accesso in scrittura al percorso del file di traccia specificato, il codice di errore Sql (53)|L'utente che esegue lo strumento DEA deve avere accesso al computer che esegue SQL Server. L'utente deve essere assegnato il ruolo sysadmin.|  
|Non è possibile avviare la traccia nella destinazione di SQL Server, verificare che si disponga delle autorizzazioni necessarie e che l'account di SQL Server disponga di accesso in scrittura al percorso del file di traccia specificato, il codice di errore Sql (19062)|Il percorso di traccia specificato potrebbe non esistere o la cartella non ha le autorizzazioni di scrittura per l'account in cui SQL Server sono in esecuzione servizi (ad esempio, servizio di rete). Il percorso deve esistere e deve avere le autorizzazioni necessarie per avviare la traccia.|  
|Una traccia DEA attualmente è in esecuzione nel server di destinazione.|La traccia attiva è già in esecuzione nel server di destinazione. Quando una traccia a livello di server è già in esecuzione non è possibile avviare una nuova traccia.|  
|Non è possibile aprire il database richiesto per l'acquisizione di traccia. Questo errore potrebbe essere causato da un nome di database non corretto.|Il database specificato non esiste o non è accessibile all'utente corrente. Usare il nome di database corretto.|  

Se vengono visualizzati altri errori etichettati *codice di errore Sql*, vedere [i messaggi di errore di sistema](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105)) per descrizioni dettagliate e le risoluzioni.
    
## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come configurare gli strumenti di Distributed Replay in SQL Server prima riprodurre una traccia acquisita, vedere [replay configura](database-experimentation-assistant-configure-replay.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
