---
title: Panoramica della soluzione Database sperimentazione Assistant per SQL Server viene aggiornato
description: Panoramica dell'Assistente di sperimentazione di Database
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 1c2a28a5dc83d22a327bf797358d5edae69eb82b
ms.sourcegitcommit: 9ea11d738503223b46d2be5db6fed6af6265aecc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/07/2019
ms.locfileid: "56987827"
---
# <a name="overview-of-database-experimentation-assistant"></a>Panoramica dell'Assistente di sperimentazione di Database

Database sperimentazione Assistant DEA () è una soluzione di sperimentazione per gli aggiornamenti di SQL Server. DEA consentono di valutare una versione di destinazione di SQL Server per un carico di lavoro specifico. I clienti che eseguono l'aggiornamento da versioni precedenti di SQL Server (a partire 2005) a una versione più recente di SQL Server possono usare le metriche di analisi che fornisce lo strumento. 

Le metriche di analisi DEA includono:
- Query che contengono errori di compatibilità
- Le query con funzionalità ridotte e piani di query
- Altri dati di confronto del carico di lavoro

Dati di confronto possono causare una probabilità elevata e una corretta esperienza di aggiornamento.

Per un'introduzione di 19 minuti DEA e una dimostrazione, guardare il video seguente:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>Ottenere DEA

Per installare, DEA [scaricare](https://www.microsoft.com/download/details.aspx?id=54090) la versione più recente dello strumento. Eseguire quindi il **DatabaseExperimentationAssistant.exe** file.

## <a name="solution-architecture-for-comparing-workloads"></a>Architettura della soluzione per il confronto tra i carichi di lavoro

Il diagramma seguente mostra l'architettura della soluzione per un confronto di carico di lavoro. Il confronto di carico di lavoro Usa DEA e Distributed Replay durante un aggiornamento da SQL Server 2008 a SQL Server 2016.

![Architettura della soluzione di confronto del carico di lavoro](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Prerequisiti DEA

Di seguito sono alcuni prerequisiti per l'esecuzione DEA:
- Requisiti hardware minimi: Un computer a core singolo con 3,5 GB di RAM.
- Requisito hardware ideale: Una CPU di otto core (con 3,5 GB di RAM o superiore). I processori che dispone di più di otto core non migliorano DEA Runtime.
- È necessario un ulteriore 33% delle dimensioni di traccia delle prestazioni per archivio A, B e database di report di analisi.

## <a name="configure-dea"></a>Configurare DEA

Nell'architettura dell'ambiente dei prerequisiti, è consigliabile installare DEA *nello stesso computer del controller di riesecuzione distribuita*. Questa esercitazione consente di evitare le chiamate tra computer e semplifica la configurazione.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>Configurazione necessaria per il confronto di carico di lavoro usando DEA

DEA si connette al server di database tramite l'autenticazione di Windows. Assicurarsi che un utente che esegue DEA possa connettersi ai server di database (origine, destinazione e analisi) tramite l'autenticazione di Windows.

**Acquisire i requisiti di configurazione**:

*   Utente che esegue DEA può connettersi al server di database di origine con l'autenticazione di Windows.
*   Utente che esegue DEA con diritti sysadmin nel server di database di origine.
*   Account del servizio che esegue il server di database di origine ha accesso in scrittura al percorso della cartella di traccia.

Per altre informazioni, vedere il [acquisire domande frequenti](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisiti di configurazione per la riproduzione**: 

*   Utente che esegue DEA può connettersi al server di database di destinazione tramite l'autenticazione di Windows.
*   Utente che esegue DEA con diritti sysadmin nel server di database di destinazione.
*   Account del servizio in esecuzione il server di database di destinazione ha accesso in scrittura al percorso della cartella di traccia.
*   Account del servizio client riesecuzione distribuita di esecuzione è possibile connettersi al server di database di destinazione tramite l'autenticazione di Windows.
*   DEA comunica con il controller di riesecuzione distribuita tramite interfacce COM. Assicurarsi che le porte TCP siano aperte per le richieste in ingresso nel controller di riesecuzione distribuita.

Per altre informazioni, vedere il [riprodurre domande frequenti](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Requisiti di configurazione analisi**: 

*   Utente che esegue DEA può connettersi al server di database di analisi tramite l'autenticazione di Windows.
*   Utente che esegue DEA con diritti sysadmin nel server di database di origine.

Per altre informazioni, vedere il [domande frequenti su analisi](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Impostare i dati di telemetria

DEA dispone di una funzionalità abilitate per internet che invia informazioni di telemetria a Microsoft. Microsoft raccoglie dati di telemetria per migliorare l'esperienza di prodotto. I dati di telemetria è facoltativo. Le informazioni raccolte viene salvate anche nel computer per il controllo locale. È sempre possibile visualizzare l'inventario raccolto. Tutti i file di log da DEA vengono salvati nella cartella % temp %\\cartella DEA.

È possibile decidere quali eventi vengono raccolti. È inoltre possibile decidere se gli eventi raccolti vengono inviati a Microsoft. Esistono quattro tipi di eventi:

*   **TraceEvent**: Eventi di utilizzo per l'applicazione (ad esempio, "acquisizione attivate stop").
*   **Eccezione**: Eccezione generata durante l'utilizzo dell'applicazione.
*   **DiagnosticEvent**: Un log eventi per facilitare la diagnosi quando si verificano problemi (*non* inviate a Microsoft).
*   **FeedbackEvent**: Feedback utente che viene inviato tramite l'applicazione.

Questi passaggi illustrano come scegliere gli eventi che vengono raccolti e indica se gli eventi vengono inviati a Microsoft:

1.  Passare al percorso in cui è installata DEA (ad esempio, c\\Program Files (x86)\\Microsoft Corporation\\Database sperimentazione Assistant).
2.  Aprire i due file con estensione config: DEA.exe.config (per l'applicazione) e DEACmd.exe.config (per l'interfaccia CLI).
3.  Per arrestare la raccolta di un tipo di evento, impostare il valore della *evento* (ad esempio **TraceEvent**) per **false**. Per iniziare a raccogliere nuovamente l'evento, impostare il valore su **true**.
4.  Per arrestare il salvataggio di copie locali degli eventi, impostare il valore della **TraceLoggerEnabled** al **false**. Per iniziare il salvataggio di copie locali anche in questo caso, impostare il valore su **true**.
5.  Per arrestare l'invio di eventi a Microsoft, impostare il valore della **AppInsightsLoggerEnabled** al **false**. Per iniziare a inviare eventi a Microsoft anche in questo caso, impostare il valore su **true**.

DEA è disciplinata dalle [informativa sulla Privacy Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Passaggi successivi

[Iniziare a usare](database-experimentation-assistant-get-started.md) illustra i passaggi necessari per acquisire e riprodurre e analizzare una traccia.
