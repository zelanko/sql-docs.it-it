---
title: Estensione SQL Server dacpac
titleSuffix: Azure Data Studio
description: Installare e usare l'estensione SQL Server dacpac (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959191"
---
# <a name="sql-server-dacpac-extension-preview"></a>Estensione dacpac di SQL Server (anteprima)

**La procedura guidata dell'applicazione a livello di dati** offre una soluzione di facile utilizzo per distribuire ed estrarre file con estensione DACAPC e importare ed esportare file con estensione BACPAC.

Questa funzionalità è attualmente disponibile in versione di anteprima iniziale. Segnalare eventuali problemi e richieste di funzionalità [qui](https://github.com/microsoft/azuredatastudio/issues).

![azioni dati](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisiti
 * Per avviare questa procedura guidata è necessaria una connessione attiva a un'istanza di SQL Server.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>Com'è possibile avviare la procedura guidata dell'applicazione a livello di dati?
 * Il punto di ingresso principale della procedura guidata è fare clic con il pulsante destro del mouse su un database in Esplora oggetti e quindi scegliere **Data-tier Application wizard** (Procedura guidata dell'applicazione a livello di dati).
 * Se un utente è connesso a un'istanza di SQL Server, può avviare la procedura guidata anche dal riquadro comandi (CTRL+MAIUSC+P) cercando **Procedura guidata dell'applicazione a livello di dati**.

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>Perché usare la procedura guidata dell'applicazione a livello di dati?
 Questa procedura guidata è stata creata per aggiungere la possibilità di estrarre e distribuire file con estensione DACPAC e di importare ed esportare file con estensione BACPAC in Azure Data Studio.

## <a name="install-the-sql-server-dacpac-extension"></a>Installare l'estensione SQL Server dacpac

1. Per aprire Gestione estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni oppure l'opzione **Estensioni** dal menu **Visualizza**.
2. Selezionare l'estensione SQL Server dacpac e fare clic su **Installa**.
1. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).
2. Passare al dashboard di gestione facendo clic con il pulsante destro del mouse sul server o sul database in uso e scegliendo quindi **Gestisci**.
3. Le estensioni installate vengono visualizzate come schede nel dashboard di gestione:

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su dacpac, [consultare la documentazione di riferimento](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017).