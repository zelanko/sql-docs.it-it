---
title: Aggiornamento SQL Server locale a SQL Server o SQL Server nelle macchine virtuali di Azure usando Data Migration Assistant | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per eseguire l'aggiornamento di un Server SQL locale a una versione successiva di SQL Server o a SQL Server in macchine virtuali di Azure
ms.custom: ''
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 672473c4e4cfaf5314f53ae7d3a351cb82a93e6d
ms.sourcegitcommit: 179ab0e55f918f58a18c43af076130f4ac3decd6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875174"
---
# <a name="upgrade-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>Eseguire l'aggiornamento in SQL Server locale a SQL Server o SQL Server in macchine virtuali di Azure usando Data Migration Assistant

Data Migration Assistant offre valutazioni senza problemi di SQL Server in locale e gli aggiornamenti alle versioni successive di SQL Server o la migrazione a SQL Server in macchine virtuali di Azure o Database SQL di Azure.

Questo articolo vengono fornite istruzioni dettagliate per l'aggiornamento di SQL Server in locale per le versioni successive di SQL Server o a SQL Server in macchine virtuali di Azure usando Data Migration Assistant.

## <a name="create-a-new-migration-project"></a>Creare un nuovo progetto di migrazione

1. Nel riquadro sinistro, selezionare **New** (+) e quindi la **migrazione** tipo di progetto.

2. Il tipo di server di origine e di destinazione impostato su **SQL Server** se si sta aggiornando un SQL Server locale a una versione più recente di on-premises SQL Server.

3. Selezionare **Create**.

   ![Crea progetto di migrazione](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Specificare l'origine e destinazione

1. Per l'origine, immettere il nome dell'istanza SQL Server nel **nome Server** campo le **i dettagli del server di origine** sezione. 

2. Selezionare il **tipo di autenticazione** supportati dall'istanza di SQL Server di origine.

3. Per la destinazione, immettere il nome dell'istanza SQL Server nel **nome Server** campo le **i dettagli del server di destinazione** sezione. 

4. Selezionare il **tipo di autenticazione** supportati dall'istanza di SQL Server di destinazione.

5. È consigliabile crittografare la connessione selezionando **Encrypt connection** nel **delle proprietà di connessione** sezione.

6. Scegliere **Avanti**.

   ![Pagina di origine e di destinazione specifica](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Aggiungere i database

1. Scegliere i database specifici che si desidera migrare selezionando solo questi database, nel riquadro sinistro della finestra di **aggiungono database** pagina.

   Per impostazione predefinita sono selezionati tutti i database utente nell'istanza di SQL Server di origine per la migrazione

2. Usare le impostazioni della migrazione sul lato destro della pagina per impostare le opzioni di migrazione che vengono applicate ai database, eseguire le operazioni seguenti.

   > [!NOTE]
   > È possibile applicare le impostazioni di migrazione in tutti i database che si esegue la migrazione, selezionando il server nel riquadro sinistro. È anche possibile configurare un database singolo con impostazioni specifiche selezionando il database nel riquadro sinistro.

    a. Specificare il **condiviso percorso accessibile dal server SQL di origine e destinazione per l'operazione di backup**. Assicurarsi che l'account del servizio in esecuzione l'origine SQL Server istanza dispone di scrivere privilegi per la posizione condivisa e l'account del servizio di destinazione dispone di privilegi di lettura per la posizione condivisa.

    b. Specificare il percorso in cui ripristinare i dati e file di log transazionale nel server di destinazione.

    ![Aggiungi pagina di database](../dma/media/AddDatabases.png)

3. Immettere un percorso condiviso a cui le istanze di SQL Server di origine e di destinazione hanno accesso, nelle **condividono opzioni posizione** casella.

4. Se non è possibile fornire un percorso condiviso che istanze di SQL Server di origine e destinazione hanno accesso, selezionare **copiare i backup del database in un percorso diverso che il server di destinazione può leggere e ripristinare dalla**. Quindi, immettere un valore per il **percorso per i backup per l'opzione di ripristino** casella. 

   Assicurarsi che l'account utente che esegue Data Migration Assistant disponga dei privilegi necessari per il percorso di backup di lettura e scrittura i privilegi per il percorso da cui ripristinare il server di destinazione.

   ![Opzione per copiare i backup dei database in un percorso diverso](../dma/media/CopyDatabaseDifferentLocation.png)

5. Selezionare **Avanti**.

Data Migration Assistant esegue le convalide di cartelle di backup, dati e file di log. Se qualsiasi convalida non riesce, correggere le opzioni e quindi selezionare **successivo**.

## <a name="select-logins"></a>Selezionare gli account di accesso

1. Selezionare un account di accesso specifici per la migrazione.

   > [!IMPORTANT]
   > Assicurarsi di selezionare gli account di accesso viene eseguito il mapping a uno o più utenti nei database selezionati per la migrazione.   

   Per impostazione predefinita, tutti i Server SQL e Windows gli account di accesso che soddisfano le condizioni per la migrazione sono selezionati per la migrazione.

2. Selezionare **avviare la migrazione**.

   ![Selezionare gli account di accesso e avviare la migrazione](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Visualizzare i risultati

È possibile monitorare l'avanzamento della migrazione sul **visualizzare i risultati** pagina.

![Pagina di visualizzazione dei risultati](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Esportare i risultati della migrazione

1. Fare clic su **esportare report** in fondo il **visualizzare risultati** pagina per salvare i risultati di migrazione in un file CSV.

2. Esaminare il file salvato per informazioni dettagliate relative alla migrazione di account di accesso e quindi verificare le modifiche.

## <a name="see-also"></a>Vedere anche

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: Impostazioni di configurazione](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: Le procedure consigliate](../dma/dma-bestpractices.md)
