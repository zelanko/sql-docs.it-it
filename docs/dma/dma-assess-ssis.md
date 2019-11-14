---
title: Creare una valutazione della migrazione SSIS con la Data Migration Assistant
description: Informazioni su come usare Data Migration Assistant per valutare un servizio di integrazione SQL Server locale (SSIS) prima di eseguire la migrazione al database SQL di Azure o istanza gestita di database SQL di Azure
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
ms.openlocfilehash: fa97cc647a194257441997032f2248a3ce9e5110
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056637"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Eseguire una valutazione della migrazione di SQL Server Integration Services con Data Migration Assistant

Le istruzioni dettagliate seguenti consentono di eseguire la prima valutazione per la migrazione di pacchetti di SQL Server Integration Service (SSIS) a un database SQL di Azure o a un'istanza gestita di database SQL di Azure, usando Data Migration Assistant.

## <a name="create-an-assessment"></a>Creare una valutazione

1. Selezionare l'icona **nuovo** (+), quindi selezionare il tipo di progetto **Assessment** come **Integration Services**.

1. Impostare il tipo di server di origine e di destinazione.

    Selezionare l'origine come **SQL Server**e impostare il tipo di server di destinazione come **database SQL** di Azure o **istanza gestita di database SQL di Azure**.

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
1. Fare clic su **Avvia valutazione**.
  ![Avvia valutazione](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Visualizzazione dei risultati

La categoria problemi di compatibilità fornisce funzionalità parzialmente supportate o non supportate che bloccano la migrazione di pacchetti SSIS locali a Azure-SSIS Integration Runtime. Fornisce quindi consigli per risolvere tali problemi.

![Visualizzazione dei risultati](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Passaggi successivi

- [Panoramica della migrazione di carichi di lavoro SSIS locali a SSIS in ADF](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [Eseguire la migrazione di pacchetti di SQL Server Integration Services a un'istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Ridistribuire i pacchetti SQL Server Integration Services nel database SQL di Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
