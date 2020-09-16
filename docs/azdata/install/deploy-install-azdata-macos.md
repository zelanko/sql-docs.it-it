---
title: Installare azdata per macOS
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data per macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6662a5ff7ced4c260e2b1a3fbd1efe5a285cf4a
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733869"
---
# <a name="install-azdata-on-macos"></a>Installare `azdata` in macOS

Per la piattaforma macOS, è possibile installare `azdata-cli` con la gestione pacchetti Homebrew. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di macOS seguenti: 
* 10.13 High Sierra
* 10.14 Mojave
* 10.15 Catalina

## <a name="install-with-homebrew"></a>Eseguire l'installazione con Homebrew

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli` prevede una dipendenza dai pacchetti di Homebrew `python3`, `freetds`, `unixodbc`, `zeromq`e li installerà. Per `azdata-cli` è garantita la compatibilità con l'ultima versione di queste dipendenze pubblicata in Homebrew.

## <a name="verify-install"></a>Verificare l'installazione

```bash
azdata
azdata --version
```

## <a name="update"></a>Aggiornamento

Aggiornare le informazioni del repository locale e quindi aggiornare il pacchetto `azdata-cli`.

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>Disinstallare

Usare Homebrew per disinstallare il pacchetto `azdata-cli`.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)