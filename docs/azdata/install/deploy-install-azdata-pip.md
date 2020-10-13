---
title: Installare azdata tramite pip
titleSuffix: ''
description: Informazioni su come installare lo strumento azdata con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ecf4eaaddf9423bb9a3ae88036b5c3cb2090451b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725285"
---
# <a name="install-azdata-with-pip"></a>Installare `azdata` con `pip`

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Questo articolo descrive come installare lo strumento `azdata` in Windows, Linux o macOS/OS X usando `pip`.

> [!TIP]
> Per un'esperienza più semplice, è possibile installare `azdata` con uno [strumento di gestione pacchetti](./deploy-install-azdata.md) per Windows, Linux, (distribuzioni Ubuntu, Debian, RHEL, CentOS, openSUSE e SLE) e macOS.

## <a name="prerequisites"></a><a id="prerequisites"></a> Prerequisiti

`azdata` è un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire le risorse dati tramite API REST. La versione minima richiesta di Python è 3.5. `pip` è obbligatorio per scaricare e installare lo strumento `azdata`. Le istruzioni seguenti forniscono esempi per Windows, Linux (Ubuntu) e macOS/OS X. Per l'installazione di Python in altre piattaforme, vedere la documentazione di [Python](https://wiki.python.org/moin/BeginnersGuide/Download). È anche necessario installare e aggiornare la versione più recente del pacchetto Python `requests`:

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Installazione di `azdata` per Windows

1. In un client Windows, scaricare il pacchetto Python necessario da [https://www.python.org/downloads/](https://www.python.org/downloads/). Per Python 3.5.3 e versioni successive, quando si installa Python viene installato anche pip3.

   > [!TIP]
   > Quando si installa Python 3, selezionare l'opzione per aggiungere Python a `PATH`. In alternativa, è possibile individuare in seguito la posizione di pip3 e aggiungerlo a `PATH` manualmente.

1. Aprire una nuova sessione di Windows PowerShell in modo che acceda al percorso di Python più recente.

1. A partire da SQL Server versione 2019 CU5, azdata include una versione semantica indipendente dal server. Se sono state installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente.

   Ad esempio, per 2019-cu4 eseguire questo comando:

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > Negli esempi precedenti sostituire `2019-cu6` con la versione e l'aggiornamento CU dell'installazione di `azdata`. 

1. Installare `azdata`.

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

1. Aggiornare pip3.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. A partire da SQL Server versione 2019 CU5, azdata include una versione semantica indipendente dal server. Se sono state installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente.

   Ad esempio, eseguire questo comando per `2019-cu6`:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > Negli esempi precedenti sostituire `2019-cu6` con la versione e l'aggiornamento CU dell'installazione di `azdata`.

1. Installare `azdata`.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > L'opzione `--user` consente di installare `azdata` nella directory di installazione utente di Python, che in Linux solitamente è `~/.local/bin`. Aggiungere questa directory al percorso o passare alla directory di installazione utente ed eseguire `./azdata` da questa posizione.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Installare `azdata` in macOS o OS X

Per installare `azdata` in macOS o OS X, eseguire questa procedura. Per ogni passaggio, eseguire l'esempio nel terminale.

1. In un client macOS installare [Homebrew](https://brew.sh) se non è stato ancora installato:

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Installare Python e pip, versione minima 3.0:

   ```bash
   brew install python3
   ```

1. Installare le dipendenze:

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. A partire da SQL Server versione 2019 CU5, azdata include una versione semantica indipendente dal server. Se sono state installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente. Ad esempio il comando seguente rimuove la versione RC1 di `azdata`:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Installare `azdata`.

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)

Usare azdata con i [servizi dati con abilitazione di Azure Arc](/azure/azure-arc/data/)
