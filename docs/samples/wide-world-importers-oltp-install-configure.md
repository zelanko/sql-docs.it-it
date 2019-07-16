---
title: Installare e configurare i database di esempio WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6fc303892fdefda350a2bb6513a71226264e50fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067668"
---
# <a name="installation-and-configuration"></a>Installazione e configurazione
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Le istruzioni sull'installazione e configurazione del database Wide World Importers OLTP.

## <a name="prerequisites"></a>Prerequisiti

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o versione successiva) oppure [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/). Per la versione completa dell'esempio, usare SQL Server Evaluation o Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere risultati ottimali usano la versione di giugno 2016 o versione successiva.

## <a name="download"></a>Scarica

La versione più recente dell'esempio:

[Wide world-importers-delle versioni](https://go.microsoft.com/fwlink/?LinkID=800630)

Scaricare l'esempio WideWorldImporters database backup/bacpac che corrisponde all'edizione di SQL Server o Database SQL di Azure.

Codice sorgente per ricreare il database di esempio è disponibile dal percorso seguente. Si noti che ricrea il codice di esempio genererà piccole differenze nei dati, poiché non esiste un fattore casuale la generazione di dati:

[world-wide-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

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
5. Sotto **le impostazioni del Database** cambiare il nome di database in *WideWorldImporters* e selezionare l'obiettivo di edizione e il servizio di destinazione da usare.
6. Fare clic su **successivo** e **fine** per avviare la distribuzione. Si verifica qualche minuto per essere completate in un P1. Se un piano tariffario inferiore livello desiderata, è consigliabile importare in un nuovo database P1 e quindi modificare il piano tariffario per il livello desiderato.

## <a name="configuration"></a>Configurazione

### <a name="full-text-indexing"></a>Indicizzazione full-text

Il database di esempio può sfruttare l'indicizzazione Full-Text. Tuttavia, tale funzionalità non è installata per impostazione predefinita con SQL Server, è necessario selezionarla durante l'installazione di SQL Server (è abilitata per impostazione predefinita nel database SQL di Azure). Pertanto, un passaggio di post-installazione è obbligatorio.

1. In SQL Server Management Studio, connettersi al database WideWorldImporters e aprire una nuova finestra query.
2. Eseguire il comando T-SQL seguente per abilitare l'utilizzo dell'indicizzazione Full-Text nel database:  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

Si applica a SQL Server

L'abilitazione del controllo in SQL Server richiede la configurazione del server. Per abilitare il controllo di SQL Server per l'esempio WideWorldImporters, eseguire l'istruzione seguente nel database:

    EXECUTE [Application].[Configuration_ApplyAuditing]

Nel Database SQL di Azure, controllo viene configurato tramite il [portale di Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Sicurezza a livello di riga

Si applica a Database SQL di Azure

Sicurezza a livello di riga non è abilitata per impostazione predefinita nel download del file bacpac di WideWorldImporters. Per abilitare la sicurezza a livello di riga nel database, eseguire la stored procedure seguente:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

