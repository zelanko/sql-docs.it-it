---
title: Creare una valutazione della migrazione SSIS con la Data Migration Assistant
description: Informazioni su come usare Data Migration Assistant per valutare un servizio di integrazione SQL Server locale (SSIS) prima di eseguire la migrazione al database SQL di Azure o a SQL di Azure Istanza gestita
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.custom: seo-lt-2019
ms.openlocfilehash: 9a7b077c3046b2f0c7e50b7ec20f68a5544e91e1
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2020
ms.locfileid: "87822196"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Eseguire una valutazione della migrazione di SQL Server Integration Services con Data Migration Assistant

## <a name="prerequisites"></a>Prerequisiti

Per valutare SQL Server pacchetti di Integration Services (SSIS), è necessario installare i componenti seguenti con Data Migration Assistant:

- SQL Server servizio di integrazione con la stessa versione dei pacchetti SSIS da valutare.
- Feature Pack di Azure o altri componenti di terze parti se i pacchetti SSIS da valutare hanno questi componenti.  

È necessario eseguire DMA con accesso **amministratore** per valutare i pacchetti SSIS nell'archivio pacchetti.

## <a name="performance-assessments"></a>Valutazioni delle prestazioni

Le istruzioni dettagliate seguenti consentono di eseguire la prima valutazione per la migrazione di pacchetti di SQL Server Integration Service (SSIS) nel database SQL di Azure o in Azure SQL Istanza gestita, usando Data Migration Assistant.

## <a name="create-an-assessment"></a>Creare una valutazione

1. Selezionare l'icona **nuovo** (+), quindi selezionare il tipo di progetto **Assessment** come **Integration Services**.

1. Impostare il tipo di server di origine e destinazione.

    Selezionare l'origine come **SQL Server**e impostare il tipo di server di destinazione come **database SQL di Azure** o **istanza gestita SQL di Azure**.

1. Fare clic su **Crea**.

    ![Crea valutazione](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>Connettersi a un server

1. Seguire l'opzione predefinita e fare clic su **Avanti** per **selezionare le origini**.
1. Immettere il nome dell'istanza di SQL Server, scegliere il tipo di autenticazione, impostare le proprietà di connessione corrette.
1. Opzionale Immettere un percorso di cartella contenente i pacchetti SSIS.
1. Opzionale Immettere la password di crittografia del pacchetto, se applicabile.
1. Fare clic su **Connetti** a SQL Server di origine.
  ![Aggiungi origine](media/dma-assess-ssis/dma-assess-ssis-addsource.png)

## <a name="add-sources-to-assess"></a>Aggiungere origini da valutare

1. Selezionare i tipi di archiviazione del pacchetto SSIS da valutare e quindi selezionare **Aggiungi**.
![Aggiungi origine](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png)
1. Selezionare **Aggiungi origini** per aprire il menu a comparsa connessione, se è necessario valutare più cartelle.
1. Fare clic su **Start Assessment** (Avvia valutazione).
  ![Avvia valutazione](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Visualizzazione dei risultati

La categoria problemi di compatibilità fornisce funzionalità parzialmente supportate o non supportate che bloccano la migrazione di pacchetti SSIS locali a Azure-SSIS Integration Runtime. Fornisce quindi consigli per risolvere tali problemi.

![Visualizzazione dei risultati](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Passaggi successivi

- [Panoramica della migrazione di carichi di lavoro SSIS locali a SSIS in ADF](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [Eseguire la migrazione di pacchetti di SQL Server Integration Services a un Istanza gestita SQL di Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Ridistribuire i pacchetti SQL Server Integration Services nel database SQL di Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
