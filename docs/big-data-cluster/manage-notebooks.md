---
title: Gestire un cluster Big Data di SQL Server con notebook di Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Usare un notebook di Azure Data Studio per gestire e risolvere problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846652"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gestire cluster Big Data di SQL Server con notebook di Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornisce un'estensione per Azure Data Studio contenente alcuni notebook. Un notebook include codice e documentazione che è possibile usare in Azure Data Studio per gestire cluster Big Data di SQL Server.

Originariamente implementati come progetto open source, i [notebook](notebooks-guidance.md) sono stati successivamente implementati in [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare markdown per testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare notebook per distribuire cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Oltre ai notebook, gli utenti possono visualizzare una raccolta di notebook, denominati libri Jupyter. Un Jupyter Book costituisce un sommario di riferimento per una raccolta di notebook, in modo che ogni utente possa trovare facilmente il notebook necessario, ad esempio per risolvere un problema relativo a SQL Server o per visualizzare lo stato di un cluster.

## <a name="prerequisites"></a>Prerequisiti

Per poter avviare il notebook è necessario soddisfare i prerequisiti seguenti:

* Versione più recente di [Build Insider per Azure Data Studio Insider](https://aka.ms/azuredatastudio-rc)
* Estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] installata in Azure Data Studio

Oltre ai prerequisiti precedenti, la distribuzione di un cluster Big Data di SQL Server 2019 richiede anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Accesso ai notebook per la risoluzione dei problemi
Sono disponibili tre modi per accedere ai notebook per la risoluzione dei problemi.

### <a name="command-palette"></a>Riquadro comandi
1. Fare clic su **Visualizza** e quindi su **tavolozza comandi**
2. Digitare "Jupyter Books: Guida SQL Server 2019 "
3. In questo modo si apriranno i libri Jupyter viewlet con il libro Jupyter che contiene i dati del STG correlati a SQL Server cluster di Big Data.

### <a name="sql-master-dashboard"></a>Dashboard master SQL
1. Dopo aver installato Insider per Azure Data Studio, connettersi a un'istanza del cluster Big Data di SQL Server.
2. Una volta stabilita la connessione, fare clic con il pulsante destro del mouse sul nome del server nel viewlet Connessioni e scegliere **Gestisci**.
3. Nel dashboard fare clic su **SQL Server Big Data Cluster** (Cluster Big Data di SQL Server). Fare clic su **SQL Server 2019 guide** (Guida a SQL Server 2019) per aprire Jupyter Book con i notebook necessari.
    ![button](media/manage-notebooks/jupyter-book-button.png)

1. Verrà aperta la documentazione di Jupyter viewlet con il libro STG Jupyter già aperto.
4. Fare clic sul notebook relativo all'attività che è necessario completare.

### <a name="controller-dashboard"></a>Dashboard del controller
1. Nella visualizzazione **connessioni** espandere **SQL Server cluster di Big Data.**
2. Aggiungere i dettagli dell'endpoint del controller.
3. Dopo aver completato la connessione al controller, fare clic con il pulsante destro del mouse sull'endpoint e scegliere **Gestisci.**
4. Al termine del caricamento del dashboard, fare clic su risoluzione dei problemi per avviare il libro Jupyter STG.

## <a name="how-to-use-troubleshooting-notebooks"></a>Come usare i notebook per la risoluzione dei problemi
1. Esaminare il sommario del libro Jupyter esistente fino a trovare il STG necessario.
1. Tutti i notebook sono ottimizzati quando l'utente deve solo fare clic su **Esegui celle.** Ogni cella del notebook verrà eseguita singolarmente fino al completamento.
1. Se viene eseguito un errore, il libro Jupyter suggerisce un notebook che è possibile eseguire per correggere l'errore. Seguire i passaggi, quindi eseguire di nuovo il notebook.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook nella versione di anteprima di SQL Server 2019](notebooks-guidance.md).
