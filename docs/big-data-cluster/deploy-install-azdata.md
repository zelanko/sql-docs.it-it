---
title: Installare il modulo azdata
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aaccdff9d5debe30eacfddfd8423a0a57b8a37fb
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028559"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>Installare azdata per gestire i cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare lo strumento **azdata** per CTP 3.2 in Windows o Linux.

## <a id="prerequisites"></a> Prerequisiti

**azdata** è un'utilità da riga di comando scritta in Python che consente agli amministratori del cluster di avviare e gestire il cluster Big Data tramite le API REST. La versione minima richiesta di Python è 3.5. È necessario avere lo strumento `pip` usato per scaricare e installare lo strumento **azdata**. Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python su altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).
È inoltre necessario installare e aggiornare la versione più recente del pacchetto Python *requests*:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se si installa una versione più recente del cluster Big Data, è necessario eseguire il backup dei dati ed eliminare il cluster precedente *prima* di aggiornare **azdata** e installare la nuova versione. Per altre informazioni, vedere [Aggiornamento a una nuova versione](deployment-upgrade.md).

## <a id="windows"></a> Installazione di azdata per Windows

1. In un client Windows, scaricare il pacchetto Python necessario da [https://www.python.org/downloads/](https://www.python.org/downloads/). Per Python 3.5.3 e versioni successive, quando si installa Python viene installato anche pip3. 

   > [!TIP] 
   > Quando si installa Python 3, selezionare l'opzione per aggiungere Python al **PERCORSO**. In caso contrario, è possibile trovare in seguito la posizione di pip3 e aggiungerlo manualmente al **PERCORSO**.

1. Aprire una nuova sessione di Windows PowerShell in modo che acceda al percorso di Python più recente.

1. Se sono installate versioni precedenti dello strumento installato (precedentemente denominato **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di **azdata**.

   Per CTP 3.1 o versione precedente, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di **azdata**, è importante disinstallarlo prima di installare la versione più recente.

   Per CTP 3.2 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.2` nel comando con la versione di **azdata** che si sta disinstallando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Installare **azdata** con il comando seguente:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a> Installazione di azdata per Linux

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

1. Se sono installate versioni precedenti dello strumento installato (precedentemente denominato **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di **azdata**.

   Per CTP 3.1 o versione precedente, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di **azdata**, è importante disinstallarlo prima di installare la versione più recente.

   Per CTP 3.2 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.2` nel comando con la versione di **azdata** che si sta disinstallando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Installare **azdata** con il comando seguente:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > L'opzione `--user` consente di installare azdata nella directory di installazione utente di Python, che in Linux solitamente è `~/.local/bin`. Aggiungere questa directory al percorso o passare alla directory di installazione utente ed eseguire `./azdata` da questa posizione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md).
