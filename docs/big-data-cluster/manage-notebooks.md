---
title: Gestire SQL Server cluster Big Data con Azure Data Studio notebook
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Usare un notebook da Azure Data Studio per gestire e risolvere i problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8d87b09878539cccd40191d870bf97487579dca2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426401"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Gestire i cluster di Big Data per SQL Server con Azure Data Studio notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]fornisce un'estensione per Azure Data Studio che include i notebook per la distribuzione. Un notebook di distribuzione include documentazione e codice che è possibile usare in Azure Data Studio per gestire i cluster Big Data per SQL Server.

Originariamente implementato come progetto open source, i [notebook](notebooks-guidance.md) sono stati implementati in [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download). È possibile usare Markdown per il testo nelle celle di testo e uno dei kernel disponibili per scrivere codice nelle celle di codice.

È possibile usare i notebook per distribuire cluster di Big Data per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="prerequisites"></a>Prerequisiti

Per poter avviare il notebook sono necessari i prerequisiti seguenti:

* Versione più recente di [Azure Data Studio Build](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) Insider
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]estensione installata in Azure Data Studio

Oltre a quanto descritto in precedenza, la distribuzione di SQL Server 2019 Big Data cluster richiede anche:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)
