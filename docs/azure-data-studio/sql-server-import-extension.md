---
title: Estensione SQL Server Import
description: Installare e usare l'estensione SQL Server Import (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a2795282c7a43c5ae582a059ae8b56d1f592e6e6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758340"
---
# <a name="sql-server-import-extension-preview"></a>Estensione SQL Server Import (anteprima)

L'estensione SQL Server Import (anteprima) converte file con estensione TXT e CSV in una tabella SQL. Questa procedura guidata usa un framework sviluppato da Microsoft Research noto come [Program Synthesis using Examples (PROSE)](https://microsoft.github.io/prose/) per analizzare in modo intelligente il file con un intervento minimo dell'utente. Si tratta di un framework avanzato per il data wrangling ed è basato sulla stessa tecnologia usata da Anteprima suggerimenti di Microsoft Excel

Per altre informazioni sulla versione di questa funzionalità per SSMS, è possibile leggere [questo articolo](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard).


## <a name="install-the-sql-server-import-extension"></a>Installare l'estensione SQL Server Import.

1. Per aprire Gestione estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni oppure l'opzione **Estensioni** dal menu **Visualizza**.
2. Selezionare un'estensione disponibile per visualizzarne i dettagli.

   ![Gestione estensione Import](media/sql-server-import-extension/import-wizard-install.png)

1. Selezionare l'estensione desiderata e **installarla**.
2. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).

## <a name="start-import-wizard"></a>Avviare la procedura guidata di Import

1. Per avviare SQL Server Import, creare prima una connessione a un server nella scheda Server.
2. Dopo aver stabilito una connessione, eseguire il drill-down nel database di destinazione all'interno del quale si vuole importare un file in una tabella SQL.
3. Fare clic con il pulsante destro del mouse sul database e scegliere **Import Wizard** (Procedura guidata Import).
    ![apertura procedura guidata Import](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>Importazione di un file
1. Quando si fa clic con il pulsante destro del mouse per avviare la procedura guidata, il server e il database risultano già compilati automaticamente. Se sono presenti altre connessioni attive, è possibile selezionarle nell'elenco a discesa. 
    
    Selezionare un file facendo clic su **Sfoglia**. Il nome della tabella viene compilato automaticamente in base al nome del file, ma è possibile anche modificarlo manualmente.

    Per impostazione predefinita, lo schema sarà dbo, ma anche in questo caso è possibile modificarlo. Fare clic su **Avanti** per continuare.
    ![file di input](media/sql-server-import-extension/import-wizard-input-file.png)
1. La procedura guidata genererà un'anteprima basata sulle prime 50 righe. Non sono previste altre azioni in questa pagina, se non verificare che i siano corretti. Fare clic su **Avanti** per continuare.
    ![apertura procedura guidata Import](media/sql-server-import-extension/import-wizard-preview-data.png)
2. In questa pagina è possibile modificare il nome delle colonne e il tipo di dati, nonché indicare se si tratta di una chiave primaria e se sono consentiti valori null. È possibile apportare tutte le modifiche desiderate. Fare clic su **Importa dati** per continuare.
    ![apertura procedura guidata Import](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. Questa pagina fornisce un riepilogo delle azioni scelte e consente di verificare che la tabella sia stata inserita correttamente. 

    È possibile fare clic su **Completato, Precedente** se è necessario apportare modifiche o **Import new file** (Importa nuovo file) se si vuole importare rapidamente un altro file.
    ![apertura procedura guidata Import](media/sql-server-import-extension/import-wizard-summary.png)
1. Verificare che la tabella sia stata importata correttamente aggiornando il database di destinazione o eseguendo una query SELECT sul nome della tabella.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulla procedura guidata di Import, leggere questo [post di blog](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/).
- Per altre informazioni su PROSE, leggere la [documentazione di riferimento](https://microsoft.github.io/prose/).
