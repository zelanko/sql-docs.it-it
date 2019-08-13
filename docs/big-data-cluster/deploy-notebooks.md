---
title: Distribuire un cluster Big Data di SQL Server con notebook di Azure Data Studio
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Usare un notebook di Azure Data Studio per distribuire un cluster Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb1da50fb84cbfd44aeab50a00be1c8433b3041e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892450"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Distribuire un cluster Big Data di SQL Server con notebook di Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornisce un'estensione per Azure Data Studio contenente notebook di distribuzione. Un notebook di distribuzione include codice e documentazione che è possibile usare in Azure Data Studio per creare un cluster Big Data di SQL Server.

Originariamente implementati come progetto open source, i [notebook](notebooks-guidance.md) sono stati successivamente implementati in [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare markdown per testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare notebook per distribuire cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerequisiti

Per poter avviare il notebook è necessario soddisfare i prerequisiti seguenti:

* Versione più recente di [Azure Data Studio Build](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) Insider installata
* Estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] installata in Azure Data Studio

Oltre ai prerequisiti precedenti, la distribuzione di un cluster Big Data di SQL Server 2019 richiede anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Avviare il notebook

1. Avviare il Azure Data Studio Insider.

1. Nella scheda **Connessioni** fare clic su... **...** e selezionare **Distribuire un cluster Big Data di SQL Server**.

   ![Intelligenza artificiale e Machine Learning](media/deploy-notebooks/deploy-notebooks-1.png)

1. In **Destinazione di distribuzione**, sotto la voce **Opzioni**, selezionare **New Azure Kubernetes Cluster** (Nuovo cluster Azure Kubernetes) oppure **Existing Azure Kubernetes Service cluster** (Cluster del servizio Azure Kubernetes esistente).

1. Fare clic sul pulsante **Seleziona** .

1. Questa azione avvia una finestra di dialogo per raccogliere l'input dell'utente, fornire le informazioni necessarie ed esaminare i valori predefiniti.

1. Fare clic sul pulsante **Apri Notebook** .
Questa azione avvia il notebook appropriato. Per completare la distribuzione, seguire le istruzioni nel notebook per distribuire un cluster Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in un cluster del servizio Azure Kubernetes nuovo o esistente.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla distribuzione, vedere le [linee guida per la distribuzione di cluster Big Data di SQL Server](deployment-guidance.md).
