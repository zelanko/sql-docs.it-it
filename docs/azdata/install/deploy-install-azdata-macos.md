---
title: Installare Azure Data CLI (azdata) per macOS
titleSuffix: ''
description: Informazioni su come installare lo strumento Azure Data CLI (azdata) in macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0e3d7217ef917c794f1c497f7c5548588c2da1ba
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257381"
---
# <a name="install-azure-data-cli-azdata-on-macos"></a>Installare [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] in macOS

Per la piattaforma macOS, è possibile installare `azdata-cli` con la gestione pacchetti Homebrew. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di macOS seguenti:

- 10.13 High Sierra
- 10.14 Mojave
- 10.15 Catalina

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

Usare azdata con i [servizi dati con abilitazione di Azure Arc](/azure/azure-arc/data/)
