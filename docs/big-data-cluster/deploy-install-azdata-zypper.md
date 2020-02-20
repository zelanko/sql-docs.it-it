---
title: Installare azdata con zypper
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data con zypper.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a02b4f0707d98d8acc9e65a2a27cee8d886c1ae7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75728572"
---
# <a name="install-azdata-with-zypper"></a>Installare `azdata` con zypper

Per le distribuzioni Linux con `zypper` è disponibile un pacchetto per `azdata-cli`. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di Linux che usano `zyper`:

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>Eseguire l'installazione con Zypper
>[!IMPORTANT]
>Il pacchetto RPM di `azdata-cli` dipende dal pacchetto python3. Nel sistema potrebbe trattarsi di una versione di Python che risale a una data precedente al requisito di *Python 3.6.x*. Se questa situazione costituisce un problema, trovare un pacchetto python3 sostitutivo o seguire le istruzioni per l'installazione manuale che usano [`pip`](deploy-install-azdata-pip.md).

1. Installare le dipendenze necessarie per l'installazione di `azdata-cli`

   ```bash
   sudo zypper install -y curl
   ```

1. Importare la chiave del repository Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Creare le informazioni del repository locale

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

1. Installazione

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>Verificare l'installazione

   ```bash
   azdata
   azdata --version
   ```

## <a name="update"></a>Aggiornamento

Aggiornare `azdata-cli` con il comando `zypper update`.

   ```bash
   sudo zypper refresh
   sudo zypper update azdata-cli
   ```

## <a name="uninstall"></a>Disinstallare

Rimuovere il pacchetto dal sistema

```bash
   sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
