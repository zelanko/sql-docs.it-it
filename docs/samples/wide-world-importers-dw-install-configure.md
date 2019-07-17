---
title: Database di esempio WideWorldImporters OLAP - installare e configurare - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: ed3c5f1a4f2168196a651aea64c9c88311a197b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104249"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>Configurazione e installazione WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Istruzioni di installazione e configurazione per il database WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o versione successiva) oppure [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/). Per usare la versione completa dell'esempio, usare SQL Server Evaluation o Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere risultati ottimali usano la versione di giugno 2016 o versione successiva.

## <a name="download"></a>Scarica

La versione più recente dell'esempio:

[Wide world-importers-delle versioni](https://go.microsoft.com/fwlink/?LinkID=800630)

Scaricare l'esempio WideWorldImportersDW database backup/bacpac che corrisponde all'edizione di SQL Server o Database SQL di Azure.

Codice sorgente per ricreare il database di esempio è disponibile dal percorso seguente. Si noti che il popolamento dei dati si basa su ETL del database OLTP (WideWorldImporters):

[Wide world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Installazione


### <a name="sql-server"></a>SQL Server

Per ripristinare un backup in un'istanza di SQL Server, è possibile utilizzare Management Studio.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic sui **database** nodo e selezionare **Ripristina Database**.
3. Selezionare **periferica** e fare clic sul pulsante **...**
4. Nella finestra di dialogo **Seleziona dispositivi di backup**, fare clic su **Add**, passare al backup del database nel file System del server e selezionare il backup. Fare clic su **OK**.
5. Se necessario, modificare il percorso di destinazione per i dati e file di log, nelle **file** riquadro. Si noti che è buona norma inserire i dati di file e di log su unità differenti.
6. Fare clic su **OK**. Verrà avviata il ripristino di database. Al termine, si disporrà del database WideWorldImporters installato nell'istanza di SQL Server.

### <a name="azure-sql-database"></a>Database SQL di Azure

Per importare un file bacpac in un nuovo Database SQL, è possibile utilizzare Management Studio.

1. (facoltativo) Se non si dispone ancora un SQL Server in Azure, passare al [portale di Azure](https://portal.azure.com/) e creare un nuovo Database SQL. In quanto di creare un database, si creerà un server. Prendere nota del server.
   - Visualizzare [in questa esercitazione](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) per creare un database in pochi minuti
2. Aprire SQL Server Management Studio e connettersi al server in Azure.
3. Fare clic sui **database** nodo e selezionare **Importa applicazione livello dati**.
4. Nel **impostazioni di importazione** selezionate **Importa da disco locale** e selezionare il file bacpac del database di esempio dal file system.
5. Sotto **le impostazioni del Database** cambiare il nome di database in *WideWorldImportersDW* e selezionare l'obiettivo di edizione e il servizio di destinazione da usare.
6. Fare clic su **successivo** e **fine** per avviare la distribuzione. Questa operazione richiederà qualche minuto. Quando si specifica un obiettivo di servizio inferiore a S2 potrebbe richiedere più tempo.

## <a name="configuration"></a>Configurazione

[Si applica a SQL Server 2016 (e versioni successive) Developer o Evaluation o Enterprise Edition]

Il database di esempio può avvalersi di PolyBase per i file di query in Hadoop o Azure nell'archivio blob. Tuttavia, tale funzionalità non è installata per impostazione predefinita con SQL Server, è necessario selezionarla durante l'installazione di SQL Server. Pertanto, un passaggio di post-installazione è obbligatorio.

1. In SQL Server Management Studio, connettersi al database WideWorldImportersDW e aprire una nuova finestra query.
2. Eseguire il comando T-SQL seguente per abilitare l'uso di PolyBase nel database:

   ESEGUIRE [applicazioni]. [Configuration_ApplyPolyBase]
