---
title: Installare azdata
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di SQL Server cluster 2019 Big Data (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426441"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>Installare azdata per gestire i cluster di Big Data SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare lo strumento **azdata** per CTP 3,2 in Windows o Linux.

## <a id="prerequisites"></a> Prerequisiti

**azdata** è un'utilità della riga di comando scritta in Python che consente agli amministratori del cluster di eseguire il bootstrap e gestire il cluster Big data tramite le API REST. La versione minima di Python richiesta è v 3.5. È necessario `pip` che sia usato anche per scaricare e installare lo strumento **azdata** . Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python su altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Inoltre, è necessario installare e aggiornare la versione più recente del pacchetto python *richieste* :
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se si installa una versione più recente di Big Data cluster, è necessario eseguire il backup dei dati ed eliminare il vecchio cluster *prima* di aggiornare **azdata** e installare la nuova versione. Per ulteriori informazioni, vedere [aggiornamento a una nuova versione](deployment-upgrade.md).

## <a id="windows"></a>Installazione di Windows azdata

1. In un client Windows, scaricare il pacchetto Python necessario da [https://www.python.org/downloads/](https://www.python.org/downloads/). Per Python 3.5.3 e versioni successive, PIP3 viene installato anche quando si installa Python. 

   > [!TIP] 
   > Quando si installa python3, selezionare per aggiungere Python al **percorso**. In caso contrario, è possibile trovare in seguito la posizione in cui si trova PIP3 e aggiungerlo manualmente al **percorso**.

1. Aprire una nuova sessione di Windows PowerShell in modo da ottenere il percorso più recente con Python.

1. Se sono state installate versioni precedenti dello strumento (previosly denominato **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di **azdata**.

   Per la versione CTP 3,1 o una versione precedente, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di **azdata** , è importante disinstallarlo prima di installare la versione più recente.

   Per CTP 3,2 o versioni successive, eseguire il comando seguente. Sostituire `ctp3.2` nel comando con la versione di **azdata** che si sta disinstallando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Installare **azdata** con il comando seguente:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Installazione di azdata Linux

In Linux è necessario installare Python 3,5 e quindi eseguire l'aggiornamento di PIP. Nell'esempio seguente vengono illustrati i comandi che funzionano per Ubuntu. Per altre piattaforme Linux, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Installare i pacchetti Python necessari:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. PIP3 di aggiornamento:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se sono state installate versioni precedenti dello strumento (in precedenza denominate **mssqlctl**), è importante disinstallarlo prima di installare la versione più recente di **azdata**.

   Per la versione CTP 3,1 o una versione precedente, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se sono installate versioni precedenti di **azdata** , è importante disinstallarlo prima di installare la versione più recente.

   Per CTP 3,2 o versioni successive, eseguire il comando seguente. Sostituire `ctp3.2` nel comando con la versione di **azdata** che si sta disinstallando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Installare **azdata** con il comando seguente:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > Il `--user` Commuter installa azdata nella directory di installazione utente di Python. Si tratta in `~/.local/bin` genere di Linux. Aggiungere questa directory al percorso o passare alla directory di installazione dell'utente ed eseguire `./azdata` da questa posizione.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster Big Data, vedere [che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md).
