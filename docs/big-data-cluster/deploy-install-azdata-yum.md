---
title: Installare azdata con yum
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cf6e061b0ca4fca7c843575a87038a801ab8f758
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75728552"
---
# <a name="install-azdata-with-yum"></a>Installare `azdata` con yum

Per le distribuzioni Linux con `yum` è disponibile un pacchetto per `azdata-cli`. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di Linux che usano `yum`:

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>Eseguire l'installazione con Yum

>[!IMPORTANT]
> Il pacchetto RPM di `azdata-cli` dipende dal pacchetto python3. Nel sistema potrebbe trattarsi di una versione di Python che risale a una data precedente al requisito di *Python 3.6.x*. Se questa situazione costituisce un problema, trovare un pacchetto python3 sostitutivo o seguire le istruzioni per l'installazione manuale che usano [`pip`](deploy-install-azdata-pip.md).

1. Importare la chiave del repository Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Creare le informazioni del repository locale

   Per un client RHEL 7, eseguire:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```
  
   Per un client RHEL 8, eseguire:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   ```

1. Eseguire l'installazione con il comando `yum install`

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>Verificare l'installazione

```
azdata
azdata --version
```

## <a name="update"></a>Aggiornamento

Aggiornare `azdata-cli` con il comando `yum update`.

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>Disinstallare

1. Rimuovere il pacchetto dal sistema

   ```bash
   sudo yum remove azdata-cli
   ```

1. Rimuovere le informazioni del repository se non si prevede di reinstallare `azdata-cli`

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
