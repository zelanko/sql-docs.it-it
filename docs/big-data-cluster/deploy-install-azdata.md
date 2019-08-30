---
title: Installare azdata con pip
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] la gestione (anteprima) con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160728"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>Installa `azdata` per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare lo `azdata` strumento per la versione finale candidata in Windows o Linux usando. `pip`

## <a id="prerequisites"></a> Prerequisiti

`azdata`è un'utilità della riga di comando scritta in Python che consente agli amministratori del cluster di bootstrap e gestire il cluster Big Data tramite le API REST. La versione minima richiesta di Python è 3.5. È inoltre `pip` necessario che sia utilizzato per scaricare e installare `azdata` lo strumento. Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python su altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).
È inoltre necessario installare e aggiornare la versione più recente del pacchetto Python *requests*:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se si installa una versione più recente di Big Data cluster, è necessario eseguire il backup dei dati ed eliminare il vecchio cluster prima `azdata` di aggiornare e installare la nuova versione. Per altre informazioni, vedere [Aggiornamento a una nuova versione](deployment-upgrade.md).

## <a id="windows"></a>Installazione `azdata` di Windows

1. In un client Windows, scaricare il pacchetto Python necessario da [https://www.python.org/downloads/](https://www.python.org/downloads/). Per Python 3.5.3 e versioni successive, quando si installa Python viene installato anche pip3. 

   > [!TIP] 
   > Quando si installa Python 3, selezionare l'opzione per aggiungere Python al **PERCORSO**. In caso contrario, è possibile trovare in seguito la posizione di pip3 e aggiungerlo manualmente al **PERCORSO**.

1. Aprire una nuova sessione di Windows PowerShell in modo che acceda al percorso di Python più recente.

1. Se sono state installate versioni precedenti dello strumento (prima della versione CTP 3,2, lo strumento era denominato **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di `azdata`. Il seguente comando rimuove la versione CTP 3,1 di **mssqlctl**.

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di, `azdata` è importante disinstallarlo prima di installare la versione più recente.

   Per la versione CTP 3,2, eseguire il comando seguente.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Eseguire `azdata` l'installazione con il comando seguente:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Installazione `azdata` di Linux

In Linux è necessario installare Python 3.5 e quindi eseguire l'aggiornamento di pip. Nell'esempio seguente vengono illustrati i comandi da usare per Ubuntu. Per altre piattaforme Linux, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Installare i pacchetti Python necessari:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. Aggiornare pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se sono state installate versioni precedenti dello strumento (prima della versione CTP 3,2, lo strumento era denominato **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di `azdata`. Il seguente comando rimuove la versione CTP 3,1 di **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di, `azdata` è importante disinstallarlo prima di installare la versione più recente.

   Per la versione CTP 3,2, eseguire il comando seguente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Eseguire `azdata` l'installazione con il comando seguente:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > Il `--user` Commuter viene installato `azdata` nella directory di installazione utente di Python. che in Linux solitamente è `~/.local/bin`. Aggiungere questa directory al percorso o passare alla directory di installazione utente ed eseguire `./azdata` da questa posizione.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
