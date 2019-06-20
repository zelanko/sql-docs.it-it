---
title: Introduzione a Database sperimentazione Assistant per gli aggiornamenti di SQL Server
description: Introduzione a Database sperimentazione Assistant
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
ms.openlocfilehash: 8f5cf6696b66504357279ab45432b4439894e4ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794471"
---
# <a name="get-started-with-database-experimentation-assistant"></a>Introduzione a Database sperimentazione Assistant

Database sperimentazione Assistant DEA () è un oggetto test a / B soluzione per le modifiche in ambienti di SQL Server, ad esempio gli aggiornamenti o nuovi indici. DEA consente di valutare come il carico di lavoro nel server di origine (nell'ambiente corrente) eseguirà nuovo nell'ambiente in uso. DEA in modo semplificato che esegue un test a / B completando tre passaggi: 

- Acquisizione
- riproduzione
- Analisi

Questo articolo illustra questi passaggi.

## <a name="capture"></a>Acquisizione

Il primo passaggio di SQL Server A / B test consiste nell'acquisire una traccia nel server di origine. Il server di origine è in genere il server di produzione. I file di traccia di acquisire il carico di lavoro dell'intera query su tale server, inclusi i timestamp. In un secondo momento, questa riproduzione della traccia viene eseguita nel server di destinazione per l'analisi. Il report di analisi fornisce informazioni dettagliate sulla differenza nelle prestazioni del carico di lavoro tra i server di due destinazione.

Considerazioni:

- Prima di iniziare l'acquisizione della traccia, assicurarsi di eseguire il backup dei database da cui si esegue l'acquisizione una traccia.
- Un utente DEA deve essere configurato per connettersi al database tramite l'autenticazione di Windows.
- Un account del servizio SQL Server richiede l'accesso al percorso del file di traccia di origine.

Per acquisire una traccia nel server di origine:

1. In DEA, passare a **acquisisce tutti** selezionando l'icona della fotocamera nel menu a sinistra.

   ![Menu di spostamento a sinistra](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Immettere o selezionare le informazioni seguenti:

   - **Nome traccia**: Il nome di file per il nuovo file di traccia che si sta creando. Evitare un nome di traccia che usa il rollover dei file convenzione di denominazione, ad esempio, CaptureName\_NNN.
   - **Durata**: La durata per l'acquisizione.
   - **Nome dell'istanza SQL Server**: Istanza di SQL Server da cui si desidera acquisire una traccia.
   - **Nome del database**: Il nome del database nel computer che esegue SQL Server che si desidera acquisire una traccia di. Se lasciato vuoto, traccia viene acquisita da tutti i database nel server.
   - **Percorso in cui archiviare i file di traccia di origine nel computer SQL Server**: Il percorso della cartella in cui si desidera salvare il file di traccia.

1. Assicurarsi che il database di destinazione viene eseguito il backup. Quindi, selezionare la casella di controllo del database.
1. Selezionare **avviare** per avviare l'acquisizione.

È possibile visualizzare lo stato di avanzamento dell'acquisizione, tra cui ora di inizio, la durata e tempo rimanente. È anche possibile avviare una nuova acquisizione mentre si attende la fine dell'acquisizione. Al termine dell'operazione di acquisizione, usare il file di output di traccia per avviare la seconda fase: riproduzione di file di traccia nel server di destinazione.

Per domande comuni sull'acquisizione di traccia, vedere la [acquisire domande frequenti su](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>riproduzione

Il secondo passaggio di SQL Server A / B testing è riprodurre il file di traccia acquisiti per i server di destinazione. Quindi, raccogliere le tracce complete dalle riproduzioni per l'analisi. 

Riprodurre il file di traccia nei due server di destinazione: uno che simula il server di origine (destinazione 1) e uno che simuli la modifica di proposta (destinazione 2). Le configurazioni di hardware di destinazione 1 e 2 di destinazione devono essere il più possibile simili in modo che SQL Server può analizzare in modo accurato l'effetto sulle prestazioni delle modifiche proposte.

Considerazioni:

- Per l'esecuzione di riesecuzione, è necessario configurare le macchine per eseguire le tracce di riesecuzione distribuita (DReplay). Per altre informazioni, vedere [installazione di Distributed Replay controller e client](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Assicurarsi di ripristinare i database nel server di destinazione usando il backup dal server di origine.
- La memorizzazione nella cache di query in SQL Server può influire sui risultati della valutazione. È consigliabile riavviare il servizio SQL Server (MSSQLSERVER) nell'applicazione Servizi per migliorare la coerenza nei risultati della valutazione.

Per riprodurre il file di traccia:

1. In DEA, selezionare l'icona di riproduzione nel menu a sinistra per passare al **tutte le riproduzioni**. Elenco delle riproduzioni precedenti eseguiti durante la sessione, se presente, viene visualizzato. Per avviare una riproduzione di nuovo, selezionare **Replay nuovo**.

1. Immettere o selezionare le informazioni seguenti:

   - **Nome di riproduzione**: Il nome di file per la traccia di riproduzione.
   - **Nome computer del controller**: Nome del computer del controller di riesecuzione distribuita.
   - **Percorso del file di traccia di origine nel controller**: Il percorso del file per il file di traccia di origine dal [acquisire](#capture).
   - **Nome dell'istanza SQL Server**: Il nome dell'istanza di SQL Server in cui si desidera riprodurre la traccia di origine.
   - **Percorso in cui archiviare i file di traccia di destinazione nel computer SQL Server**: Il percorso della cartella per il file di traccia di riproduzione risultante.

1. Selezionare la casella di controllo per ripristinare il backup dal primo passaggio.

1. Selezionare **avviare** per avviare la riproduzione. 

È possibile visualizzare lo stato della riproduzione. Dopo che riprodurre la traccia di origine su entrambi i server di destinazione, si è pronti per generare un report di analisi.

Per domande frequenti sulla riproduzione, vedere la [domande frequenti di riproduzione](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay).

## <a name="analysis"></a>Analisi

Il passaggio finale consiste per generare un report di analisi tramite le tracce di riproduzione. Il report di analisi può aiutarti a ottenere informazioni sulle implicazioni sulle prestazioni della modifica proposta.

Considerazioni:

- Se uno o più componenti risultano mancanti, viene visualizzata una pagina di prerequisiti con collegamenti per download quando si prova a generare un nuovo report di analisi (connessione a internet richiesta).
- Per visualizzare un report che è stato generato in una versione precedente dello strumento, è prima necessario aggiornare lo schema.

Per generare un report di analisi:

1. Nel menu a sinistra, passare a **report di analisi**. Connettersi al computer che esegue SQL Server in cui vengono archiviati i database di report. Viene visualizzato un elenco di tutti i report nel server. Per creare un nuovo report, selezionare **nuovo Report**.

1. Immettere o selezionare le informazioni necessarie per generare un report:

   - **Nome del report**: Il nome del report di analisi per creare.
   - **Traccia per SQL Server di destinazione 1**: Il percorso del file di traccia da riprodurre nella destinazione 1.
   - **Traccia per SQL Server di destinazione 2**: Il percorso per il file di traccia da riprodurre in 2 di destinazione.

1. Selezionare **avviare** per generare il report. Il nuovo report viene visualizzato nella parte superiore dell'elenco. L'icona accanto al report diventa un segno di spunta verde quando è stato generato il report.

A questo punto, visualizzare il report di analisi per ottenere informazioni dettagliate fornite per l'oggetto test a / B.

Per domande frequenti sui report di analisi, vedere la [domande frequenti su analisi](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Report di analisi

Nella prima pagina del report, vengono visualizzate informazioni sulla versione e compilazione per i server di destinazione in cui è stato eseguito l'esperimento. È possibile usare una soglia per regolare la sensibilità o la tolleranza dell'oggetto / analisi del Test di B. Per impostazione predefinita, la soglia è impostata nel percorso % 5. Qualsiasi miglioramento delle prestazioni che sono maggiore o uguale a % 5 è stato categorizzato come **migliorato**. Selezionare le opzioni nel menu a discesa per valutare il report utilizzando le soglie di prestazioni diverso.

![Soglia](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Due grafici a torta vengono illustrate le implicazioni sulle prestazioni della differenza tra il server di due destinazione per il carico di lavoro. Il grafico a sinistra si basa sul conteggio delle esecuzioni. Il grafico a destra si basa su query distinte. Esistono cinque categorie possibili:

- **Migliorato**:  Statisticamente, la query è stata eseguita meglio in 2 destinazione rispetto a destinazione 1.
- **Danneggiato**: Statisticamente, la query è stata eseguita peggio in 2 destinazione rispetto a destinazione 1.
- **Stesso**: Non c'è alcuna differenza statistica per la query tra destinazione 1 e 2 di destinazione.
- **Non è possibile valutare**: Le dimensioni del campione per la query sono troppo piccola per l'analisi statistica. Per un test analysis B, DEA richiede le stesse query disponga di almeno 30 esecuzioni per ogni destinazione.
- **Errore**: La query che hanno generato errore almeno una volta in una delle destinazioni.

![Grafico a torta](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Selezionare una sezione per eseguire il drill-in una determinata categoria e ottenere le metriche delle prestazioni, tra cui il **non è possibile valutare** fetta di torta.

La pagina di drill-down per ottenere prestazioni una modifica categoria mostra un elenco delle query in tale categoria. Il **errore** pagina contiene tre schede:

- **Nuovi errori**: Errori che venivano visualizzate in 2 di destinazione ma non nella destinazione 1.
- **Gli errori esistenti**: Errori che venivano visualizzate in sia destinazione 1 e 2 di destinazione.
- **Gli errori risolti**: Errori che venivano visualizzate su destinazione 1 ma non su 2 di destinazione.

   ![Pagina di errore](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Selezionare una query da passare a un **Comparison Summary** pagina per tale query.

Il **confronto riepilogo** pagina Mostra le statistiche di riepilogo della query. Il riepilogo include il numero di esecuzioni, la durata media, valore medio della CPU, medio di letture/scritture e numero di errori.

![Statistiche di riepilogo](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Se la query è un errore, il **informazioni sull'errore** scheda Mostra altre informazioni sull'errore. Il **le informazioni sulla pianificazione di Query** scheda Visualizza informazioni sui piani di query che vengono utilizzati per la query nella destinazione 1 e 2 di destinazione.

![Piano di query](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

In qualsiasi pagina del report di analisi, selezionare il **stampare** pulsante nella parte superiore destra per stampare tutti gli elementi che è visibile.

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come generare un file di traccia che include un log di eventi che si verificano in un server, vedere [acquisire traccia](database-experimentation-assistant-capture-trace.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
