---
title: Panoramica del processo di confronto del carico di lavoro
description: Database Experimentation Assistant (DEA) è una soluzione di test A/B per le modifiche in ambienti SQL Server, ad esempio aggiornamenti o nuovi indici.
ms.date: 11/16/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 18cba7abf0d73197c248a62283d52126873169a3
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165755"
---
# <a name="overview-of-the-workload-comparison-process"></a>Panoramica del processo di confronto del carico di lavoro

Database Experimentation Assistant (DEA) consente di valutare il modo in cui il carico di lavoro nel server di origine (nell'ambiente corrente) viene eseguito nel nuovo ambiente. DEA guida l'utente durante l'esecuzione di un test A/B completando tre fasi:

- Acquisizione di una traccia del carico di lavoro nel server di origine.
- Riproduzione della traccia del carico di lavoro acquisita sulla destinazione 1 e destinazione 2.
- Analisi delle tracce del carico di lavoro riprodotte raccolte da target 1 e target 2.

Questo articolo fornisce una panoramica di questo processo.

## <a name="capturing-a-workload-trace"></a>Acquisizione di una traccia del carico di lavoro

La prima fase di SQL Server test A/B consiste nell'acquisire una traccia nel server di origine. Il server di origine è in genere il server di produzione. I file di traccia acquisiscono l'intero carico di lavoro di query su tale server, inclusi i timestamp.

Considerazioni:

- Prima di iniziare a acquisire la traccia del carico di lavoro, assicurarsi di eseguire il backup dei database da cui si sta acquisendo la traccia.
- È necessario configurare un utente di DEA per la connessione al database tramite l'autenticazione di Windows.
- Un account del servizio SQL Server richiede l'accesso al percorso del file di traccia di origine.
- Per determinare se le prestazioni di una query sono state migliorate o diminuite, la query deve essere eseguita almeno 15 volte durante il periodo di acquisizione.

## <a name="replaying-a-workload-trace"></a>Riproduzione di una traccia del carico di lavoro

La seconda fase di SQL Server test A/B consiste nel riprodurre il file di traccia acquisito in due server di destinazione:

Target 1, che simula la destinazione del server di origine 2, che simula l'ambiente di destinazione proposto.

Le configurazioni hardware di target 1 e target 2 devono essere il più simile possibile, in modo SQL Server possibile analizzare accuratamente l'effetto sulle prestazioni delle modifiche proposte.

Considerazioni:

- Per riprodurre una traccia del carico di lavoro, è necessario configurare i computer per l'esecuzione di Riesecuzione distribuita tracce (DReplay).
- Assicurarsi di ripristinare i database nei server di destinazione usando il backup del server di origine.
- È consigliabile riavviare il servizio SQL Server (MSSQLSERVER) nell'applicazione Servizi per migliorare la coerenza dei risultati della valutazione. La memorizzazione nella cache delle query in SQL Server può influire sui risultati della valutazione.

## <a name="analyzing-the-replayed-workload-traces"></a>Analisi delle tracce del carico di lavoro riprodotte

La fase finale del processo consiste nel generare un report di analisi utilizzando le tracce di riproduzione. È quindi possibile esaminare il report di analisi per informazioni approfondite sulle potenziali implicazioni delle prestazioni della modifica proposta.

Considerazioni:

- Se uno o più componenti risultano mancanti, viene visualizzata una pagina dei prerequisiti con collegamenti per i download quando si tenta di generare un nuovo report di analisi (connessione Internet necessaria).
- Per visualizzare un report generato in una versione precedente dello strumento, è necessario prima aggiornare lo schema.

## <a name="see-also"></a>Vedere anche

- Per informazioni su come produrre un file di traccia con un log degli eventi che si verificano in un server, vedere [Capture Trace](database-experimentation-assistant-capture-trace.md).
