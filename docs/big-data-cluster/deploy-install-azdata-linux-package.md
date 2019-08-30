---
title: Installare azdata con il programma di installazione in Linux
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] la gestione (anteprima) con il programma di installazione (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160679"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Installare `azdata` per la [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] gestione in Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare `azdata` per la versione finale candidata di SQL Server 2019 di cluster Big data in Linux. Prima che questi gestori di pacchetti fossero disponibili, l' `azdata` installazione `pip`di richiedeva.

I gestori di pacchetti sono progettati per diversi sistemi operativi e distribuzioni.

- Per Linux (Ubuntu), [installare `azdata` con `apt` ](#azdata-apt)

Al momento non sono disponibili gestori di pacchetti da installare `azdata` in altri sistemi operativi o distribuzioni. Per queste piattaforme, vedere [install `azdata` without Package Manager](./deploy-install-azdata.md).

## <a id="linux"></a>Installare `azdata` per Linux

`azdata`il pacchetto di installazione è disponibile per `apt`Ubuntu con.

### <a id="azdata-apt"></a>Eseguire `azdata` l'installazione con APT (Ubuntu)

>[!NOTE]
>Il `azdata` pacchetto non usa Python di sistema, bensì installa il proprio interprete Python.

1. Ottenere i pacchetti necessari per il processo di installazione:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Scaricare e installare la chiave di firma:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. Aggiungere le `azdata` informazioni sul repository:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Aggiornare le informazioni sul repository `azdata`e installare:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verificare l'installazione:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Aggiorna

Solo `azdata` aggiornamento:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Disinstallare

1. Disinstalla con apt-get remove:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Rimuovere le `azdata` informazioni sul repository:

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

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
