---
title: Estensione di file dacpac di SQL Server
titleSuffix: Azure Data Studio
description: Installare e usare l'estensione di file dacpac di SQL Server (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 70b06749d1cbecc2127c70fee28b60f49583d5ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797987"
---
# <a name="sql-server-dacpac-extension-preview"></a>Estensione dacpac di SQL Server (anteprima)

**La creazione guidata applicazione livello dati** offre un'esperienza facile da usare per distribuire ed estrarre file con estensione dacpac e importare ed esportare file con estensione bacpac.

Questa esperienza è attualmente la versione di anteprima iniziale. Per segnalare problemi e richieste di funzionalità [qui.](https://github.com/microsoft/azuredatastudio/issues)

![azioni dati](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisiti
 * Questa procedura guidata richiede una connessione attiva a un'istanza di SQL Server per iniziare.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>Come si inizia la creazione guidata applicazione livello dati?
 * Il punto di ingresso principale per la procedura guidata è un database in Esplora oggetti fare clic destro e fare clic su **Creazione guidata applicazione livello dati**.
 * Se un utente è connesso a un'istanza di SQL Server, l'utente può anche avviare la procedura guidata dal riquadro comandi (Ctrl + MAIUSC + P) eseguendo una ricerca per **Creazione guidata applicazione livello dati.**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>Perché usare la procedura guidata dell'applicazione livello dati?
 Questa procedura guidata è stata creata per aggiungere la possibilità di estrarre e distribuire i file con estensione dacpac e importare ed esportare file bacpac in Azure Data Studio.

## <a name="install-the-sql-server-dacpac-extension"></a>Installare l'estensione di file dacpac di SQL Server

1. Per aprire la gestione delle estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni o scegliere **Estensioni** dal menu **Visualizza**.
2. Selezionare l'estensione di file dacpac di SQL Server e fare clic su **installare**.
1. Selezionare **Ricarica** per abilitare l'estensione (richiesto solo la prima volta in cui l'estensione viene installata).
2. Passare al dashboard di gestione facendo clic con il tasto destro del mouse sul server o sul database e selezionando **Gestisci**.
3. Le estensioni installate vengono visualizzate come schede nel dashboard di gestione:

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui file dacpac, [controllare la documentazione.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)