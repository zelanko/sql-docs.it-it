---
title: Installare e configurare il database di esempio WideWorldImporters
description: Seguire queste istruzioni per scaricare, installare e configurare il database di esempio WideWorldImporters con SQL Server Management Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 355eaa254fcc7bb6cd4aa9a39c2cbcb269d88396
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487070"
---
# <a name="installation-and-configuration"></a>Installazione e configurazione
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Istruzioni per l'installazione e la configurazione del database OLTP di Wide World Importers.

## <a name="prerequisites"></a>Prerequisiti

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o versione successiva) o Database SQL di [Azure.](https://azure.microsoft.com/services/sql-database/) Per la versione completa dell'esempio, usare SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere i migliori risultati, utilizzare la versione di giugno 2016 o successiva.

## <a name="download"></a>Download

L'ultima versione dell'esempio:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Scaricare l'esempio WideWorldImporters database backup/bacpac che corrisponde all'edizione di SQL Server sql Server o del database SQL di Azure.Download the sample WideWorldImporters database backup/bacpac that corresponds to your edition of SQL Server or Azure SQL Database.

Il codice sorgente per ricreare il database di esempio è disponibile dal percorso seguente. Si noti che la ricreazione dell'esempio comporterà lievi differenze nei dati, poiché esiste un fattore casuale nella generazione dei dati:Note that recreating the sample will result in slight differences in the data, since there is a random factor in the data generation:

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>Installazione


### <a name="sql-server"></a>SQL Server

To restore a backup to a SQL Server instance, you can use Management Studio.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic con il pulsante destro del mouse sul nodo **Database** e scegliere **Ripristina database**.
3. Selezionare **Dispositivo** e fare clic sul pulsante **...**
4. Nella finestra di dialogo **Selezione periferiche di backup**fare clic su **Aggiungi**, passare al backup del database nel file system del server e selezionare il backup. Fare clic su **OK**.
5. Se necessario, modificare il percorso di destinazione per i file di dati e di log nel riquadro **File.** Si noti che è consigliabile inserire i file di dati e di log in unità diverse.
6. Fare clic su **OK**. Verrà avviato il ripristino del database. Al termine, il database WideWorldImporters sarà installato nell'istanza di SQL Server.

### <a name="azure-sql-database"></a>database SQL di Azure

Per importare un bacpac in un nuovo database SQL, è possibile usare Management StudioManagement Studio.To import a bacpac into a new SQL Database, you can use Management StudioManagement Studio.

1. (opzionale) Se non si dispone ancora di UN SQL Server in Azure, passare al portale di [Azure](https://portal.azure.com/) e creare un nuovo database SQL. Nel processo di creazione di un database, si creerà un server. Prendere nota del server.
   - Vedere [questa esercitazione](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) per creare un database in pochi minutiSee this tutorial to create a database in minutes
2. Aprire SQL Server Management Studio e connettersi al server in Azure.Open SQL Server Management Studio and connect to your server in Azure.
3. Fare clic con il pulsante destro del mouse sul nodo **Database** e selezionare **Importa applicazione livello dati**.
4. In **Impostazioni di importazione** selezionare **Importa dal disco locale** e selezionare il bacpac del database di esempio dal file system.
5. In **Impostazioni database** modificare il nome del database in *WideWorldImporters* e selezionare l'edizione di destinazione e l'obiettivo del servizio da utilizzare.
6. Fare clic su **Avanti** e **Fine** per avviare la distribuzione. Sarà un paio di minuti per completare su un P1. Se si desidera un piano tariffario inferiore, è consigliabile eseguire l'importazione in un nuovo database P1 e quindi modificare il piano tariffario al livello desiderato.

## <a name="configuration"></a>Configurazione

### <a name="full-text-indexing"></a>Indicizzazione full-text

Il database di esempio può utilizzare l'indicizzazione di testo completo. Tuttavia, tale funzionalità non viene installata per impostazione predefinita con SQL Server: è necessario selezionarla durante l'installazione di SQL Server (è abilitata per impostazione predefinita nel database SQL di Azure). Pertanto, è necessaria una fase di post-installazione.

1. In SQL Server Management StudioSQL Server Management Studioconnettersi al database WideWorldImporters e aprire una nuova finestra di query.
2. Eseguire il comando T-SQL seguente per abilitare l'utilizzo dell'indicizzazione di testo completo nel database:`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

Si applica a: SQL Server

L'abilitazione del controllo in SQL ServerSQL Server richiede la configurazione del server. Per abilitare il controllo di SQL Server per l'esempio WideWorldImporters, eseguire l'istruzione seguente nel database:

    EXECUTE [Application].[Configuration_ApplyAuditing]

Nel database SQL di Azure il controllo viene configurato tramite il portale di [Azure.](https://portal.azure.com/)

### <a name="row-level-security"></a>Sicurezza a livello di riga

Si applica a: Database SQL di AzureApplies to: Azure SQL Database

La sicurezza a livello di riga non è abilitata per impostazione predefinita nel download bacpac di WideWorldImporters. Per abilitare la sicurezza a livello di riga nel database, eseguire la stored procedure seguente:To enable Row-Level Security in the database, run the following stored procedure:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

