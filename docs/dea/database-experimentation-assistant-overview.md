---
title: Panoramica della soluzione Database Experimentation Assistant per gli aggiornamenti SQL Server
description: Panoramica di Database Experimentation Assistant
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 656236be66ecb2b7127e45ab1ef361f1eb7703e6
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637938"
---
# <a name="overview-of-database-experimentation-assistant"></a>Panoramica di Database Experimentation Assistant

Database Experimentation Assistant (DEA) è una soluzione di sperimentazione per gli aggiornamenti di SQL Server. DEA può aiutarti a valutare una versione di destinazione di SQL Server per un carico di lavoro specifico. I clienti che eseguono l'aggiornamento da versioni precedenti di SQL Server (a partire da 2005) a una versione più recente di SQL Server possono usare la metrica di analisi fornita dallo strumento.

Le metriche di analisi di DEA includono:

- Query con errori di compatibilità
- Query degradate e piani di query
- Altri dati di confronto del carico di lavoro

I dati di confronto possono comportare una maggiore confidenza e un'esperienza di aggiornamento corretta.

## <a name="get-dea"></a>Ottenere DEA

Per installare DEA, [scaricare](https://www.microsoft.com/download/details.aspx?id=54090) la versione più recente dello strumento. Eseguire quindi il file **DatabaseExperimentationAssistant. exe** .

## <a name="solution-architecture-for-comparing-workloads"></a>Architettura della soluzione per il confronto dei carichi di lavoro

Il diagramma seguente illustra l'architettura della soluzione per un confronto del carico di lavoro. Il confronto del carico di lavoro USA DEA e Riesecuzione distribuita durante un aggiornamento da SQL Server 2008 a SQL Server 2016.

![Architettura della soluzione di confronto del carico di lavoro](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>Prerequisiti di DEA

Di seguito sono riportati alcuni prerequisiti per l'esecuzione di DEA:

- Requisito hardware minimo: un computer a core singolo con 3,5 GB di RAM.
- Requisito hardware ideale: CPU con 8 core (con 3,5 GB di RAM o superiore). I processori con più di otto core non migliorano i runtime di DEA.
- Per archiviare A, B e database di analisi dei report è necessario un ulteriore 33% delle dimensioni della traccia delle prestazioni.

## <a name="configure-dea"></a>Configura DEA

Nell'architettura dell'ambiente prerequisiti è consigliabile installare DEA nello *stesso computer del controller di riesecuzione distribuita*. Questa pratica evita le chiamate tra computer e semplifica la configurazione.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>Configurazione richiesta per il confronto dei carichi di lavoro tramite DEA

DEA si connette ai server di database tramite l'autenticazione di Windows. Assicurarsi che un utente che esegue DEA possa connettersi ai server di database (origine, destinazione e analisi) usando l'autenticazione di Windows.

**Requisiti di configurazione di acquisizione**:

- L'utente che esegue DEA può connettersi al server di database di origine usando l'autenticazione di Windows.
- L'utente che esegue DEA dispone dei diritti sysadmin nel server di database di origine.
- L'account del servizio che esegue il server di database di origine ha accesso in scrittura al percorso della cartella di traccia.

Per ulteriori informazioni, vedere le [domande frequenti sull'acquisizione](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**Requisiti di configurazione della riproduzione**: 

- L'utente che esegue DEA può connettersi al server di database di destinazione tramite l'autenticazione di Windows.
- L'utente che esegue DEA dispone dei diritti sysadmin nel server di database di destinazione.
- L'account del servizio che esegue i server del database di destinazione ha accesso in scrittura al percorso della cartella di traccia.
- L'account del servizio che esegue Riesecuzione distribuita client può connettersi al server di database di destinazione tramite l'autenticazione di Windows.
- DEA comunica con il controller di Riesecuzione distribuita usando le interfacce COM. Verificare che le porte TCP siano aperte per le richieste in ingresso nel controller di Riesecuzione distribuita.

Per ulteriori informazioni, vedere le [domande frequenti sulla riproduzione](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**Requisiti di configurazione dell'analisi**:

- L'utente che esegue DEA può connettersi al server di database di Analysis usando l'autenticazione di Windows.
- L'utente che esegue DEA dispone dei diritti sysadmin nel server di database di origine.

Per ulteriori informazioni, vedere le [domande frequenti sull'analisi](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>Configurare la telemetria

DEA dispone di una funzionalità abilitata per Internet che può inviare informazioni di telemetria a Microsoft. Microsoft raccoglie i dati di telemetria per migliorare l'esperienza del prodotto. La telemetria è facoltativa. Anche le informazioni raccolte vengono salvate nel computer per il controllo locale. È sempre possibile visualizzare gli elementi raccolti. Tutti i file di log di DEA vengono salvati nella cartella% Temp%\\DEA.

È possibile decidere quali eventi vengono raccolti. Si decide inoltre se gli eventi raccolti vengono inviati a Microsoft. Sono disponibili quattro tipi di eventi:

- **TraceEvent**: eventi di utilizzo per l'applicazione (ad esempio, "attivato arresta acquisizione").
- **Eccezione**: eccezione generata durante l'utilizzo dell'applicazione.
- **DiagnosticEvent**: registro eventi per facilitare la diagnosi quando si verificano problemi (*non* inviati a Microsoft).
- **FeedbackEvent**: Commenti utente inviati tramite l'applicazione.

Questi passaggi illustrano come scegliere quali eventi vengono raccolti e se gli eventi vengono inviati a Microsoft:

1. Passare al percorso in cui è installato DEA (ad esempio, C:\\programmi (x86)\\Microsoft Corporation\\Database Experimentation Assistant).
2. Aprire i due file. config: DEA. exe. config (per l'applicazione) e DEACmd. exe. config (per l'interfaccia della riga di comando).
3. Per interrompere la raccolta di un tipo di evento, impostare il valore dell' *evento* (ad esempio, **TraceEvent**) su **false**. Per iniziare a raccogliere nuovamente l'evento, impostare il valore su **true**.
4. Per arrestare il salvataggio delle copie locali degli eventi, impostare il valore di **TraceLoggerEnabled** su **false**. Per iniziare a salvare di nuovo le copie locali, impostare il valore su **true**.
5. Per arrestare l'invio di eventi a Microsoft, impostare il valore di **AppInsightsLoggerEnabled** su **false**. Per iniziare a inviare nuovamente gli eventi a Microsoft, impostare il valore su **true**.

DEA è disciplinato dall' [informativa sulla privacy Microsoft](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>Passaggi successivi

In [Introduzione vengono](database-experimentation-assistant-get-started.md) illustrati i passaggi necessari per acquisire, riprodurre e analizzare una traccia.
