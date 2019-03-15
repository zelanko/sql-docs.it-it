---
title: Eseguire una valutazione della migrazione di SQL Server (Data Migration Assistant) | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per valutare un SQL Server in locale prima della migrazione a un altro SQL Server o Database SQL di Azure
ms.custom: ''
ms.date: 03/12/2019
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
manager: craigg
ms.openlocfilehash: 2e7d75b1ef9e540802457cf63e7d2f59468941f9
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973860"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Eseguire una valutazione della migrazione di SQL Server con Data Migration Assistant

Le istruzioni dettagliate seguenti consentono di eseguire la prima valutazione per la migrazione di on-premises SQL Server, SQL Server in esecuzione in una macchina virtuale di Azure o Database SQL di Azure usando Data Migration Assistant.

## <a name="create-an-assessment"></a>Creare una valutazione

1.  Selezionare il **New** (+) icona e quindi selezionare la **Assessment** tipo di progetto.

2.  Impostare il tipo di server di origine e di destinazione.

    Se si sta aggiornando l'istanza di SQL Server locale a un'istanza di SQL Server moderno in locale o a SQL Server ospitato in una VM di Azure, impostare il tipo di server di origine e destinazione su **SQL Server**. Se si esegue la migrazione al Database SQL di Azure, invece impostare il tipo di server di destinazione **Database SQL di Azure**.

3.  Fare clic su **Crea**.

    ![Creare una valutazione](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Scegliere le opzioni di valutazione

1. Selezionare la versione di SQL Server di destinazione che si intende eseguire la migrazione a.

2. Selezionare il tipo di report.

   Quando si è verificata l'istanza di SQL Server di origine per la migrazione a SQL Server in locale o a SQL Server ospitati in destinazioni di macchina virtuale di Azure, è possibile scegliere uno o entrambi i tipi di report di valutazione seguenti:

    -   **Problemi di compatibilità**
    -   **Raccomandazione di nuove funzionalità**

    ![Selezionare un tipo di report di valutazione per la destinazione di SQL Server](../dma/media/AssessmentTypes.png)

   Quando viene verificata l'istanza di SQL Server di origine per la migrazione al Database SQL di Azure, è possibile scegliere uno o entrambi i tipi di report di valutazione seguenti:

    -   **Verificare la compatibilità del database**
    -   **Verifica parità delle funzionalità**

    ![Selezione tipo di report di valutazione per la destinazione di Database SQL](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Aggiungere i database per valutare

1.  Selezionare **Aggiungi origini** per aprire il menu a comparsa di connessione.

2.  Immettere il nome dell'istanza SQL server, scegliere il tipo di autenticazione, impostare le proprietà di connessione corretta e quindi selezionare **Connect**.

3.  Selezionare i database per valutare e quindi selezionare **Add**.

    > [!NOTE] 
    > È possibile rimuovere più database selezionandole mentre tenendo premuto il tasto MAIUSC o Ctrl e quindi scegliendo **rimuovere origini**. È anche possibile aggiungere database da più istanze di SQL Server usando il **Aggiungi origini** pulsante.

4.  Fare clic su **successivo** per avviare la valutazione.

    ![Aggiungere le origini e avviare una valutazione](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Visualizzare i risultati

La durata della valutazione dipende dal numero di database aggiunti e le dimensioni dello schema di ogni database. I risultati vengono visualizzati per ogni database, non appena risultano disponibili.

1.  Selezionare il database in cui è stata completata la valutazione e quindi passare da una **problemi di compatibilità** e **funzionalità consigliate** usando l'apposito controllo.

2.  Esaminare i problemi di compatibilità per tutti i livelli di compatibilità supportati dalla versione di SQL Server di destinazione selezionato nella **opzioni** pagina.

È possibile esaminare i problemi di compatibilità grazie all'analisi di oggetto interessato, i dettagli e potenzialmente una correzione per ogni problema individuato in **modifiche di rilievo**, **modifiche del comportamento**, e  **Funzionalità deprecate**.

![Visualizzare i risultati della valutazione](../dma/media/ReviewResults.png)

Allo stesso modo, è possibile esaminare l'indicazione di funzionalità tra **Performance**, **archiviazione**, e **sicurezza** aree.

Funzionalità consigliate coprono un'ampia gamma di funzionalità come OLTP In memoria, Columnstore, Stretch Database, Always Encrypted, Dynamic Data Masking e Transparent Data Encryption.

![Visualizzazione funzionalità consigliate](../dma/media/FeatureRecommendations.png)

Per il Database SQL di Azure, le valutazioni forniscono i problemi di blocco della migrazione e problemi di parità della funzionalità. Esaminare i risultati per entrambe le categorie selezionando le opzioni specifiche.

- Il **parità delle funzionalità di SQL Server** categoria offre un set completo di indicazioni, approcci alternativi disponibili in Azure e le procedure di mitigazione. Consente di pianificare questa attività nei progetti di migrazione.

  ![Visualizzare le informazioni di parità delle funzionalità di SQL Server](../dma/media/SQLFeatureParity.png)

- Il **problemi di compatibilità** categoria offre funzionalità parzialmente supportate o non supportata che bloccano la migrazione dei database di SQL Server in locale per database SQL di Azure. Quindi, fornisce indicazioni che consentono di risolvere tali problemi.

  ![Visualizza i problemi di compatibilità](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Esportare i risultati

Dopo che tutti i database completare la valutazione, selezionare **esportare report** per esportare i risultati in un file JSON o un file CSV. È quindi possibile analizzare i dati a seconda delle proprie esigenze.

È possibile eseguire più valutazioni contemporaneamente e visualizzare lo stato delle valutazioni, aprire il **tutte le valutazioni** pagina.
