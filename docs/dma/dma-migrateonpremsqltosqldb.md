---
title: Eseguire la migrazione di un'istanza locale SQL Server o SQL Server in macchine virtuali di Azure al Database SQL di Azure usando Data Migration Assistant | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per eseguire la migrazione di un Server SQL locale per Database SQL di Azure
ms.custom: ''
ms.date: 03/12/2019
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
ms.author: rajpo
manager: craigg
ms.openlocfilehash: d807396f7c8bd334de38cdc1744f6bee90d619e0
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57974061"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Eseguire la migrazione di un'istanza locale SQL Server o SQL Server in macchine virtuali di Azure al Database SQL di Azure con Data Migration Assistant

Data Migration Assistant offre valutazioni senza problemi di SQL Server in locale e gli aggiornamenti alle versioni successive di SQL Server o la migrazione a SQL Server in macchine virtuali di Azure o Database SQL di Azure.

Questo articolo vengono fornite istruzioni dettagliate per la migrazione dei Server SQL locale per Database SQL di Azure usando Data Migration Assistant.   

## <a name="create-a-new-migration-project"></a>Creare un nuovo progetto di migrazione

1. Nel riquadro sinistro, selezionare **New** (+), quindi selezionare la **migrazione** tipo di progetto.

2. Impostare il tipo di origine su **SQL Server** e il server di destinazione digitare per **Database SQL di Azure**.

3. Selezionare **Create**.

   ![Crea progetto di migrazione](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>Specificare il server di origine e il database

1. Per l'origine, sotto **Connetti al server di origine**, nella **nome Server** testo casella, immettere il nome dell'istanza di SQL Server di origine.

2. Selezionare il **tipo di autenticazione** supportati dall'istanza di SQL Server di origine.

   > [!NOTE]
   > È recommedned per crittografare la connessione, selezionare la **Encrypt connection** casella di controllo sotto **connessione poperties**.

    ![Selezionare il server di origine](../dma/media/select-source-server.png)

3. Selezionare **Connetti**.

4. Selezionare un database di origine singolo per eseguire la migrazione al Database SQL di Azure.

   > [!NOTE]
   > Se si desidera valutare il database e la visualizzazione e applicare soluzioni consigliate prima della migrazione, seleziona la **valutazione database prima della migrazione?** casella di controllo.

    ![Selezionare il database di origine](../dma/media/select-source-database.png)

5. Selezionare **Avanti**.

## <a name="specify-the-target-server-and-database"></a>Specificare il server di destinazione e il database

1. Per la destinazione, sotto **Connetti al server di destinazione**, nella **nome Server** testo casella, immettere il nome dell'istanza del Database SQL di Azure. 

2. Selezionare il **tipo di autenticazione** supportati dall'istanza di Database SQL di Azure di destinazione.

   > [!NOTE]
   > È recommedned per crittografare la connessione, selezionare la **Encrypt connection** casella di controllo sotto **connessione poperties**.

     ![Selezionare il server di destinazione](../dma/media/select-target-server.png)

3. Selezionare **Connetti**.

4. Selezionare un database di destinazione singola in cui eseguire la migrazione.

   > [!NOTE]
   > Se si prevede di eseguire la migrazione di utenti Windows, nelle **nome di dominio di destinazione utente esterno** testo, assicurarsi che il nome di dominio utente esterno di destinazione sia specificato correttamente.

    ![Seleziona database di destinazione](../dma/media/select-target-database.png)

5. Selezionare **Avanti**.

## <a name="select-schema-objects"></a>Selezionare gli oggetti dello schema

1.  Selezionare gli oggetti dello schema dal database di origine che si desidera eseguire la migrazione al Database SQL di Azure.

    ![Selezionare gli oggetti dello schema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Alcuni degli oggetti che non possono essere convertiti come-è vengono presentati con opportunità di correzione automatica. Facendo clic su questi oggetti nel riquadro sinistro vengono visualizzate le correzioni suggerite nel riquadro destro. Esaminare le correzioni e specificare se applicare o ignorare tutte le modifiche, oggetto per oggetto. Si noti che applicare o ignorare tutte le modifiche per un oggetto non interferiscano con le modifiche agli altri oggetti di database. Le istruzioni che non possono essere convertite o corretti automaticamente vengono riprodotte al database di destinazione e impostata come commento.

    ![Correzione suggerita](../dma/media/suggested-fix.png)

2. Selezionare **lo script SQL generale**.
 
3. Rivedere lo script generato.

    ![Script generato](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>Distribuire lo schema

1. Selezionare **Distribuisci schema**.

2. Esaminare i risultati della distribuzione dello schema.
 
    ![Risultati della distribuzione dello schema](../dma/media/schema-deployment-results.png)

3. Selezionare **la migrazione dei dati** per avviare il processo di migrazione dei dati.
 
4. Selezionare le tabelle con i dati da migrare.

    ![Selezionare le tabelle da migrare](../dma/media/select-tables-to-migrate.png) 

5. Selezionare **avviare la migrazione dei dati**.
 
Schermata finale Mostra lo stato complessivo.

   ![Stato di migrazione](../dma/media/migration-status.png) 

## <a name="see-also"></a>Vedere anche

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: Impostazioni di configurazione](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: Le procedure consigliate](../dma/dma-bestpractices.md)
