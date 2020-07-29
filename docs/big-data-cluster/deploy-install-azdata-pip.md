---
title: Installare azdata tramite pip
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 034514c13a65171fca9eb1fc20b6c496329816a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773634"
---
# <a name="install-azdata-with-pip"></a>Installare `azdata` con `pip`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come installare lo strumento `azdata` in Windows o Linux tramite `pip`.

Per Windows e Linux (distribuzione Ubuntu), è possibile semplificare l'esperienza di installazione con uno strumento di [gestione pacchetti](./deploy-install-azdata-installer.md).

## <a name="prerequisites"></a><a id="prerequisites"></a> Prerequisiti

`azdata` è un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big Data tramite le API REST. La versione minima richiesta di Python è 3.5. L'uso di `pip` è obbligatorio per scaricare e installare lo strumento `azdata`. Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python su altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).
È anche necessario installare e aggiornare la versione più recente del pacchetto Python `requests`:

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se si intende installare una versione più recente del cluster Big Data, eseguire il backup dei dati ed eliminare il cluster precedente aggiornando `azdata` e installando la nuova versione. Per altre informazioni, vedere [Aggiornamento a una nuova versione](deployment-upgrade.md).

## <a name="windows-azdata-installation"></a><a id="windows"></a> Installazione di `azdata` per Windows

1. In un client Windows, scaricare il pacchetto Python necessario da [https://www.python.org/downloads/](https://www.python.org/downloads/). Per Python 3.5.3 e versioni successive, quando si installa Python viene installato anche pip3. 

   > [!TIP] 
   > Quando si installa Python 3, selezionare l'opzione per aggiungere Python a `PATH`. In alternativa, è possibile individuare in seguito la posizione di pip3 e aggiungerlo a `PATH` manualmente.

1. Aprire una nuova sessione di Windows PowerShell in modo che acceda al percorso di Python più recente.

1. Se sono installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente.

   Per CTP 3.2 o RC1, eseguire il comando seguente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   o
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Installare `azdata` con il comando seguente:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Installazione di `azdata` per Linux

In Linux è necessario installare Python 3.5 e quindi eseguire l'aggiornamento di pip. Nell'esempio seguente vengono illustrati i comandi da usare per Ubuntu. Per altre piattaforme Linux, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Installare i pacchetti Python necessari:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. Aggiornare pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se sono installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente.

   Per CTP 3.2 o RC1, eseguire il comando seguente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   o
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Installare `azdata` con il comando seguente:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > L'opzione `--user` consente di installare `azdata` nella directory di installazione utente di Python, che in Linux solitamente è `~/.local/bin`. Aggiungere questa directory al percorso o passare alla directory di installazione utente ed eseguire `./azdata` da questa posizione.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Installare `azdata` in macOS o OS X

Per installare `azdata` in macOS o OS X, eseguire questa procedura. Per ogni passaggio, eseguire l'esempio nel terminale.

1. In un client macOS installare [Homebrew](https://brew.sh) se non è stato ancora installato:

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Installare Python e pip, versione minima 3.0:

   ```
   brew install python3
   ```

1. Installare le dipendenze:

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. Se sono installate versioni precedenti dello strumento, è importante disinstallarle prima di installare la versione più recente di `azdata`. Il comando seguente rimuove la versione di `azdata` installata.

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Installare `azdata` con il comando seguente:

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
