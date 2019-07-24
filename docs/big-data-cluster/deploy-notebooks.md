---
title: Distribuire SQL Server cluster Big Data con Azure Data Studio notebook
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Usare un notebook da Azure Data Studio per distribuire un cluster di Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f12a4f06ceb1c3a48b2b2fc661c59594e6d6cce3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426421"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Distribuire SQL Server cluster Big Data con Azure Data Studio notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]fornisce un'estensione per Azure Data Studio che include i notebook per la distribuzione. Un notebook di distribuzione include documentazione e codice che è possibile usare in Azure Data Studio per creare un cluster Big Data SQL Server. 

Originariamente implementato come progetto open source, i [notebook](notebooks-guidance.md) sono stati implementati in [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare Markdown per il testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare i notebook per distribuire cluster di Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerequisiti
Per poter avviare il notebook sono necessari i prerequisiti seguenti:

* [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) installata la versione più recente di
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]estensione installata in Azure Data Studio

Oltre a quanto descritto in precedenza, la distribuzione di SQL Server 2019 Big Data cluster richiede anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Avviare il notebook

1. Installare e avviare la [compilazione Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)Insider.
1.  Nella scheda **connessioni** fare clic su **...** e selezionare **Distribuisci SQL Server Big Data cluster...** .

   ![Intelligenza artificiale e ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. Dalla **destinazione di distribuzione**, in **Opzioni**Selezionare **nuovo cluster di Azure Kubernetes** o **cluster di servizi Kubernetes di Azure esistente**.
1. Selezionare **Apri Notebook**.

Questa azione avvia il notebook appropriato. Per completare la distribuzione, seguire le istruzioni nel notebook per distribuire un cluster di Big data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in un cluster del servizio Azure Kubernetes nuovo o esistente.
