---
title: Valutare l'idoneità di un tuoi dati di SQL Server la migrazione al Database SQL di Azure | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per eseguire la migrazione di un tuoi dati di SQL Server per la migrazione al Database SQL di Azure
ms.custom: ''
ms.date: 07/16/2019
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
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269383"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Valutare l'idoneità di un tuoi dati di SQL Server la migrazione al Database SQL di Azure con Data Migration Assistant

La migrazione di centinaia di istanze di SQL Server e migliaia di database al Database SQL di Azure, l'offerta di piattaforma come servizio (PaaS), è un'attività una notevole. Per semplificare il processo quanto più possibile, è necessario avere la ragionevole certezza sulla conformità dei relative per la migrazione. Identificazione ristretta, tra cui il server e database che sono pronti o che richiedono uno sforzo minimo per preparare la migrazione, semplifica e accelera l'impegno.

Questo articolo vengono fornite istruzioni dettagliate per sfruttare il [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) per riepilogare i risultati di conformità ed esporli nel [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) hub.

## <a name="create-a-project-and-add-a-tool"></a>Creare un progetto e aggiungere uno strumento

Configurare un nuovo progetto Azure Migrate in una sottoscrizione di Azure e quindi aggiungere uno strumento.

Consente di archiviare il rilevamento, valutazione e migrazione i metadati raccolti dall'ambiente si è verificata o la migrazione di un progetto Azure Migrate. È anche possibile usare un progetto per tenere traccia delle risorse individuate e per orchestrare la valutazione e la migrazione.

1. Accedere al portale di Azure, selezionare **tutti i servizi**e quindi cercare Azure Migrate.
2. Sotto **Services**, selezionare **Azure Migrate**.

   ![Azure Migrate - Seleziona servizio](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. Nel **Overview** pagina, selezionare **valutazione e la migrazione dei database**.

   ![Azure Migrate - avvio della valutazione](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. Nelle **database**, in **introduttiva**, selezionare **aggiungere altri strumenti**.

   ![Azure Migrate - Aggiungi strumenti](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. Nel **progetto di migrazione** scheda, selezionare il gruppo di risorse e sottoscrizione di Azure (se non si ha già una risorsa gruppo, crearne uno).
6. Sotto **dettagli progetto**, specificare il nome del progetto e l'area geografica in cui si desidera creare il progetto.

    ![Azure Migrate - aggiungere una finestra di dialogo dello strumento](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    È possibile creare un progetto Azure Migrate in una qualsiasi di queste aree geografiche.

    | **Area geografica**  | **Area del percorso di archiviazione** |
    | ------------- | ------------- |
    | Asia | Asia sud-orientale o Asia orientale |
    | Europa | Europa meridionale o Europa occidentale |
    | Regno Unito | Regno Unito meridionale e Regno Unito occidentale |
    | Stati Uniti | Stati Uniti centrali o Stati Uniti occidentali 2 |

    L'area geografica specificata per il progetto viene usato solo per archiviare i metadati raccolti dalle macchine virtuali in locale. È possibile selezionare qualsiasi area di destinazione per la migrazione effettiva.

7. Selezionare **successivo**e quindi aggiungere uno strumento di valutazione.

   > [!NOTE]
   > Quando si crea un progetto, è necessario aggiungere almeno uno strumento di valutazione o la migrazione.

8. Nel **lo strumento di valutazione Select** scheda, **Azure Migrate: Valutazione del database** viene visualizzato come lo strumento di valutazione da aggiungere. Se non è attualmente necessario uno strumento di valutazione, selezionare la **ignorare l'aggiunta di uno strumento di valutazione per il momento** casella di controllo. Selezionare **Avanti**.

    ![Azure Migrate - scheda dello strumento di valutazione della selezione](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. Nel **lo strumento di migrazione selezionare** scheda, **Azure Migrate: Migrazione di un database** viene visualizzato come lo strumento di migrazione da aggiungere. Se non è attualmente necessario uno strumento di migrazione, selezionare la **ignorare l'aggiunta di uno strumento di migrazione per il momento**. Selezionare **Avanti**.

    ![Azure Migrate - scheda degli strumenti di migrazione selezionare](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. In **rivedere e aggiungere gli strumenti**, esaminare le impostazioni e quindi selezionare **aggiungere gli strumenti**.

    ![Azure Migrate - revisione + Aggiungi scheda altri strumenti](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    Dopo aver creato il progetto, è possibile selezionare altri strumenti per la valutazione e migrazione di server e carichi di lavoro, i database e le app web.

## <a name="assess-and-upload-assessment-results"></a>Valutare e caricare i risultati della valutazione

Dopo aver creato correttamente un progetto di migrazione, sotto **strumenti di valutazione**, nella **Azure Migrate: Valutazione del database** finestra, le istruzioni per scaricare e utilizzare la visualizzazione dello strumento Data Migration Assistant.

   ![Azure Migrate - strumento di valutazione aggiunto](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Scarica Data Migration Assistant usando il collegamento fornito e quindi installarlo in un computer con accesso alle istanze di SQL Server di origine.
2. Avviare Data Migration Assistant.

### <a name="create-an-assessment"></a>Creare una valutazione

1. A sinistra, selezionare la **+** icona e quindi selezionare la valutazione **tipo di progetto**
2. Specificare il nome del progetto e quindi selezionare il server di origine e i tipi di server di destinazione.

    Se si sta aggiornando l'istanza di SQL Server locale a una versione successiva di SQL Server o a SQL Server ospitato in una VM di Azure, impostare il tipo di server di origine e destinazione su **SQL Server**. Il tipo di server di destinazione impostato su **istanza gestita di Azure SQL Database** per una valutazione della conformità di destinazione di Database SQL di Azure (PaaS).

3. Selezionare **Create**.

   ![Azure Migrate - interfaccia Data Migration Assistant](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>Scegliere le opzioni di valutazione

1. Selezionare il tipo di report.

    È possibile scegliere uno o entrambi i tipi di report seguenti:
    * Verificare la compatibilità del database
    * Verifica parità delle funzionalità

   ![Schermata Opzioni di Azure Migrate - Data Migration Assistant - valutazione](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. Selezionare **Avanti**.

### <a name="add-databases-to-assess"></a>Aggiungere i database per valutare

1. Selezionare **Aggiungi origini** per aprire il riquadro a comparsa connessione con menu di scelta.
2. Immettere il nome dell'istanza SQL server, scegliere il tipo di autenticazione, impostare le proprietà di connessione corretta e quindi selezionare **Connect**.
3. Selezionare i database per valutare e quindi selezionare **Add**.

   > [!NOTE]
   > È possibile rimuovere più database selezionandole, tenendo premuto il tasto MAIUSC o Ctrl e quindi facendo clic su Rimuovi origini. È anche possibile aggiungere database da più istanze di SQL Server con il pulsante Aggiungi origini.

4. Selezionare **successivo** per avviare la valutazione.

   ![Schermata di selezione delle origini di Azure Migrate - Data Migration Assistant-](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. Dopo aver completato la valutazione, selezionare **caricare in Azure Migrate**.

   ![Schermata di Azure Migrate - Data Migration Assistant - verifica dei risultati](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Accedere al portale di Azure.

   ![Schermata di Azure Migrate - Data Migration Assistant - verifica dei risultati](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. Selezionare la sottoscrizione e il progetto Azure Migrate in cui si desidera caricare i risultati della valutazione e quindi selezionare **caricare**.

   Attendere la conferma di caricamento della valutazione.

## <a name="view-target-readiness-assessment-results"></a>Risultati della valutazione di conformità destinazione di visualizzazione

1. Accesso nel portale di Azure, ricerca di Azure migrate e quindi selezionare **Azure Migrate**.

   ![Ricerca di Azure Migrate - portale di Azure - servizio](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. Selezionare **fase di valutazione e la migrazione dei database** per ottenere i risultati della valutazione.

   ![Azure Migrate - risultati della valutazione di revisione](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    È possibile visualizzare il riepilogo dello stato di preparazione di SQL Server, assicurarsi che si usa il progetto di migrazione appropriato, in caso contrario, usare modificare l'opzione per selezionare un progetto di migrazione diverso.

    Progetto eseguire la migrazione di ogni volta che si aggiornano i risultati della valutazione in Azure, Azure migrate hub consolidare tutti i risultati e fornire il report di riepilogo.  È possibile eseguire più valutazioni Data Migration Assistant in parallelo e caricare i risultati per il progetto di migrazione singolo per ottenere il rapporto conformità consolidati.

   ![Azure Migrate - risultati della verifica conformità](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **Valutare le istanze del database**:  Il numero di istanze di SQL Server valutati finora.
    **Database valutati**: Numero totale di database valutato tra uno o più istanze di SQL Server valutate **database pronto per il database SQL**:  Numero di database pronto per eseguire la migrazione al Database SQL di Azure (PaaS).
    **Database pronto per la macchina virtuale di SQL Azure**:  Numero di database sono costituiti da uno o più blocchi di migrazione al Database SQL di Azure (PaaS), ma pronti per eseguire la migrazione di SQL Server nelle VM di Azure.

3. Selezionare **valutato le istanze del database** per accedere alla visualizzazione a livello di istanza SQL Server.

   ![Azure Migrate - revisione istanza readiness](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    È possibile trovare lo stato di idoneità percentuale di ogni istanza di SQL Server, eseguire la migrazione al Database SQL di Azure (PaaS).

4. Selezionare un'istanza specifica per ottenere la visualizzazione dello stato di preparazione del database.

   ![Azure Migrate - revisione dello stato di preparazione del database](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    È possibile visualizzare il numero di blocchi di migrazione per ogni database, la destinazione consigliata per ciascun database nella vista precedente.

5. Esaminare i risultati della valutazione DMA per ottenere altri dettagli sui blocchi di migrazione.

   ![Azure Migrate - blocchi migrazione revisione](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>Vedere anche

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: Impostazioni di configurazione](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: Le procedure consigliate](../dma/dma-bestpractices.md)
