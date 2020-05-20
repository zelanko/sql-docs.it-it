---
title: Aggiornare SQL Server usando il Data Migration Assistant
description: Informazioni su come usare Data Migration Assistant per aggiornare una SQL Server locale a una versione più recente di SQL Server o SQL Server in macchine virtuali di Azure
ms.custom: seo-lt-2019
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
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 00d27decc533d33056a7cc0cb19c2584fea564fb
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885869"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>Aggiornare SQL Server usando il Data Migration Assistant

Il Data Migration Assistant fornisce valutazioni senza problemi della SQL Server locale e degli aggiornamenti a versioni successive di SQL Server o migrazioni a SQL Server in macchine virtuali di Azure o nel database SQL di Azure.

In questo articolo vengono fornite istruzioni dettagliate per l'aggiornamento SQL Server da locale a versioni successive di SQL Server o per SQL Server in macchine virtuali di Azure tramite la Data Migration Assistant.

## <a name="create-a-new-migration-project"></a>Creare un nuovo progetto di migrazione

1. Nel riquadro sinistro selezionare **nuovo** (+) e quindi il tipo di progetto di **migrazione** .

2. Impostare il tipo di server di origine e di destinazione su **SQL Server** se si sta aggiornando una SQL Server locale a una versione successiva di SQL Server locale.

3. Selezionare **Crea**.

   ![Crea progetto di migrazione](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Specificare l'origine e la destinazione

1. Per l'origine, immettere il nome dell'istanza SQL Server nel campo **nome server** della sezione **Dettagli del server di origine** . 

2. Selezionare il **tipo di autenticazione** supportato dall'istanza di SQL Server di origine.

3. Per la destinazione, immettere il nome dell'istanza SQL Server nel campo **nome server** della sezione **Dettagli server di destinazione** . 

4. Consente di selezionare il **tipo di autenticazione** supportato dall'istanza di SQL Server di destinazione.

5. È consigliabile crittografare la connessione selezionando **Crittografa connessione** nella sezione **Proprietà connessione** .

6. Fare clic su **Avanti**.

   ![Specificare la pagina di origine e di destinazione](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Aggiungi database

1. Scegliere i database specifici di cui si desidera eseguire la migrazione selezionando solo i database, nel riquadro sinistro della pagina **Aggiungi database** .

   Per impostazione predefinita, tutti i database utente nell'istanza di SQL Server di origine sono selezionati per la migrazione

2. Utilizzare le impostazioni di migrazione sul lato destro della pagina per impostare le opzioni di migrazione applicate ai database, effettuando le operazioni seguenti.

   > [!NOTE]
   > È possibile applicare le impostazioni di migrazione a tutti i database di cui si sta eseguendo la migrazione selezionando il server nel riquadro sinistro. È anche possibile configurare un singolo database con impostazioni specifiche selezionando il database nel riquadro sinistro.

    a. Specificare il **percorso condiviso accessibile da SQL Server di origine e di destinazione per l'operazione di backup**. Verificare che l'account del servizio che esegue l'istanza di SQL Server di origine disponga dei privilegi di scrittura per il percorso condiviso e che l'account del servizio di destinazione disponga dei privilegi di lettura per il percorso condiviso.

    b. Specificare il percorso in cui ripristinare i dati e i file di log transazionali nel server di destinazione.

    ![Pagina Aggiungi database](../dma/media/AddDatabases.png)

3. Immettere un percorso condiviso a cui possono accedere le istanze di SQL Server di origine e di destinazione, nella casella **Opzioni percorso condivisione** .

4. Se non è possibile fornire un percorso condiviso a cui possono accedere entrambi i server SQL di origine e di destinazione, selezionare **copia i backup del database in un percorso diverso da cui il server di destinazione può leggere e ripristinare**. Immettere quindi un valore per la casella di **opzione percorso per i backup per il ripristino** . 

   Verificare che l'account utente che esegue Data Migration Assistant disponga dei privilegi di lettura per il percorso di backup e i privilegi di scrittura nel percorso da cui viene ripristinato il server di destinazione.

   ![Opzione per copiare i backup del database in un percorso diverso](../dma/media/CopyDatabaseDifferentLocation.png)

5. Selezionare **Avanti**.

Il Data Migration Assistant esegue le convalide sulle cartelle di backup, i dati e i percorsi dei file di log. Se la convalida ha esito negativo, correggere le opzioni e quindi fare clic su **Avanti**.

## <a name="select-logins"></a>Seleziona account di accesso

1. Selezionare account di accesso specifici per la migrazione.

   > [!IMPORTANT]
   > Assicurarsi di selezionare gli account di accesso di cui è stato eseguito il mapping a uno o più utenti nei database selezionati per la migrazione.   

   Per impostazione predefinita, tutti gli account di accesso di SQL Server e Windows che sono idonei per la migrazione sono selezionati per la migrazione.

2. Selezionare **Avvia migrazione**.

   ![Selezionare gli account di accesso e avviare la migrazione](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Visualizzazione dei risultati

È possibile monitorare lo stato di avanzamento della migrazione nella pagina **Visualizza risultati** .

![Visualizza la pagina dei risultati](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Esportare i risultati della migrazione

1. Fare clic su **Esporta report** nella parte inferiore della pagina **Visualizza risultati** per salvare i risultati della migrazione in un file CSV.

2. Esaminare il file salvato per informazioni dettagliate sulla migrazione degli account di accesso, quindi verificare le modifiche.

## <a name="see-also"></a>Vedere anche

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: impostazioni di configurazione](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: procedure consigliate](../dma/dma-bestpractices.md)
