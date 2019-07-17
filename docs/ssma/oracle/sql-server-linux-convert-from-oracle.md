---
title: Eseguire la migrazione dello Schema HR Oracle a SQL Server in Linux | Microsoft Docs
description: Convertire lo schema di esempio Oracle a SQL Server in Linux
author: shamikg
ms.author: shamikg
manager: shamikg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 1926c13b739de8294966fd6ce84df3d1e02a676e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266523"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Eseguire la migrazione di uno schema Oracle a SQL Server 2017 in Linux con SQL Server Migration Assistant

Questa esercitazione Usa SQL Server Migration Assistant (SSMA) per Oracle su Windows per convertire il codice di esempio di Oracle **HR** schema [SQL Server 2017 in Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Scaricare e installare SSMA in Windows
> * Creare un progetto di SSMA per la gestione della migrazione
> * Connettersi a Oracle
> * Eseguire un report di migrazione
> * Convertire lo schema delle risorse Umane di esempio
> * La migrazione dei dati

## <a name="prerequisites"></a>Prerequisiti

- Un'istanza di Oracle 12C (12.2.0.1.0) con i **HR** schema installato
- Un'istanza di lavoro di SQL Server in Linux

> [!NOTE]
> Gli stessi passaggi possono essere utilizzato per destinazione SQL Server in Windows, ma è necessario selezionare Windows nel **eseguire la migrazione a** impostazione del progetto.

## <a name="download-and-install-ssma-for-oracle"></a>Scaricare e installare SSMA per Oracle

Sono disponibili diverse edizioni di SQL Server Migration Assistant, a seconda del database di origine.  Scaricare la versione corrente di [SQL Server Migration Assistant per Oracle](https://aka.ms/ssmafororacle) e installarlo usando le istruzioni disponibili nella pagina di download.

> [!NOTE]
> A questo punto, il **SSMA per Oracle Extension Pack** non è supportato in Linux, ma non è necessario per questa esercitazione.

## <a name="create-and-set-up-project"></a>Creare e configurare project

Per creare un nuovo progetto SSMA, procedere come segue:

1. Aprire SSMA per Oracle e scegliere **nuovo progetto** dalle **File** menu.

1. Assegnare un nome al progetto.

1. Scegliere "SQL Server 2017 (Linux) - anteprima" nel **eseguire la migrazione a** campo.

SSMA per Oracle non usa gli schemi di esempio di Oracle per impostazione predefinita. Per abilitare lo schema HR, procedere come segue:

1. In SSMA, selezionare la **strumenti** menu.

1. Selezionare **impostazioni di progetto predefinite**, quindi scegliere **il caricamento di oggetti di sistema**.

1. Assicurarsi che **HR** sia selezionata e scegliere **OK**.

## <a name="connect-to-oracle"></a>Connettersi a Oracle

Successivamente, connettersi SSMA per Oracle.

1. Sulla barra degli strumenti, fare clic su **Connetti a Oracle**.

1. Immettere il nome del server, porta, il SID Oracle, nome utente e password.

   ![Connettersi a Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. quindi fare clic su **Connect**(Connetti). Dopo alcuni istanti, SSMA per Oracle si connette al database e legge i metadati.

## <a name="create-a-report"></a>Creare un report

Usare la procedura seguente per generare un report di migrazione.

1. Nel **Visualizzatore metadati Oracle**, espandere il nodo del server.

1. Espandere **schemi**, fare doppio clic su **HR**e selezionare **crea Report**.

   ![Visualizzatore metadati Oracle creazione di Report](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Una nuova finestra del browser si apre un report che elenca tutti gli avvisi e gli errori associati con la conversione.

   > [!NOTE]
   > Non è necessario eseguire un'operazione con tale elenco per questa esercitazione. Se si eseguono questi passaggi per il proprio database Oracle, è consigliabile esaminare il rapporto per risolvere eventuali problemi di conversione importante per il database.

   ![Report di migrazione di esempio](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Connessione a SQL Server

Scegliere quindi **Connetti al Server SQL** e immettere le informazioni di connessione appropriata.  Se si usa un nome di database che non è già esiste, lo crea automaticamente SSMA per Oracle.

![Connessione a SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Converti Schema

Fare clic su **HR** nelle **Visualizzatore metadati Oracle**e scegliere Converti Schema.

![Converti Schema](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Sincronizzare Database

Successivamente, eseguire la sincronizzazione del database.

1. Dopo il completamento della conversione, usare il **Visualizzatore metadati di SQL Server** per passare al database creato nel passaggio precedente.

1. Pulsante destro del mouse sul database, seleziona **Sincronizza con Database**, quindi fare clic su OK.

   ![Eseguire la sincronizzazione con Database](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>La migrazione dei dati

Il passaggio finale consiste nella migrazione dei dati.

1. Nel **Visualizzatore metadati Oracle**, fare clic su **HR**e selezionare **Migrate Data**.

1. Il passaggio di migrazione dei dati richiede che si nuovamente le credenziali Oracle e SQL Server.

1. Al termine, esaminare il rapporto sulla migrazione dei dati, che dovrebbe essere simile allo screenshot seguente:

   ![Report di migrazione dati](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Passaggi successivi

Per uno schema Orcale più complesso, il processo di conversione comporta più tempo, il test e individuare eventuali modifiche alle applicazioni client. Lo scopo di questa esercitazione è illustrare come è possibile usare SSMA per Oracle come parte del processo di migrazione globale.

In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Installare SSMA in Windows
> * Creare un nuovo progetto SSMA
> * Valutare ed eseguire una migrazione da Oracle

Successivamente, esplorare altre modalità d'uso di SSMA:

> [!div class="nextstepaction"]
>[Documentazione di SQL Server Migration Assistant](../sql-server-migration-assistant.md)
