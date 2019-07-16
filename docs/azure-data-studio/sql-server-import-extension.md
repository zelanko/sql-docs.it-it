---
title: Estensione di importazione SQL Server
titleSuffix: Azure Data Studio
description: Installare e usare l'estensione di SQL Server Import (anteprima) di Studio dei dati di Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959129"
---
# <a name="sql-server-import-extension-preview"></a>Estensione di SQL Server Import (anteprima)

L'estensione di SQL Server Import (anteprima) converte file txt e CSV in una tabella SQL. Questa procedura guidata Usa un framework di Microsoft Research detto [Program Synthesis using esempi (PROSE)](https://microsoft.github.io/prose/) analizzare in modo intelligente il file con input minimo dell'utente. È un framework potente per la gestione dei dati ed è la stessa tecnologia alla base Flash Fill in Microsoft Excel

Per altre informazioni sulla versione di SSMS di questa funzionalità, è possibile leggere [questo articolo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Installare l'estensione di SQL Server Import

1. Per aprire la gestione delle estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni o scegliere **Estensioni** dal menu **Visualizza**.
2. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![gestore di estensioni di importazione](media/sql-server-import-extension/import-wizard-install.png)

1. Selezionare l'estensione desiderata e scegliere **Installa**.
2. Selezionare **Ricarica** per abilitare l'estensione (richiesto solo la prima volta in cui l'estensione viene installata).

## <a name="start-import-wizard"></a>Avviare Importazione guidata

1. Per avviare SQL Server Import, assicurarsi prima di tutto una connessione a un server nella scheda Server.
2. Dopo aver effettuato una connessione, eseguire il drill down il database di destinazione che si desidera importare un file in una tabella SQL.
3. Fare doppio clic sul database e fare clic su **importazione guidata**.
    ![Aprire importazione guidata](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importazione di un file
1. Facendo clic su per avviare la procedura guidata, il server e database sono già compilato automaticamente. Se sono presenti altre connessioni attive, è possibile selezionare nell'elenco a discesa. 
    
    Selezionare un file facendo clic **Sfoglia.** Dovrebbe essere il nome di tabella basato sul nome del file di compilazione automatica, ma è anche possibile modificarla manualmente.

    Per impostazione predefinita, lo schema sarà dbo, ma è possibile modificarlo. Fare clic su **Avanti** per continuare.
    ![file di input](media/sql-server-import-extension/import-wizard-input-file.png)
1. La procedura guidata genererà un'anteprima basata le prime 50 righe. Non vi è alcuna azione aggiuntiva in questa pagina diverso da quello di verifica per determinare se che i dati siano accurati. Fare clic su **Avanti** per continuare.
    ![Aprire importazione guidata](media/sql-server-import-extension/import-wizard-preview-data.png)
2. In questa pagina, è possibile apportare modifiche al nome di colonna, tipo di dati, se si tratta di una chiave primaria o per consentire i valori null. È possibile apportare modifiche tante nel modo desiderato. Fare clic su **Import Data** per procedere.
    ![Aprire importazione guidata](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Questa pagina fornisce un riepilogo delle azioni scelte. È anche possibile visualizzare se la tabella inserito correttamente o meno. 

    È possibile scegliere **, Previous** se è necessario apportare modifiche, o **nuovo file di importazione** per importare rapidamente un altro file.
    ![Aprire importazione guidata](media/sql-server-import-extension/import-wizard-summary.png)
1. Verificare se la tabella importata correttamente l'aggiornamento del database di destinazione o eseguendo una query di selezione sul nome della tabella.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sull'importazione guidata, vedere la [post di blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Per altre informazioni su PROSE, leggere il [documentazione.](https://microsoft.github.io/prose/)
