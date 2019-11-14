---
title: Riprodurre una traccia per gli aggiornamenti di SQL Server
description: Riprodurre una traccia con Database Experimentation Assistant per gli aggiornamenti SQL Server
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056702"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Riprodurre una traccia in Database Experimentation Assistant

In Database Experimentation Assistant (DEA) è possibile riprodurre un file di traccia acquisito su un ambiente di testing aggiornato. Si consideri, ad esempio, un carico di lavoro di produzione in esecuzione in SQL Server 2008 R2. Il file di traccia per il carico di lavoro deve essere riprodotto due volte: una volta in un ambiente con la stessa versione di SQL Server eseguita in produzione e di nuovo in un ambiente in cui è presente la versione di destinazione dell'aggiornamento SQL Server, ad esempio SQL Server 2016.

> [!NOTE]
> Per eseguire questa azione, è necessario configurare manualmente le macchine virtuali o i computer fisici per l'esecuzione di Riesecuzione distribuita tracce. Per ulteriori informazioni, vedere la pagina relativa alla [configurazione di riesecuzione distribuita controller e client](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Creazione di una riproduzione della traccia

In DEA selezionare l'icona di menu. Nel menu espanso selezionare riproduzione **tracce** accanto all'icona Riproduci.

![Selezionare Riproduci tracce nel menu](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Il computer del controller di Riesecuzione distribuita richiede le autorizzazioni per l'account utente usato per la modalità remota.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Concedere l'accesso al controller di Riesecuzione distribuita

1. Al prompt dei comandi, immettere **DCOMCNFG** per aprire l'interfaccia di **Servizi componenti** .
1. Espandere **Servizi componenti** > **computer** > **computer locale** > **configurazione DCOM** > **DReplayController**.
1. Fare clic con il pulsante destro del mouse su **DReplayController**e quindi scegliere **Proprietà**.
1. Nella scheda **sicurezza** selezionare **modifica** per aggiungere l'account utente.
1. Fare clic su **OK**.

### <a name="verify-setup"></a>Verificare il programma di installazione

1.  **SQL Server percorso di installazione**: immettere il percorso in cui è installato SQL Server. Ad esempio, C:\\Program Files (x86)\\Microsoft SQL Server\\120.
1.  **Nome computer controller**: immettere un nome per il computer configurato come controller. Questo computer esegue il servizio Windows denominato SQL Server controller Riesecuzione distribuita. Il controller di Riesecuzione distribuita orchestra le azioni dei client Riesecuzione distribuita. In ogni ambiente di Riesecuzione distribuita può essere presente una sola istanza del controller.
1.  **Nomi computer client**: immettere un nome per ogni computer client, separati da virgole. Esempio: CLIENT1, CLIENT2. È possibile avere fino a cinque controller client. I client sono uno o più computer fisici o virtuali che eseguono il servizio Windows denominato SQL Server client Riesecuzione distribuita. I client Riesecuzione distribuita vengono utilizzati insieme per simulare carichi di lavoro in un'istanza di SQL Server. In ogni ambiente di Riesecuzione distribuita possono essere presenti uno o più client.
1.  Fare clic su **Avanti**.

### <a name="select-a-trace"></a>Selezionare una traccia

1.  **Percorso del file di traccia**: immettere il percorso del file di traccia di input (con estensione TRC).
1.  **Percorso per l'archiviazione dell'output della pre-elaborazione della riproduzione**:  
    \- se non si ha già il file IRF, immettere il percorso in cui si vuole archiviare il file IRF e altri output di pre-elaborazione.  
    \- se si ha già il file IRF, immettere il percorso dei file IRF.
1. Fare clic su **Avanti**.

### <a name="replay-a-trace"></a>Riprodurre una traccia

1.  **Nome file di traccia**: immettere un nome per il file di traccia.
1.  **Dimensioni file massime (MB)** : immettere un valore per le dimensioni del rollover del file di traccia. Il valore predefinito è 200 MB. È possibile immettere un valore personalizzato.
1.  **Percorso per archiviare l'output di traccia della riproduzione**: immettere il percorso del file output. trc.
1.  **Nome istanza SQL Server**: immettere il nome dell'istanza di SQL Server su cui riprodurre le tracce.
1.  Selezionare **Start**.

Se le informazioni immesse sono valide, viene avviato il processo Riesecuzione distribuita. In caso contrario, il testo boses con informazioni non corrette viene evidenziato con il rosso. Verificare che i valori immessi siano corretti, quindi selezionare **Avvia**.

Attendere il completamento dell'esecuzione della riproduzione per visualizzare il percorso specificato. Selezionare l'icona a campana nella parte inferiore del menu a sinistra per monitorare lo stato di riproduzione.

![Stato tracce riproduzione](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Domande frequenti sulla riproduzione di tracce

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>Quali autorizzazioni di sicurezza sono necessarie per avviare un'acquisizione di riproduzione sul server di destinazione?

- L'utente di Windows che esegue l'operazione di traccia nell'applicazione DEA deve disporre dei diritti di amministratore di sistema nel computer di destinazione che esegue SQL Server. Questi diritti utente sono necessari per avviare una traccia.
- L'account di servizio in cui è in esecuzione SQL Server il computer di destinazione deve disporre dell'accesso in scrittura al percorso del file di traccia specificato.
- L'account di servizio in cui sono in esecuzione i servizi client di Riesecuzione distribuita deve disporre dei diritti utente per connettersi al computer di destinazione che esegue SQL Server e per eseguire le query.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>È possibile avviare più di una riproduzione nella stessa sessione?

Sì, è possibile avviare più Riproduci e tenerne traccia fino al completamento nella stessa sessione.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>È possibile avviare più di una riproduzione in parallelo?

Sì, ma non con lo stesso set di macchine virtuali selezionato nei **client controller Plus**. Il controller e i client saranno occupati. Configurare un set separato di computer in **controller Plus client** per avviare una riproduzione parallela.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>Quanto tempo è necessario in genere per completare una riproduzione?

Una riproduzione richiede in genere la stessa quantità di tempo della traccia di origine oltre alla quantità di tempo necessaria per la pre-elaborazione della traccia di origine. Tuttavia, se i computer client registrati con il controller non sono sufficienti per gestire il carico prodotto dalla riproduzione, il completamento della riproduzione potrebbe richiedere più tempo. È possibile registrare fino a 16 computer client con il controller.

### <a name="how-large-do-target-trace-files-get"></a>Quali sono le dimensioni dei file di traccia di destinazione?

È possibile che i file di traccia di destinazione siano compresi tra 5 e 15 volte le dimensioni della traccia di origine. Le dimensioni del file sono basate sul numero di query eseguite. Ad esempio, i BLOB del piano di query possono essere di grandi dimensioni. Se le statistiche per queste query cambiano spesso, vengono acquisiti più eventi.

### <a name="why-do-i-need-to-restore-databases"></a>Perché è necessario ripristinare I database?

SQL Server è un sistema di gestione di database relazionali con stato. Per eseguire correttamente un test A/B, è necessario mantenere sempre lo stato del database. In caso contrario, è possibile che vengano visualizzati errori nelle query durante la riproduzione che non verranno visualizzati nell'ambiente di produzione. Per evitare questi errori, è consigliabile eseguire un backup immediatamente prima dell'acquisizione dell'origine. Analogamente, è necessario ripristinare il backup nel computer di destinazione che esegue SQL Server per evitare errori durante la riproduzione.

### <a name="what-does-pass--on-the-replay-page-mean"></a>Cosa significa "Pass%" nella pagina di riproduzione?

Il **passaggio%** indica che è stata passata solo una percentuale di query. È possibile diagnosticare se il numero di errori è previsto. Gli errori potrebbero essere previsti oppure gli errori potrebbero verificarsi perché il database ha perso l'integrità. Se il valore di **pass%** non è quello previsto, è possibile arrestare la traccia ed esaminare il file di traccia in SQL Profiler per vedere quali query non sono state eseguite correttamente.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>Come è possibile esaminare gli eventi di traccia raccolti durante la riproduzione?

Aprire un file di traccia di destinazione e visualizzarlo in SQL Profiler. In alternativa, se si desidera apportare modifiche all'acquisizione di riproduzione, tutti gli script di SQL Server sono disponibili in C:\\Program Files (x86)\\Microsoft Corporation\\Database Experimentation Assistant\\scripts\\StartReplayCapture. SQL.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>Quali eventi di traccia vengono raccolti da DEA durante la riproduzione?

DEA acquisisce gli eventi di traccia che contengono informazioni relative alle prestazioni. La configurazione di acquisizione si trova nello script StartReplayCaptureTrace. SQL. Questi eventi sono tipici SQL Server eventi di traccia elencati nella documentazione di [riferimento di sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Risoluzione dei problemi di riproduzione della traccia

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>Non è possibile connettersi al computer in cui è in esecuzione SQL Server

- Verificare che il nome del computer in cui è in esecuzione SQL Server sia valido. Per confermare, provare a connettersi al server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocchi le connessioni al computer in cui è in esecuzione SQL Server.
- Verificare che l'utente disponga dei diritti utente necessari.
- Verificare che l'account del servizio Riesecuzione distribuita client disponga dell'accesso al computer in cui è in esecuzione SQL Server.

È possibile ottenere altri dettagli nei log in% Temp%\\DEA. Se il problema persiste, contattare il team del prodotto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Non è possibile connettersi al controller di Riesecuzione distribuita

- Verificare che il servizio Riesecuzione distribuita controller sia in esecuzione nel computer del controller. Per verificare, usare gli strumenti di gestione di Riesecuzione distribuita (eseguire il comando `dreplay.exe status -f 1`).
- Se la riproduzione viene avviata in modalità remota:
  - Verificare che il computer che esegue DEA possa eseguire correttamente il ping del controller. Verificare che le impostazioni del firewall consentano le connessioni in base alle istruzioni nella pagina **Configura ambiente di riproduzione** . Per ulteriori informazioni, vedere l'articolo [SQL Server riesecuzione distribuita](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Assicurarsi che l'avvio remoto e l'attivazione remota DCOM siano consentiti per l'utente del controller di Riesecuzione distribuita.
  - Verificare che i diritti utente di accesso remoto DCOM siano consentiti per l'utente di Riesecuzione distribuita controller.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>Il percorso del file di traccia esiste nel computer. Perché non è possibile trovare Riesecuzione distribuita controller?

Riesecuzione distribuita possibile accedere solo alle risorse del disco locale. È necessario copiare i file di traccia di origine nel computer del controller di Riesecuzione distribuita prima di avviare la riproduzione. Inoltre, è necessario specificare il percorso nella nuova pagina di **riproduzione** di dea. 

I percorsi UNC non sono compatibili con Riesecuzione distribuita. Riesecuzione distribuita percorsi devono essere percorsi locali assoluti del primo file di traccia di origine, inclusa l'estensione.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>Perché non è possibile cercare i file nella nuova pagina di riproduzione?

Poiché non è possibile esplorare le cartelle di un computer remoto, l'esplorazione dei file non è utile. Copiare e incollare i percorsi assoluti è più efficiente.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Ho iniziato a riprodurre con una traccia ma Riesecuzione distribuita non ha riprodotto alcun evento

Questo problema può verificarsi perché il file di traccia non ha eventi riproducibili o non contiene informazioni su come riprodurre gli eventi. Verificare se il percorso del file di traccia specificato è un file di traccia di origine. Il file di traccia di origine viene creato usando la configurazione fornita nello script StartCaptureTrace. SQL.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Viene visualizzato il messaggio "errore imprevisto". Quando si tenta di pre-elaborare i file di traccia utilizzando il controller Riesecuzione distribuita SQL Server 2017

Questo problema è noto nella versione RTM di SQL Server 2017. Per ulteriori informazioni, vedere [errore imprevisto quando si utilizza la funzionalità DReplay per riprodurre una traccia acquisita in SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
Il problema è stato risolto nell'aggiornamento cumulativo 1 più recente per SQL Server 2017. Scaricare la versione più recente dell' [aggiornamento cumulativo 1 per SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Passaggi successivi

- Per creare un report di analisi che consenta di ottenere informazioni dettagliate sulle modifiche proposte, vedere [creare report](database-experimentation-assistant-create-report.md).

- Per un'introduzione di 19 minuti a DEA e dimostrazione, Guarda il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
