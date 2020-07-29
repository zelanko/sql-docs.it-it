---
title: Installare azdata con il programma di installazione in Linux
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data di SQL Server con il programma di installazione (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 304515dcd288978c0d85ab992312eb2444430bfc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773646"
---
# <a name="install-azdata-with-apt"></a>Installare `azdata` con apt

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come installare `azdata` per i cluster Big Data di SQL Server 2019 in Linux. Prima che questi strumenti di gestione pacchetti fossero disponibili, l'installazione di `azdata` richiedeva `pip`.

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>Installare `azdata` per Linux

Il pacchetto di installazione di `azdata` è disponibile per Ubuntu con `apt`.

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>Installare `azdata` con apt (Ubuntu)

>[!NOTE]
>Il pacchetto `azdata` non usa l'interprete Python di sistema, ma ne installa uno proprio.

1. Ottenere i pacchetti necessari per il processo di installazione:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. Scaricare e installare la chiave di firma:

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. Aggiungere le informazioni del repository `azdata`.

   Per client Ubuntu 16.04 eseguire:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

   Per client Ubuntu 18.04 eseguire:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
    ```

4. Aggiornare le informazioni del repository e installare `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verificare l'installazione:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Aggiornamento

Aggiornare solo `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Disinstallare

1. Disinstallare con apt-get remove:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Rimuovere le informazioni del repository `azdata`:

    >[!NOTE]
    >Questo passaggio non è necessario se si prevede di installare `azdata` in futuro

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. Rimuovere la chiave di firma:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Rimuovere tutte le dipendenze non necessarie installate con l'interfaccia della riga di comando di Azdata:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
