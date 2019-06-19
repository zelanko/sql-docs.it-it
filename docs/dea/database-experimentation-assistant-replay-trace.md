---
title: Riprodurre una traccia con Assistente di sperimentazione di Database per gli aggiornamenti di SQL Server
description: Riprodurre una traccia con Assistente di sperimentazione di Database
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
ms.openlocfilehash: 7db0e6a83997a3be7b204f780f3c0a7ad856b0d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794447"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Riprodurre una traccia nel Database sperimentazione Assistant

Nel Database sperimentazione Assistant DEA (), è possibile riprodurre un file di traccia acquisita su un ambiente di testing aggiornato. Ad esempio, si consideri un carico di lavoro di produzione eseguito in SQL Server 2008 R2. Il file di traccia per il carico di lavoro deve essere rieseguito due volte: una volta in un ambiente con la stessa versione di SQL Server che viene eseguito in ambiente di produzione e nuovamente in un ambiente con la versione di SQL Server di destinazione di aggiornamento, ad esempio SQL Server 2016.

> [!NOTE]
> Per eseguire questa azione, è necessario impostare manualmente backup di macchine virtuali o computer fisico per eseguire le tracce di riesecuzione distribuita. Per altre informazioni, vedere [installazione di Distributed Replay controller e client](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Creare una riproduzione della traccia

In DEA, selezionare l'icona di menu. Nel menu espanso, selezionare **riprodurre le tracce** accanto all'icona di riproduzione.

![Selezionare riprodurre le tracce nel menu](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Computer del controller di riesecuzione distribuita richiede le autorizzazioni per l'account utente usato in remoto.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Concedere l'accesso al controller di riesecuzione distribuita

1. Un prompt dei comandi, immettere **dcomcnfg** per aprire il **Servizi componenti** interfaccia.
1. Espandere **Servizi componenti** > **computer** > **Computer** > **DCOM Config**  >  **DReplayController**.
1. Fare doppio clic su **DReplayController**, quindi selezionare **proprietà**.
1. Nel **sicurezza** scheda, seleziona **modificare** per aggiungere l'account utente.
1. Scegliere **OK**.

### <a name="verify-setup"></a>Verificare il programma di installazione

1.  **Percorso di installazione di SQL Server**: Immettere il percorso in cui è installato SQL Server. Ad esempio, c\\Program Files (x86)\\Microsoft SQL Server\\120.
1.  **Nome computer del controller**: Immettere un nome per il computer che è stato impostato come il controller. Questo computer è in esecuzione il servizio Windows denominato SQL Server Distributed Replay controller. Distributed Replay controller orchestrare le azioni dei client riesecuzione distribuita. In ogni ambiente di Riesecuzione distribuita può essere presente una sola istanza del controller.
1.  **I nomi dei computer client**: Immettere un nome per ogni computer client, separati da virgole. Esempio: client1 client2. È possibile avere fino a cinque controller client. I client sono uno o più computer, fisico o virtuale, che eseguono il servizio Windows denominato SQL Server Distributed Replay client. I client Riesecuzione distribuita vengono utilizzati insieme per simulare carichi di lavoro in un'istanza di SQL Server. In ogni ambiente di Riesecuzione distribuita possono essere presenti uno o più client.
1.  Selezionare **Avanti**.

### <a name="select-a-trace"></a>Selezionare una traccia

1.  **Percorso del file di traccia**: Immettere il percorso del file di traccia (trc) di input.
1.  **Percorso per l'archiviazione di riproduzione pre-elaborazione output**:  
    \- Se si ha già il file IRF, immettere il percorso della posizione in cui si desidera archiviare il file IRF e gli output di altri pre-elaborazione.  
    \- Se hai già il file IRF, immettere il percorso ai file IRF.
1. Selezionare **Avanti**.

### <a name="replay-a-trace"></a>Riprodurre una traccia

1.  **Nome file di traccia**: Immettere un nome di file di traccia.
1.  **Dimensioni file massime (MB)** : Immettere un valore di dimensione rollover dei file di traccia. Il valore predefinito è 200 MB. È possibile immettere un valore personalizzato.
1.  **Percorso per archiviare l'output di traccia di riproduzione**: Immettere il percorso del file di output con estensione trc.
1.  **Nome dell'istanza SQL Server**:  Immettere il nome dell'istanza di SQL Server in cui si desidera riprodurre le tracce.
1.  Selezionare **Start**.

Se le informazioni immesse sono valide, verrà avviato il processo di riesecuzione distribuita. In caso contrario, il boses testo contenenti informazioni non corrette sono evidenziate in rosso. Assicurarsi che i valori immessi siano corretti e quindi selezionare **avviare**.

Attendere finché non viene completata la riproduzione in esecuzione per visualizzare il percorso specificato. Selezionare l'icona a forma di campana nella parte inferiore del menu a sinistra per monitorare lo stato di avanzamento di riproduzione.

![Stato di avanzamento di riproduzione delle tracce](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Domande frequenti sulla riproduzione di tracce

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>Le autorizzazioni di sicurezza necessario avviare un'acquisizione di riproduzione sul server di destinazione?

- L'utente di Windows che esegue l'operazione di traccia nell'applicazione DEA deve disporre dei diritti sysadmin nel computer di destinazione che esegue SQL Server. Questi diritti utente sono necessari per avviare una traccia.
- L'account del servizio con cui viene eseguito il computer di destinazione che esegue SQL Server deve avere accesso in scrittura al percorso del file di traccia specificata.
- L'account del servizio in cui vengono eseguiti i servizi Distributed Replay Client deve avere diritti utente per connettersi al computer di destinazione che esegue SQL Server e per eseguire query.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>È possibile iniziare a più di una riesecuzione nella stessa sessione?

Sì, è possibile avviare più operazioni di riproduzione e tenerne traccia fino al completamento nella stessa sessione.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>Si può iniziare a più di una riesecuzione in parallelo?

Sì, ma non con lo stesso set di macchine virtuali selezionate nella **Controller e client**. Il controller e client sarà occupati. Configurare un set separato di computer sottoposti **Controller e Client** per avviare una riproduzione parallela.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>Quanto tempo una riproduzione in genere necessario alla fine?

Una riproduzione richiede in genere la stessa quantità di tempo utilizzato per la traccia di origine più il periodo di tempo impiegato per pre-elaborare la traccia di origine. Tuttavia, se i computer client che sono registrati con il controller non è sufficienti per gestire il carico prodotto dalla riproduzione, la riproduzione potrebbe richiedere più tempo. È possibile registrare fino a 16 macchine client con il controller.

### <a name="how-large-do-target-trace-files-get"></a>Le dimensioni sono il file di traccia di destinazione ottenere?

La traccia di destinazione i file potrebbero essere compreso tra 5 e 15 volte la dimensione della traccia di origine. Le dimensioni del file sono basata sul numero di query viene eseguito. Ad esempio, i BLOB di piano di query possono essere notevoli. Se le statistiche per le query cambiano spesso, vengono acquisiti altri eventi.

### <a name="why-do-i-need-to-restore-databases"></a>Il motivo per cui è necessario ripristinare i database?

SQL Server è un sistema di gestione di database relazionale con stato. Per eseguire correttamente una A / B, test, lo stato del database devono essere mantenute in qualsiasi momento. In caso contrario, è possibile visualizzare errori nelle query durante la riproduzione che non sarà più visualizzato nell'ambiente di produzione. Per evitare questi errori, è consigliabile eseguire un backup prima dell'acquisizione di origine. Analogamente, il ripristino del backup del computer di destinazione che esegue SQL Server è necessario per evitare errori durante la riproduzione.

### <a name="what-does-pass--on-the-replay-page-mean"></a>Che cosa "passare %" al valore medio pagina di riproduzione?

**Passare a %** indica che passata solo una percentuale di query. È possibile diagnosticare se il numero di errori è previsto. Si potrebbero aspettare gli errori o gli errori potrebbero verificarsi perché il database ha perso la loro integrità. Se il valore per **pass %** non è quello previsto, è possibile arrestare la traccia ed esaminare il file di traccia in SQL Profiler per visualizzare le query che non sono riuscito.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>Come è possibile esaminare gli eventi di traccia raccolti durante la riproduzione?

Aprire un file di traccia di destinazione e visualizzarlo in SQL Profiler. Oppure, se si desidera apportare modifiche per l'acquisizione di riproduzione, tutti gli script di SQL Server sono disponibili in c:\\Program Files (x86)\\Microsoft Corporation\\Database sperimentazione Assistant\\script\\ StartReplayCapture.sql.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>Quali eventi di traccia viene raccolti durante la riproduzione DEA?

DEA acquisisce gli eventi di traccia che contengono informazioni relative alle prestazioni. La configurazione di acquisizione è nello script StartReplayCaptureTrace.sql. Questi eventi sono eventi di traccia di SQL Server tipici elencati nel [documentazione di riferimento sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Risolvere i problemi di riproduzione della traccia

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>Non è possibile connettersi al computer che esegue SQL Server

- Verificare che il nome del computer che esegue SQL Server sia valido. Per confermare, provare a connettersi al server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocca le connessioni al computer che esegue SQL Server.
- Verificare che l'utente disponga dei diritti utente necessari.
- Verificare che l'account del servizio Distributed Replay client abbia accesso al computer che esegue SQL Server.

È possibile ottenere altri dettagli nei log in % temp %\\DEA. Se il problema persiste, contattare il team del prodotto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Non è possibile connettersi al controller di riesecuzione distribuita

- Verificare che il servizio Distributed Replay controller sia in esecuzione nel computer del controller. Per verificare, usare gli strumenti di gestione di riesecuzione distribuita (eseguire il comando `dreplay.exe status -f 1`).
- Se la riproduzione è stata avviata in modalità remota:
  - Verificare che il computer che esegue DEA possibile effettuare correttamente il ping del controller. Verificare che le impostazioni del firewall consentano le connessioni per le istruzioni nel **ambiente di riesecuzione configurare** pagina. Per altre informazioni, vedere l'articolo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Assicurarsi che DCOM di avvio remoto e attivazione remota sono consentite per l'utente del controller di riesecuzione distribuita.
  - Assicurarsi che i diritti utente di accesso remoto DCOM consentiti per l'utente del controller di riesecuzione distribuita.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>Il percorso del file di traccia esiste nel computer. Il motivo per cui non è controller di riesecuzione distribuita trovarlo?

Distributed Replay sono accessibili solo risorse del disco locale. Prima di iniziare la riproduzione, è necessario copiare i file di traccia di origine al computer del controller di riesecuzione distribuita. Inoltre, è necessario fornire il percorso nel DEA **Replay nuovo** pagina. 

I percorsi UNC non sono compatibili con Distributed Replay. I percorsi di riesecuzione distribuiti devono essere percorsi assoluti locali per il primo file di traccia di origine, tra cui estensione.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>Il motivo per cui non è possibile cercare i file nella pagina di riproduzione nuovo?

Perché è non è possibile esplorare le cartelle del computer remoto, di esplorazione per file non è utile. Copiare e incollare i percorsi assoluti è più efficiente.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Ho iniziato riproduzione con una traccia, ma Distributed Replay non tutti gli eventi vengono riprodotti

Questo problema può verificarsi perché il file di traccia non ha eventi riproducibili oppure non dispone di informazioni su come riprodurre gli eventi. Verificare se il percorso del file di traccia fornito è un file di traccia di origine. Il file di traccia di origine viene creato usando la configurazione fornita nello script StartCaptureTrace.sql.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Viene visualizzato "si è verificato un errore imprevisto." Quando si tenta di pre-elaborare i file di traccia, usando il controller di riesecuzione distribuita di SQL Server 2017

Questo problema è noto nella versione RTM di SQL Server 2017. Per altre informazioni, vedere [errore imprevisto quando si usa la funzionalità DReplay per riprodurre una traccia acquisita in SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
Il problema è stato risolto nell'aggiornamento 1 aggiornamento cumulativo più recente per SQL Server 2017. Scaricare la versione più recente di [aggiornamento cumulativo 1 per SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Passaggi successivi

- Per creare un report di analisi che consente di ottenere informazioni dettagliate sulle modifiche proposte, vedere [consentono di creare report](database-experimentation-assistant-create-report.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
