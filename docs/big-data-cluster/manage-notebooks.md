---
title: Gestire SQL Server cluster di Big data con Azure Data Studio notebook
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Usare un notebook di Azure Data Studio per gestire e risolvere problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313682"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Gestire SQL Server cluster di Big data con Azure Data Studio notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornisce un'estensione per Azure Data Studio contenente alcuni notebook. Un notebook fornisce la documentazione e il codice che è possibile usare in Azure Data Studio per gestire SQL Server cluster di Big Data 2019.

Originariamente implementato come progetto open source, i [notebook](notebooks-guidance.md) sono stati incorporati in [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare markdown per testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare notebook per distribuire cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Oltre ai notebook, è possibile visualizzare una raccolta di notebook, denominata Jupyter book. Un libro di Jupyter fornisce un sommario che consente di spostarsi in una raccolta di notebook in modo da trovare facilmente il notebook necessario, se si desidera risolvere i problemi SQL Server o visualizzare lo stato del cluster.

## <a name="prerequisites"></a>Prerequisiti

Questi prerequisiti sono necessari per aprire un notebook:

* La versione più recente di [Azure Data Studio Build Insider](https://aka.ms/azuredatastudio-rc)
* Estensione [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], installata in Azure Data Studio

Oltre a questi prerequisiti, per distribuire SQL Server cluster di 2019 Big data, è necessario anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>Accesso ai notebook per la risoluzione dei problemi
Sono disponibili tre modi per accedere ai notebook per la risoluzione dei problemi.

### <a name="command-palette"></a>Riquadro comandi
1. Selezionare **Visualizza** **riquadro dei comandi** > .
2. Immettere i libri **Jupyter: SQL Server 2019 guida @ no__t-0.

La documentazione di Jupyter viewlet con il libro Jupyter che contiene i notebook per la risoluzione dei problemi relativi a SQL Server cluster di Big Data si aprirà.

### <a name="sql-master-dashboard"></a>Dashboard master SQL
1. Dopo aver installato Azure Data Studio Insider, connettersi a un'istanza SQL Server Big Data clusters.
2. Dopo aver eseguito la connessione all'istanza di, fare clic con il pulsante destro del mouse sul nome del server in **connessioni** e scegliere **Gestisci**.
3. Nel Dashboard selezionare **SQL Server cluster di Big Data**. Selezionare **SQL Server guida 2019** per aprire il libro Jupyter che contiene i notebook necessari.
    @no__t notebook 0Jupyter nel dashboard @ no__t-1

1. Selezionare il notebook per l'attività che è necessario completare.

### <a name="controller-dashboard"></a>Dashboard del controller
1. Nella visualizzazione **connessioni** espandere **SQL Server cluster di Big Data**.
2. Aggiungere i dettagli dell'endpoint del controller.
3. Dopo aver eseguito la connessione al controller, fare clic con il pulsante destro del mouse sull'endpoint e scegliere **Gestisci**.
4. Al termine del caricamento del dashboard, selezionare **risoluzione dei** problemi per aprire le guide per la risoluzione dei problemi di Jupyter book.

## <a name="use-troubleshooting-notebooks"></a>Usare i notebook per la risoluzione dei problemi
1. Trovare la guida alla risoluzione dei problemi che è necessario nel sommario del libro Jupyter.
1. I notebook sono ottimizzati, quindi è sufficiente selezionare **Esegui celle**. Questa azione esegue singolarmente ogni cella del notebook fino al completamento del notebook.
1. Se viene rilevato un errore, il libro Jupyter suggerisce un notebook che è possibile eseguire per correggere l'errore. Attenersi alla procedura consigliata, quindi eseguire di nuovo il notebook.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook nella versione di anteprima di SQL Server 2019](notebooks-guidance.md).
