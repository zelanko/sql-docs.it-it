---
title: Installare & configurare il database di esempio DW WideWorldImportersInstall to configure DW WideWorldImporters sample database
description: Seguire queste istruzioni per scaricare, installare e configurare il database di esempio WideWorldImportersDW con SQL Server Management Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488548"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>Installazione e configurazione di WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Istruzioni di installazione e configurazione per il database WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o versione successiva) o Database SQL di [Azure.](https://azure.microsoft.com/services/sql-database/) Per utilizzare la versione completa dell'esempio, utilizzare SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere i migliori risultati, utilizzare la versione di giugno 2016 o successiva.

## <a name="download"></a>Download

L'ultima versione dell'esempio:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Scaricare l'esempio WideWorldImportersDW database backup/bacpac che corrisponde all'edizione di SQL Server o del database SQL di Azure.Download the sample WideWorldImportersDW database backup/bacpac that corresponds to your edition of SQL Server or Azure SQL Database.

Il codice sorgente per ricreare il database di esempio è disponibile dal percorso seguente. Si noti che il popolamento dei dati è basato su ETL dal database OLTP (WideWorldImporters):

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

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
5. In **Impostazioni database** modificare il nome del database in *WideWorldImportersDW* e selezionare l'edizione di destinazione e l'obiettivo del servizio da utilizzare.
6. Fare clic su **Avanti** e **Fine** per avviare la distribuzione. Questa operazione richiederà qualche minuto. Quando si specifica un obiettivo di servizio inferiore a S2, potrebbe essere necessario più tempo.

## <a name="configuration"></a>Configurazione

[Si applica a SQL Server 2016 (e versioni successive) Developer/Evaluation/Enterprise Edition]

Il database di esempio può usare PolyBase per eseguire query sui file nell'archiviazione BLOB di Hadoop o Azure.The sample database can make use of PolyBase to query files in Hadoop or Azure blob storage. Tuttavia, tale funzionalità non viene installata per impostazione predefinita con SQL ServerSQL Server: è necessario selezionarla durante l'installazione di SQL ServerSQL Server . Pertanto, è necessaria una fase di post-installazione.

1. In SQL Server Management StudioCONNETTERsi al database WideWorldImportersDW e aprire una nuova finestra di query.
2. Eseguire il comando T-SQL seguente per abilitare l'utilizzo di PolyBase nel database:

   EXECUTE [Applicazione]. [Configuration_ApplyPolyBase]
