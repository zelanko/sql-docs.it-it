---
title: Acquisire una traccia per gli aggiornamenti di SQL Server
description: Acquisire una traccia in Database Experimentation Assistant per gli aggiornamenti SQL Server
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 6c24632875d09125efcd043ae907e87a21847fe9
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056597"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Acquisire una traccia in Database Experimentation Assistant

È possibile utilizzare un'acquisizione di traccia in Database Experimentation Assistant (DEA) per creare un file di traccia con un log di eventi del server acquisiti. Un evento del server acquisito è un evento che si verifica in un server specifico durante un periodo di tempo specifico. Un'acquisizione di traccia deve essere eseguita una volta per ogni server.

Prima di avviare un'acquisizione di traccia, assicurarsi di eseguire il backup di tutti i database di destinazione.

La memorizzazione nella cache delle query in SQL Server potrebbe influire sui risultati della valutazione. È consigliabile riavviare il servizio SQL Server (MSSQLSERVER) nell'applicazione Servizi per migliorare la coerenza dei risultati della valutazione.

## <a name="create-a-trace-capture"></a>Creare un'acquisizione di traccia

1. In DEA selezionare l'icona di menu nel menu a sinistra. Nel menu espanso selezionare **Acquisisci tracce** accanto all'icona della fotocamera.

    ![Selezionare Acquisisci tracce nel menu](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. In **nuova acquisizione**immettere o selezionare le informazioni seguenti:

    - **Nome istanza SQL Server**: immettere un nome per il computer che esegue SQL Server in cui si desidera acquisire una traccia del server.
    - **Nome database**: immettere un nome per un database in cui avviare una traccia del database. Se non si specifica un database, la traccia viene acquisita in tutti i database del server.
    - **Nome file di traccia**: immettere un nome per il file di traccia per l'acquisizione.
    - **Dimensioni file massime (MB)** : selezionare le dimensioni del rollover per i file. Quando necessario, viene creato un nuovo file in base alle dimensioni del file selezionato. Le dimensioni consigliate per il rollover sono 200 MB.
    - **Durata (in min)** : selezionare l'intervallo di tempo (in minuti) in cui si desidera che l'acquisizione di traccia venga eseguita.
    - **Percorso per archiviare il file di traccia di output**: selezionare il percorso di destinazione per il file di traccia. 

    > [!NOTE]
    > Il percorso del file di traccia deve trovarsi nel computer in cui è in esecuzione SQL Server. Se il servizio SQL Server non è impostato per un account specifico, potrebbe essere necessario che il servizio disponga delle autorizzazioni di scrittura per la cartella specificata per il file di traccia da scrivere.
    >
    >

    ![Pagina nuova acquisizione](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Avviare l'acquisizione della traccia

Dopo aver immesso o selezionato le informazioni necessarie, selezionare **Avvia** per avviare l'acquisizione delle tracce. Se le informazioni immesse sono valide, viene avviato il processo di acquisizione della traccia. In caso contrario, le caselle di testo con voci non valide vengono evidenziate con il rosso. 

Verificare che i valori selezionati o immessi siano corretti, quindi selezionare **Avvia**.

Al termine dell'esecuzione dell'acquisizione della traccia, trovare il nuovo file di traccia nel percorso del file specificato in **percorso per archiviare il file di traccia di output**. Selezionare l'icona a campana nella parte inferiore del menu a sinistra per monitorare lo stato di avanzamento dell'acquisizione.

![Stato di acquisizione tracce](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>File di traccia

L'acquisizione della traccia scrive un file con estensione TRC nel percorso specificato. Il file di traccia include i risultati della traccia dell'attività di un database di SQL Server. I file TRC sono progettati per fornire ulteriori informazioni sugli errori rilevati e segnalati da SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Domande frequenti sull'acquisizione di tracce

Di seguito sono riportate alcune domande frequenti sull'acquisizione di tracce in DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>Quali eventi vengono acquisiti quando si esegue un'acquisizione di traccia in un database di produzione?

La tabella seguente include l'elenco di eventi e i dati di colonna corrispondenti raccolti per le tracce:
  
|Nome evento|Dati di testo (1)|Dati binari (2)|ID database (3)|Nome host (8)|Nome applicazione (10)|Nome account di accesso (11)|SPID (12)|Ora di inizio (14)|Ora di fine (15)|Nome database (35)|Sequenza di eventi (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: completato (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: avvio (11)**||*|*|*|*|*|*|*||*|*|*|  
|**Parametro di output RPC (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL:BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Controlla account di accesso (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Controllo disconnessione (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Preparare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**SQL preparato per exec (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>Si è verificato un effetto sulle prestazioni del server di produzione quando l'acquisizione della traccia è in esecuzione?
    
Sì, si verifica un effetto minimo sulle prestazioni durante la raccolta delle tracce. Nei test è stato rilevato un numero eccessivo di richieste di memoria al 3%.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>Quali tipi di autorizzazioni sono necessari per l'acquisizione di tracce su un carico di lavoro di produzione?
    
- L'utente di Windows che esegue l'operazione di traccia nell'applicazione DEA deve disporre dei diritti di amministratore di sistema nel computer in cui è in esecuzione SQL Server.
- L'account di servizio utilizzato nel computer che esegue SQL Server deve disporre dell'accesso in scrittura al percorso del file di traccia specificato.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>È possibile acquisire le tracce per l'intero server o solo per un singolo database?
    
È possibile utilizzare DEA per acquisire tracce per tutti i database nel server o per un singolo database.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Un server collegato è configurato nell'ambiente di produzione. Queste query vengono visualizzate nelle tracce?
    
Se si sta eseguendo un'acquisizione di traccia per l'intero server, la traccia acquisisce tutte le query, incluse le query del server collegato. Per eseguire un'acquisizione di traccia per l'intero server, lasciare vuota la casella **nome database** in **nuova acquisizione** .
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>Qual è il tempo minimo consigliato per le tracce del carico di lavoro di produzione?
    
Si consiglia di scegliere un'ora che meglio rappresenti l'intero carico di lavoro. In questo modo, l'analisi viene eseguita su tutte le query del carico di lavoro.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>Quanto è importante eseguire un backup del database prima di avviare un'acquisizione di traccia?
    
Prima di avviare un'acquisizione di traccia, assicurarsi di eseguire il backup di tutti i database di destinazione. La traccia acquisita in target 1 e target 2 viene rieseguita. Se lo stato del database non è lo stesso, i risultati della sperimentazione sono sbilanciati.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>È possibile raccogliere XEvent anziché tracce ed è possibile riprodurre XEvent?
    
Sì. DEA supporta XEvent. Scaricare la versione più recente di DEA e assegnarle un tentativo.

## <a name="troubleshoot-trace-captures"></a>Risolvere i problemi relativi alle acquisizioni di traccia

Se viene visualizzato un errore durante l'esecuzione di un'acquisizione di traccia, esaminare i prerequisiti seguenti:

- Verificare che il nome del computer in cui è in esecuzione SQL Server sia valido. Per confermare, provare a connettersi al computer che esegue SQL Server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocchi le connessioni al computer in cui è in esecuzione SQL Server.
- Verificare che l'utente disponga delle autorizzazioni elencate nel post di Blog relativo alla [riproduzione delle domande frequenti](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/).
- Verificare che il nome della traccia non segua la convenzione di rollover standard (acquisizione\_1). In alternativa, provare i nomi di traccia come Capture\_1A o Capture1.

Di seguito sono riportati alcuni possibili errori che possono essere visualizzati e le soluzioni per risolverli:

|Possibili errori|Soluzione|  
|---|---|  
|Impossibile avviare la traccia sul SQL Server di destinazione. verificare se si dispone delle autorizzazioni necessarie e che l'account di SQL Server disponga dell'accesso in scrittura al percorso del file di traccia specificato codice errore SQL (53)|L'utente che esegue lo strumento DEA deve disporre dell'accesso al computer in cui è in esecuzione SQL Server. All'utente deve essere assegnato il ruolo sysadmin.|  
|Impossibile avviare la traccia sul SQL Server di destinazione. verificare se si dispone delle autorizzazioni necessarie e che l'account di SQL Server disponga dell'accesso in scrittura al percorso del file di traccia specificato codice errore SQL (19062)|Il percorso di traccia specificato potrebbe non esistere o la cartella non dispone delle autorizzazioni di scrittura per l'account con cui vengono eseguiti SQL Server servizi, ad esempio servizio di rete. Il percorso deve esistere e deve disporre delle autorizzazioni necessarie per l'avvio della traccia.|  
|Una traccia DEA è attualmente in esecuzione nel server di destinazione.|Una traccia attiva è già in esecuzione nel server di destinazione. Non è possibile avviare una nuova traccia quando è già in esecuzione una traccia a livello di server.|  
|Impossibile aprire il database richiesto per l'acquisizione della traccia. Questo errore potrebbe essere causato da un nome di database errato.|Il database specificato non esiste o non è accessibile all'utente corrente. Usare il nome del database corretto.|  

Se vengono visualizzati altri errori con l'etichetta *codice errore SQL*, vedere [motore di database errori](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors) per descrizioni dettagliate.

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come configurare gli strumenti di Riesecuzione distribuita in SQL Server prima di riprodurre una traccia acquisita, vedere [configurare la riproduzione](database-experimentation-assistant-configure-replay.md).

- Per un'introduzione di 19 minuti a DEA e dimostrazione, Guarda il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
