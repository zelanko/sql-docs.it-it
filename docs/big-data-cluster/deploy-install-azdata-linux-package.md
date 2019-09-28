---
title: Installare azdata con il programma di installazione in Linux
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (anteprima) con il programma di installazione (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2795178cb975ecb620528c4a5dc8715b70d447fd
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342011"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Installare `azdata` per gestire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare `azdata` per SQL Server i cluster di Big Data 2019 per la versione finale candidata in Linux. Prima che questi gestori di pacchetti fossero disponibili, è necessario installare `azdata` `pip`.

I gestori di pacchetti sono progettati per diversi sistemi operativi e distribuzioni.

- Per Linux (Ubuntu), [installare `azdata` con `apt`](#azdata-apt)

Al momento non sono disponibili gestori di pacchetti per installare `azdata` in altri sistemi operativi o distribuzioni. Per queste piattaforme, vedere [Install `azdata` without Package Manager](./deploy-install-azdata.md).

## <a id="linux"></a>Installare `azdata` per Linux

il pacchetto di installazione di `azdata` è disponibile per Ubuntu con `apt`.

### <a id="azdata-apt"></a>Installare `azdata` con APT (Ubuntu)

>[!NOTE]
>Il pacchetto `azdata` non usa Python di sistema, bensì installa il proprio interprete Python.

1. Ottenere i pacchetti necessari per il processo di installazione:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Scaricare e installare la chiave di firma:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. Aggiungere le informazioni sul repository `azdata`:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Aggiornare le informazioni sul repository e installare `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verificare l'installazione:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

Aggiorna solo `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Disinstallare

1. Disinstalla con apt-get remove:

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

Per ulteriori informazioni sui cluster Big Data, vedere [che cosa sono [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
