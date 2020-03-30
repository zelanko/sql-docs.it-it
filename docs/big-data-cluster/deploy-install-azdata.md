---
title: Installare il modulo azdata
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 40338c4083241fedd113bca3a1beb839dbdd3fca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75721714"
---
# <a name="install-azdata"></a>Installare `azdata`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata` è un'utilità da riga di comando scritta in Python per l'avvio e la gestione di cluster Big Data tramite le API REST. 

## <a name="find-latest-version"></a>Trovare l'ultima versione

L'elenco dei file per la versione più recente è sempre disponibile all'indirizzo [https://aka.ms/azdata](https://aka.ms/azdata).

Per individuare la versione installata e verificare se è necessario aggiornarla, eseguire `azdata --version`.

## <a name="os-specific-instructions"></a>Istruzioni specifiche del sistema operativo

* [Eseguire l'installazione in Windows](deploy-install-azdata-installer.md)
* [Eseguire l'installazione in macOS](deploy-install-azdata-macos.md)
* Eseguire l'installazione in Linux o nel [sottosistema Windows per Linux (WSL)](/windows/wsl/about/)
   * [Eseguire l'installazione con APT in Debian o Ubuntu](deploy-install-azdata-linux-package.md)
   * [Eseguire l'installazione con yum in RHEL o CentOS](deploy-install-azdata-yum.md)
   * [Eseguire l'installazione con Zypper in openSUSE o SLE](deploy-install-azdata-zypper.md)
   * [Eseguire l'installazione da script](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
