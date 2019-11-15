---
title: Gestire cluster Big Data di SQL Server con notebook di Azure Data Studio
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Usare un notebook di Azure Data Studio per gestire e risolvere problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 860524daa5e6ab2db17fdf95cf5aa785aeb4fdf7
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844294"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Gestire cluster Big Data di SQL Server con notebook di Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornisce un'estensione per Azure Data Studio contenente alcuni notebook. Un notebook fornisce codice e documentazione che è possibile usare in Azure Data Studio per gestire cluster Big Data di SQL Server 2019.

Originariamente implementati come progetto open source, i [notebook](notebooks-guidance.md) sono stati successivamente integrati in [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare markdown per testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare notebook per distribuire cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Oltre ai notebook, è possibile visualizzare anche una raccolta di notebook, denominata Jupyter Book. Un Jupyter Book costituisce un sommario per la consultazione di una raccolta di notebook, in modo da poter trovare facilmente il notebook necessario, ad esempio per risolvere un problema relativo a SQL Server o per visualizzare lo stato di un cluster.

## <a name="prerequisites"></a>Prerequisites

Per l'apertura di un notebook sono necessari i prerequisiti seguenti:

* La versione più recente di [Azure Data Studio (build Insiders)](https://aka.ms/azuredatastudio-rc)
* L'estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], installata in Azure Data Studio

Oltre a questi prerequisiti, per distribuire cluster Big Data di SQL Server 2019, sono necessari anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Accedere ai notebook per la risoluzione dei problemi
Sono disponibili tre modi per accedere ai notebook per la risoluzione dei problemi.

### <a name="command-palette"></a>Riquadro comandi
1. Selezionare **Visualizza** > **Riquadro comandi**.
2. Immettere **Jupyter Books: SQL Server 2019 Guide**.

Si aprirà il viewlet dei Jupyter Book con il Book contenente il notebook per la risoluzione dei problemi relativi ai cluster Big Data di SQL Server.

### <a name="sql-master-dashboard"></a>Dashboard master di SQL
1. Dopo aver installato Azure Data Studio Insiders, connettersi all'istanza di un cluster Big Data di SQL Server.
2. Dopo aver eseguito la connessione all'istanza, fare clic con il pulsante destro del mouse sul nome del server in **CONNESSIONI** e selezionare **Gestisci**.
3. Nel dashboard selezionare **SQL Server Big Data Cluster** (Cluster Big Data di SQL Server). Selezionare **SQL Server 2019 guide** (Guida a SQL Server 2019) per aprire il Jupyter Book contenente i notebook necessari.
    ![Notebook Jupyter nel dashboard](media/manage-notebooks/jupyter-book-button.png)

1. Selezionare il notebook relativo all'attività da completare.

### <a name="controller-dashboard"></a>Dashboard del controller
1. Nella visualizzazione **Connessioni** espandere **SQL Server Big Data Clusters** (Cluster Big Data per SQL Server).
2. Aggiungere i dettagli dell'endpoint del controller.
3. Dopo aver eseguito la connessione al controller, fare clic con il pulsante destro del mouse sull'endpoint e selezionare **Gestisci**.
4. Al termine del caricamento del dashboard, selezionare **Risoluzione problemi** per aprire le guide alla risoluzione dei problemi del Jupyter Book.

## <a name="use-troubleshooting-notebooks"></a>Usare i notebook per la risoluzione dei problemi
1. Nel sommario del Jupyter Book trovare la guida alla risoluzione dei problemi necessaria.
1. I notebook sono ottimizzati, pertanto è sufficiente selezionare **Run Cells** (Esegui celle). Questa azione esegue singolarmente ogni cella del notebook fino al suo completamento.
1. Se viene rilevato un errore, il Jupyter Book suggerisce un notebook che è possibile eseguire per correggere l'errore. Seguire la procedura consigliata ed eseguire nuovamente il notebook.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook in SQL Server](notebooks-guidance.md).
