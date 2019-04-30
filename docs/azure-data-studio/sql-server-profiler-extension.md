---
title: Estensione di SQL Server Profiler
titleSuffix: Azure Data Studio
description: Installare e usare l'estensione di SQL Server Profiler (anteprima) di Studio dei dati di Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: b883883cbe201de32020e86ca2cd38746caf46be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309690"
---
# <a name="sql-server-profiler-extension-preview"></a>Estensione di SQL Server Profiler (anteprima)

L'estensione di SQL Server Profiler (anteprima) offre una semplice soluzione di analisi di SQL Server simile al Profiler di SQL Server Management Studio (SSMS), ad eccezione di compilato usando XEvents. SQL Server Profiler è molto facile da usare e ha i valori predefiniti ottimale per le configurazioni più comuni di analisi. L'esperienza utente è ottimizzato per l'esplorazione tramite eventi e visualizzazione del testo Transact-SQL (T-SQL) associato. Il Profiler di Server SQL per Azure Data Studio si presuppone inoltre i valori predefiniti ottimale per la raccolta delle attività di esecuzione di T-SQL con un'esperienza utente di facile da usare. Questa estensione è attualmente in anteprima.

**SQL Profiler-casi di utilizzo comuni:**

- Esecuzione dei singoli passaggi di query problematiche allo scopo di individuare la causa del problema.
- Individuazione e diagnosi di query con esecuzione rallentata.
- Acquisizione della serie di istruzioni Transact-SQL che hanno causato un problema.
- Monitoraggio delle prestazioni di SQL Server per ottimizzare i carichi di lavoro.
- Correlazione dei contatori delle prestazioni per la diagnosi dei problemi.


## <a name="install-the-sql-server-profiler-extension"></a>Installare l'estensione di SQL Server Profiler

1. Per aprire la gestione delle estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni o scegliere **Estensioni** dal menu **Visualizza**.
2. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![gestore estensioni del profiler](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. Selezionare l'estensione desiderata e scegliere **Installa**.
2. Selezionare **Ricarica** per abilitare l'estensione (richiesto solo la prima volta in cui l'estensione viene installata).

## <a name="start-profiler"></a>Avviare Profiler

1. Per avviare Profiler, assicurarsi prima di tutto una connessione a un server nella scheda Server.
2. Dopo aver effettuato una connessione, digitare **Alt + P** per avviare Profiler.
3. Per avviare Profiler, digitare **Alt + S.** Puoi ora iniziare a ottenere gli eventi estesi.
    ![gestore estensioni del profiler](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Per interrompere il Profiler, digitare **Alt + S.** Questo tasto di scelta rapida è un elemento toggle.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Profiler ed eventi estesi, vedere [eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).





