---
title: Installare azdata con yum
titleSuffix: ''
description: Informazioni su come installare lo strumento azdata con yum.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eae81ccee65899335b161b3a32fbb260d0a8517a
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914900"
---
# <a name="install-azdata-with-yum"></a>Installare `azdata` con yum

Per le distribuzioni Linux con `yum` è disponibile un pacchetto per `azdata-cli`. Il pacchetto dell'interfaccia della riga di comando è stato testato nelle versioni di Linux che usano `yum`:

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>Eseguire l'installazione con Yum

>[!IMPORTANT]
> Il pacchetto RPM di `azdata-cli` dipende dal pacchetto python3. Nel sistema potrebbe trattarsi di una versione di Python che risale a una data precedente al requisito di *Python 3.6.x*. Se questa situazione costituisce un problema, trovare un pacchetto python3 sostitutivo o seguire le istruzioni per l'installazione manuale che usano [`pip`](../install/deploy-install-azdata-pip.md).

1. Importare la chiave del repository Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Creare le informazioni del repository locale

   Per un client RHEL 7, eseguire:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   Per un client RHEL 8, eseguire:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
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

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)

Usare azdata con [i servizi dati con abilitazione di Azure Arc](/azure/azure-arc/data/)
