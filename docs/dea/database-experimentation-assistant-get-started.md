---
title: Introduzione a Database Experimentation Assistant per gli aggiornamenti SQL Server
description: Inizia a usare Database Experimentation Assistant
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
ms.openlocfilehash: 9fe162b2a9bc0db4a2a49648eecb76c5802f57c0
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381765"
---
# <a name="get-started-with-database-experimentation-assistant"></a>Inizia a usare Database Experimentation Assistant

Database Experimentation Assistant (DEA) è una soluzione di test A/B per le modifiche in ambienti SQL Server, ad esempio aggiornamenti o nuovi indici. DEA consente di valutare il modo in cui il carico di lavoro nel server di origine (nell'ambiente corrente) sarà eseguito nel nuovo ambiente. DEA guida l'utente durante l'esecuzione di un test A/B completando tre passaggi: 

- Acquisizione
- Riproduzione
- Analisi

Questo articolo illustra questa procedura.

## <a name="capture"></a>Acquisizione

Il primo passaggio di SQL Server test A/B consiste nell'acquisire una traccia nel server di origine. Il server di origine è in genere il server di produzione. I file di traccia acquisiscono l'intero carico di lavoro di query su tale server, inclusi i timestamp. In seguito, questa traccia viene rieseguita nei server di destinazione per l'analisi. Il report di analisi fornisce informazioni sulle differenze di prestazioni del carico di lavoro tra i due server di destinazione.

Considerazioni:

- Prima di avviare l'acquisizione della traccia, assicurarsi di eseguire il backup dei database da cui si sta acquisendo una traccia.
- È necessario configurare un utente di DEA per la connessione al database tramite l'autenticazione di Windows.
- Un account del servizio SQL Server richiede l'accesso al percorso del file di traccia di origine.
- Per determinare se le prestazioni di una query sono state migliorate o diminuite, la query deve essere eseguita almeno 15 volte durante il periodo di acquisizione.  

Per acquisire una traccia nel server di origine:

1. In DEA passare a **tutte le acquisizioni** selezionando l'icona della fotocamera nel menu a sinistra.

   ![Menu di spostamento a sinistra](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. Immettere o selezionare le seguenti informazioni:

   - **Nome traccia**: il nome del nuovo file di traccia che si sta creando. Evitare il nome di una traccia che usa la convenzione di denominazione dei file di rollover, ad esempio Capturename \_NNN.
   - **Duration**: durata dell'acquisizione.
   - **Nome istanza SQL Server**: istanza SQL Server da cui si desidera acquisire una traccia.
   - **Nome database**: nome del database nel computer che esegue SQL Server di cui si desidera acquisire una traccia. Se viene lasciato vuoto, la traccia viene acquisita da tutti i database nel server.
   - **Percorso per archiviare il file di traccia di origine nel computer SQL Server**: il percorso della cartella in cui si desidera salvare il file di traccia.

1. Verificare che sia stato eseguito il backup del database di destinazione. Selezionare quindi la casella di controllo database.
1. Selezionare **Start (avvia** ) per avviare l'acquisizione.

È possibile visualizzare lo stato di avanzamento dell'acquisizione, tra cui l'ora di inizio, la durata e il tempo rimanente. È anche possibile avviare una nuova acquisizione durante l'attesa del completamento dell'acquisizione. Al termine dell'acquisizione, utilizzare il file di traccia di output per avviare la seconda fase: riprodurre il file di traccia nei server di destinazione.

Per domande frequenti sull'acquisizione di tracce, vedere le domande [frequenti sull'acquisizione](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture).

## <a name="replay"></a>Riproduzione

Il secondo passaggio di SQL Server test A/B consiste nel riprodurre il file di traccia acquisito nei server di destinazione. Raccogliere quindi tracce estese dalle repliche per l'analisi. 

Il file di traccia viene riprodotto in due server di destinazione: uno che simula il server di origine (destinazione 1) e uno che simula la modifica proposta (destinazione 2). Le configurazioni hardware di target 1 e target 2 devono essere il più simile possibile, in modo SQL Server possibile analizzare accuratamente l'effetto sulle prestazioni delle modifiche proposte.

Considerazioni:

- Per eseguire la riproduzione, i computer devono essere configurati per l'esecuzione di Riesecuzione distribuita (DReplay) tracce. Per ulteriori informazioni, vedere [riesecuzione distribuita controller e configurazione client](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
- Assicurarsi di ripristinare i database nei server di destinazione usando il backup del server di origine.
- La memorizzazione nella cache delle query in SQL Server può influire sui risultati della valutazione. Si consiglia di riavviare il servizio SQL Server (MSSQLSERVER) nell'applicazione dei servizi per migliorare la coerenza dei risultati della valutazione.

Per riprodurre il file di traccia:

1. In DEA selezionare l'icona Riproduci nel menu a sinistra per passare a **tutti i Riproduci**. Viene visualizzato l'elenco delle esecuzioni precedenti che vengono eseguite durante la sessione. Per avviare una nuova riproduzione, selezionare **nuova**riproduzione.

1. Immettere o selezionare le seguenti informazioni:

   - **Nome riproduzione**: il nome del file per la traccia di riproduzione.
   - **Nome computer controller**: il nome del computer del controller di riesecuzione distribuita.
   - **Percorso del file di traccia di origine nel controller**: percorso del file di traccia di origine dall' [acquisizione](#capture).
   - **SQL Server nome istanza**: il nome dell'istanza di SQL Server in cui riprodurre la traccia di origine.
   - **Percorso per archiviare il file di traccia di destinazione nel computer SQL Server**: il percorso della cartella per il file di traccia della riproduzione risultante.

1. Selezionare la casella di controllo per ripristinare il backup dal primo passaggio.

1. Selezionare **Avvia** per avviare la riproduzione. 

È possibile visualizzare lo stato della riproduzione. Dopo aver riprodotto la traccia di origine in entrambi i server di destinazione, si è pronti per generare un report di analisi.

Per domande frequenti sulla riproduzione, vedere le domande [frequenti sulla riproduzione](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay).

## <a name="analysis"></a>Analisi

Il passaggio finale consiste nel generare un report di analisi utilizzando le tracce di riproduzione. Il report di analisi può essere utile per ottenere informazioni sulle implicazioni relative alle prestazioni della modifica proposta.

Considerazioni:

- Se uno o più componenti risultano mancanti, viene visualizzata una pagina dei prerequisiti con collegamenti per i download quando si tenta di generare un nuovo report di analisi (connessione Internet necessaria).
- Per visualizzare un report generato in una versione precedente dello strumento, è necessario prima aggiornare lo schema.

Per generare un report di analisi:

1. Nel menu a sinistra passare a **report di analisi**. Connettersi al computer che esegue SQL Server in cui archiviare i database dei report. Viene visualizzato un elenco di tutti i report nel server. Per creare un nuovo report, selezionare **nuovo rapporto**.

1. Immettere o selezionare le informazioni necessarie per generare un report:

   - **Nome report**: nome del report di analisi da creare.
   - **Trace for target 1 SQL Server**: percorso del file di traccia dalla riproduzione nella destinazione 1.
   - **Trace for target 2 SQL Server**: percorso del file di traccia dalla riproduzione nella destinazione 2.

1. Selezionare **Avvia** per generare il report. Il nuovo report viene visualizzato nella parte superiore dell'elenco. L'icona accanto al report diventa un segno di spunta verde quando il report è stato generato.

A questo punto, visualizzare il report di analisi per ottenere informazioni dettagliate fornite dal test A/B.

Per domande frequenti sui report di analisi, vedere le domande [frequenti sull'analisi](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports).

### <a name="analysis-report"></a>Report di analisi

Nella prima pagina del report vengono visualizzate le informazioni sulla versione e sulla build per i server di destinazione in cui è stato eseguito l'esperimento. È possibile usare la soglia per regolare la sensibilità o la tolleranza dell'analisi di test A/B. Per impostazione predefinita, la soglia è impostata su 5%. Un miglioramento delle prestazioni superiore o uguale al 5% viene classificato come **migliorato**. Selezionare opzioni nel menu a discesa per valutare il report utilizzando diverse soglie per le prestazioni.

![Soglia](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

Due grafici a torta mostrano le implicazioni sulle prestazioni della differenza tra i due server di destinazione per il carico di lavoro. Il grafico a sinistra è basato sul conteggio delle esecuzioni. Il grafico a destra si basa su query distinte. Sono disponibili cinque categorie possibili:

- **Migliorato**: statisticamente, la query è stata eseguita in modo migliore sulla destinazione 2 rispetto alla destinazione 1.
- **Danneggiato**: statisticamente, la query è peggiorata nella destinazione 2 rispetto alla destinazione 1.
- **Stesso**: non esiste alcuna differenza statistica per la query tra target 1 e target 2.
- **Non è possibile valutare**: le dimensioni del campione per la query sono troppo ridotte per l'analisi statistica. Per l'analisi di test A/B, DEA richiede che le stesse query dispongano di almeno 30 esecuzioni in ogni destinazione.
- **Errore**: errore della query almeno una volta in una delle destinazioni.

![Grafico a torta](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

Selezionare una sezione per eseguire il drill-down in una determinata categoria e ottenere le metriche delle prestazioni, incluso il **non può valutare** la sezione della torta.

La pagina di drill-down per una categoria di modifiche delle prestazioni mostra un elenco di query nella categoria. La pagina di **errore** contiene tre schede:

- **Nuovi errori**: errori visualizzati sulla destinazione 2 ma non sulla destinazione 1.
- **Errori esistenti**: errori visualizzati sia nella destinazione 1 che nella destinazione 2.
- **Errori risolti**: errori visualizzati nella destinazione 1 ma non nella destinazione 2.

   ![Pagina di errore](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

Selezionare una query per passare a una pagina di **Riepilogo del confronto** per la query.

Nella pagina **Riepilogo confronto** vengono visualizzate le statistiche di riepilogo per la query. Il riepilogo include il numero di esecuzioni, la durata media, la CPU media, le letture e le Scritture significative e il conteggio degli errori.

![Statistiche di riepilogo](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

Se la query è una query di errore, nella scheda **informazioni sull'errore** vengono visualizzate ulteriori informazioni sull'errore. Nella scheda **informazioni sul piano di query** vengono visualizzate informazioni sui piani di query utilizzati per la query nella destinazione 1 e nella destinazione 2.

![Piano di query](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

In qualsiasi pagina del report di analisi, selezionare il pulsante **stampa** in alto a destra per stampare tutti gli elementi visibili.

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come produrre un file di traccia con un log degli eventi che si verificano in un server, vedere [Capture Trace](database-experimentation-assistant-capture-trace.md).

- Per un'introduzione di 19 minuti a DEA e dimostrazione, Guarda il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
