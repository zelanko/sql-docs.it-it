---
title: Installare Azure Data CLI (azdata) con apt
description: Informazioni su come installare lo strumento Azure Data CLI (azdata) con apt.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4508db56c0246f181f9244fe0a3b853a3e91eb24
ms.sourcegitcommit: 4b7ecc080795c5f90322d60df5c0550884f48140
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2020
ms.locfileid: "94334450"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>Installare [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con apt

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Per le distribuzioni Linux con `apt` è disponibile un pacchetto per `azdata-cli`. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di Linux che usano `apt`:

- Ubuntu 16.04, Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>Eseguire l'installazione con APT

>[!IMPORTANT]
> Il pacchetto RPM di `azdata-cli` dipende dal pacchetto python3. Nel sistema potrebbe trattarsi di una versione di Python che risale a una data precedente al requisito di *Python 3.6.x*. Se questa situazione costituisce un problema, trovare un pacchetto python3 sostitutivo o seguire le istruzioni per l'installazione manuale che usano [`pip`](../install/deploy-install-azdata-pip.md).

1. Installare le dipendenze necessarie per l'installazione di `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. Importare la chiave del repository Microsoft.

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. Creare le informazioni del repository locale.

   Per client Ubuntu 16.04 eseguire:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Per client Ubuntu 18.04 eseguire:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   Per client Ubuntu 20.04 eseguire:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)"
    ```

4. Installare `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>Verificare l'installazione

```bash
azdata
azdata --version
```

## <a name="update"></a>Aggiornamento

Aggiornare `azdata-cli` con i comandi `apt-get update` e `apt-get install`.

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>Disinstallare

1. Rimuovere il pacchetto dal sistema.

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. Rimuovere le informazioni del repository se non si prevede di reinstallare `azdata-cli`.

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. Rimuovere la chiave del repository.

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. Rimuovere le dipendenze non più necessarie.

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)

Usare azdata con i [servizi dati con abilitazione di Azure Arc](/azure/azure-arc/data/)
