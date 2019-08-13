---
title: Gestire un cluster Big Data di SQL Server con notebook di Azure Data Studio
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Usare un notebook di Azure Data Studio per gestire e risolvere problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1a6156dad127ea2a86e8a6f4dfbdd6f692fd8f6e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893654"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gestire cluster Big Data di SQL Server con notebook di Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornisce un'estensione per Azure Data Studio contenente alcuni notebook. Un notebook include codice e documentazione che è possibile usare in Azure Data Studio per gestire cluster Big Data di SQL Server.

Originariamente implementati come progetto open source, i [notebook](notebooks-guidance.md) sono stati successivamente implementati in [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare markdown per testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare notebook per distribuire cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Oltre ai notebook, gli utenti possono visualizzare una raccolta di notebook, denominati libri Jupyter. Un Jupyter Book costituisce un sommario di riferimento per una raccolta di notebook, in modo che ogni utente possa trovare facilmente il notebook necessario, ad esempio per risolvere un problema relativo a SQL Server o per visualizzare lo stato di un cluster.

## <a name="prerequisites"></a>Prerequisiti

Per poter avviare il notebook è necessario soddisfare i prerequisiti seguenti:

* Versione più recente di [Build Insider per Azure Data Studio Insider](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* Estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] installata in Azure Data Studio

Oltre ai prerequisiti precedenti, la distribuzione di un cluster Big Data di SQL Server 2019 richiede anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>Accesso ai notebook per la risoluzione dei problemi

1. Dopo aver installato Insider per Azure Data Studio, connettersi a un'istanza del cluster Big Data di SQL Server.
2. Una volta stabilita la connessione, fare clic con il pulsante destro del mouse sul nome del server nel viewlet Connessioni e scegliere **Gestisci**.
3. Nel dashboard fare clic su **SQL Server Big Data Cluster** (Cluster Big Data di SQL Server). Fare clic su **SQL Server 2019 guide** (Guida a SQL Server 2019) per aprire Jupyter Book con i notebook necessari.
    ![pulsante](media/manage-notebooks/jupyter-book-button.png)

1. Nella finestra di selezione della cartella scegliere un percorso in cui salvare Jupyter Book.
2. Fare clic su **Ricarica** per ricaricare Azure Data Studio e visualizzare Jupyter Book. Fare clic su **Apri nuova istanza** per aprire una nuova istanza di Azure Data Studio con Jupyter Book.
3. Nella vista di esplorazione dovrebbe essere disponibile una sezione denominata **Books**. Se non è già espansa, fare clic sul nome della sezione per visualizzare i notebook.
4. Fare clic sul notebook relativo all'attività che è necessario completare.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook nella versione di anteprima di SQL Server 2019](notebooks-guidance.md).
