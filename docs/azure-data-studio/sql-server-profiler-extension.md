---
title: Estensione SQL Server Profiler
description: Installare e usare l'estensione SQL Server Profiler (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: f86257f7d024d36109901e09f11ab910525810e5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758314"
---
# <a name="sql-server-profiler-extension-preview"></a>Estensione SQL Server Profiler (anteprima)

L'estensione SQL Server Profiler (anteprima) offre una semplice soluzione di analisi per SQL Server con funzionalità analoghe al profiler di SQL Server Management Studio (SSMS), ma realizzate con eventi estesi. SQL Server Profiler è molto facile da usare e offre valori predefiniti per le più comuni configurazioni di analisi. L'esperienza utente è ottimizzata per la ricerca di eventi e la visualizzazione del testo Transact-SQL (T-SQL) associato. SQL Server Profiler per Azure Data Studio prevede anche valori predefiniti per la raccolta di attività di esecuzione di T-SQL tramite un'esperienza utente di facile utilizzo. Questa estensione è attualmente disponibile in anteprima.

**Casi d'uso comuni di SQL Profiler:**

- Esecuzione dei singoli passaggi di query problematiche allo scopo di individuare la causa del problema.
- Individuazione e diagnosi di query con esecuzione rallentata.
- Acquisizione della serie di istruzioni Transact-SQL che ha generato un problema.
- Monitoraggio delle prestazioni di SQL Server per l'ottimizzazione dei carichi di lavoro.
- Correlazione dei contatori delle prestazioni per la diagnosi dei problemi.


## <a name="install-the-sql-server-profiler-extension"></a>Installare l'estensione SQL Server Profiler

1. Per aprire Gestione estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni oppure l'opzione **Estensioni** dal menu **Visualizza**.
2. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![Gestione estensioni Profiler](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. Selezionare l'estensione desiderata e **installarla**.
2. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).

## <a name="start-profiler"></a>Avvio Profiler

1. Per avviare Profiler, creare prima una connessione a un server nella scheda Server.
2. Dopo aver creato una connessione, digitare **ALT + P** per avviare Profiler.
3. Per avviare Profiler, digitare **ALT + S**. È ora possibile iniziare a visualizzare gli eventi estesi.
    ![Gestione estensioni Profiler](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Per arrestare Profiler, digitare **Alt + S**. Questo tasto di scelta rapida è un elemento Toggle.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Profiler e sugli eventi estesi, vedere [Eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).





