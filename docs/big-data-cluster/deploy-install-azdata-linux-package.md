---
title: Installare azdata con il programma di installazione in Linux
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data di SQL Server con il programma di installazione (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532067"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Installare `azdata` per gestire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare `azdata` per i cluster Big Data di SQL Server 2019 in Linux. Prima che questi strumenti di gestione pacchetti fossero disponibili, l'installazione di `azdata` richiedeva `pip`.

Gli strumenti di gestione pacchetti sono progettati per diversi sistemi operativi e diverse distribuzioni.

- Per Windows e Linux (distribuzione Ubuntu), è possibile semplificare l'esperienza di installazione con uno strumento di [gestione pacchetti](./deploy-install-azdata-installer.md).
- Per Linux (Ubuntu), [installare `azdata` con `apt`](#azdata-apt)

Non sono attualmente disponibili strumenti di gestione pacchetti per installare `azdata` in altri sistemi operativi o altre distribuzioni. Per queste piattaforme, vedere [Installare `azdata` senza strumenti di gestione pacchetti](./deploy-install-azdata.md).

## <a id="linux"></a>Installare `azdata` per Linux

Il pacchetto di installazione di `azdata` è disponibile per Ubuntu con `apt`.

### <a id="azdata-apt"></a>Installare `azdata` con apt (Ubuntu)

>[!NOTE]
>Il pacchetto `azdata` non usa l'interprete Python di sistema, ma ne installa uno proprio.

1. Ottenere i pacchetti necessari per il processo di installazione:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Scaricare e installare la chiave di firma:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. Aggiungere le informazioni del repository `azdata`:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
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

### <a name="update"></a>Update

Aggiornare solo `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

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
