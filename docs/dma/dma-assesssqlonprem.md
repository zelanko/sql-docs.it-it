---
title: Eseguire una valutazione della migrazione di SQL ServerPerform a SQL Server migration assessment
titleSuffix: Data Migration Assistant
description: Informazioni su come usare Assistente migrazione dati per valutare un SQL Server locale prima della migrazione a un altro SQL ServeroSQL Server o al database SQL di Azure
ms.date: 01/15/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809747"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Eseguire una valutazione della migrazione di SQL Server con Data Migration Assistant

Le istruzioni dettagliate seguenti consentono di eseguire la prima valutazione per la migrazione a SQL Server locale, SQL Server in esecuzione in una macchina virtuale di Azure o un database SQL di Azure tramite Assistente migrazione dati.

   > [!NOTE]
   > Data Migration Assistant v5.0 introduce il supporto per l'analisi della connettività del database e delle query SQL incorporate nel codice dell'applicazione. Per ulteriori informazioni, vedere il post di blog Utilizzo di Assistente migrazione dati per valutare il livello di [accesso ai dati di un'applicazione.](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)

## <a name="create-an-assessment"></a>Creare una valutazione

1. Selezionare l'icona **Nuovo** (-) e quindi selezionare il tipo di progetto **Valutazione.**

2. Impostare il tipo di server di origine e destinazione.

    Se si sta aggiornando l'istanza di SQL Server locale a un'istanza di SQL Server locale moderna o a SQL Server ospitata in una macchina virtuale di Azure, impostare il tipo di server di origine e di destinazione su **SQL Server.** Se si esegue la migrazione al database SQL di Azure, impostare invece il tipo di server di destinazione su Database SQL di Azure.If you're migrating to Azure SQL Database, instead set the target server type to **Azure SQL Database**.

3. Fare clic su **Crea**.

   ![Creare una valutazione](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>Scegliere le opzioni di valutazione

1. Selezionare la versione di SQL Server di destinazione in cui si intende eseguire la migrazione.

2. Selezionare il tipo di report.

   Quando si valuta l'istanza di SQL Server di origine per la migrazione a SQL Server locale o a SQL Server ospitata in destinazioni di macchine virtuali di Azure, è possibile scegliere uno o entrambi i tipi di report di valutazione seguenti:When you're assessing your source SQL Server instance for migrating to on-premises SQL Server or to SQL Server hosted on Azure VM targets, you can choose one or both of the following assessment report types:

    - **Problemi di compatibilità**
    - **Raccomandazione delle nuove funzionalità**

   ![Selezionare un tipo di report di valutazione per la destinazione di SQL ServerSelect an assessment report type for SQL Server target](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Quando si valuta l'istanza di SQL Server di origine per la migrazione al database SQL di Azure, è possibile scegliere uno o entrambi i tipi di report di valutazione seguenti:When assessing your source SQL Server instance for migrating to Azure SQL Database, you can choose one or both of the following assessment report types:

    - **Check database compatibility (Verificare la compatibilità del database)**
    - **Check feature parity (Verificare la parità di funzionalità)**

    ![Selezionare il tipo di report di valutazione per la destinazione del database SQLSelect assessment report type for SQL Database target](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>Aggiungere database e traccia di eventi estesi per valutare

1. Selezionare **Aggiungi origini** per aprire il menu a comparsa della connessione.

2. Immettere il nome dell'istanza di SQL Server, scegliere il tipo di autenticazione, impostare le proprietà di connessione corrette e quindi selezionare **Connetti**.

3. Selezionare i database da valutare e quindi selezionare **Aggiungi**.

    > [!NOTE]
    > È possibile rimuovere più database selezionandoli tenendo premuto il tasto MAIUSC o CTRL e quindi facendo clic su **Rimuovi origini**. È inoltre possibile aggiungere database da più istanze di SQL Server selezionando **Aggiungi origini**.

4. Se si dispone di query SQL ad hoc o dinamiche o di qualsiasi istruzione DML avviata tramite il livello dati dell'applicazione, immettere il percorso della cartella in cui sono stati inseriti tutti i file di sessione degli eventi estesi raccolti per acquisire il carico di lavoro nell'origine SQL Server.

     Nell'esempio seguente viene illustrato come creare una sessione di eventi estesa nell'origine SQL ServerSQL Server per acquisire il carico di lavoro del livello dati dell'applicazione.  Acquisire il carico di lavoro per la durata che rappresenta il carico di lavoro di picco.

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. Fare clic su **Next** (Avanti) per avviare la valutazione.

    ![Aggiungere fonti e avviare la valutazione](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> È possibile eseguire più valutazioni contemporaneamente e visualizzarne lo stato aprendo la pagina **All Assessments** (Tutte le valutazioni).

## <a name="view-results"></a>Visualizzazione dei risultati

La durata della valutazione dipende dal numero di database aggiunti e dalle dimensioni dello schema di ogni database. I risultati vengono visualizzati per ogni database non appena sono disponibili.

1. Selezionare il database che ha completato la valutazione, quindi passare tra Problemi di **compatibilità** e **Consigli sulle funzionalità** utilizzando lo switcher.

2. Esaminare i problemi di compatibilità in tutti i livelli di compatibilità supportati dalla versione di SQL Server di destinazione selezionata nella pagina **Opzioni.**

È possibile esaminare i problemi di compatibilità analizzando l'oggetto interessato, i relativi dettagli e potenzialmente una correzione per ogni problema identificato in **Modifiche di rilievo**, Modifiche del **comportamento**e **Funzionalità deprecate**.

![Visualizzare i risultati della valutazione](../dma/media/dma-assesssqlonprem/review-results.png)

Analogamente, è possibile esaminare le raccomandazioni relative alle funzionalità nelle **aree Prestazioni**, **Archiviazione**e **Sicurezza** .

I suggerimenti sulle funzionalità riguardano diversi tipi di funzionalità, ad esempio OLTP in memoria, Columnstore, Stretch Database, Always Encrypted, Dynamic Data Masking e Transparent Data Encryption.

![Visualizzare i consigli sulle funzionalità](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Per il database SQL di Azure, le valutazioni forniscono problemi di blocco della migrazione e problemi di parità delle funzionalità.Esaminare i risultati per entrambe le categorie selezionando le opzioni specifiche.

- La categoria di parità delle funzionalità di **SQL Serversql Server** offre un set completo di consigli, approcci alternativi disponibili in Azure e passaggi di attenuazione. Consente di pianificare questo sforzo nei progetti di migrazione.

  ![Visualizzare le informazioni per la parità delle funzionalità di SQL ServerView information for SQL Server feature parity](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- La categoria Problemi di **compatibilità** fornisce funzionalità parzialmente supportate o non supportate che bloccano la migrazione dei database di SQL Server locali ai database SQL di Azure.The Compatibility issues category provides partially supported or unsupported features that block migrating on-premises SQL Server databases to Azure SQL databases.Fornisce quindi consigli per risolvere tali problemi.

  ![Visualizzare i problemi di compatibilità](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>Valutare un patrimonio di dati per la conformità al target

Se si desidera estendere ulteriormente queste valutazioni all'intero data estate e trovare la relativa disponibilità delle istanze e dei database di SQL Server per la migrazione al database SQL di Azure, caricare i risultati nell'hub azure Migrate selezionando **Carica in Azure Migrate**.

In questo modo è possibile visualizzare i risultati consolidati nel progetto hub di Azure Migrate.Doing so allows you to view the consolidated results on the Azure Migrate hub project.

Istruzioni dettagliate e dettagliate per le valutazioni della conformità degli obiettivi sono disponibili [qui](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017).

   ![Caricare i risultati in Azure MigrateUpload results to Azure Migrate](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>Esportare i risultati

Al termine della valutazione in tutti i database, selezionare **Esporta report** per esportare i risultati in un file JSON o in un file CSV. È quindi possibile analizzare i dati a proprio piacimento.

## <a name="save-and-load-assessments"></a>Salvare e caricare valutazioni

Oltre a esportare i risultati di una valutazione, è possibile salvare i dettagli della valutazione in un file e caricare un file di valutazione per una revisione successiva.  Per ulteriori informazioni, vedere l'articolo [Salvare e caricare le valutazioni con Assistente migrazione dati](../dma/dma-save-load-assessments.md).
