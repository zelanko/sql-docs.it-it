---
title: Installare mssqlctl
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento mssqlctl per l'installazione e gestione dei cluster di big data 2019 Server SQL (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 61c1596de09f230020b3332730eb51cd131bba62
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728951"
---
# <a name="install-mssqlctl-to-manage-sql-server-big-data-clusters"></a>Installare mssqlctl per gestire i cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare il **mssqlctl** strumento per la versione CTP 3.1 in Windows o Linux.

**mssqlctl** è un'utilità della riga di comando scritta in Python che consente agli amministratori per avviare e gestire i cluster di big data tramite le API REST del cluster. La versione di Python minima richiesta è v3.5. È inoltre necessario disporre `pip` che consente di scaricare e installare **mssqlctl** dello strumento. Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python in altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

> [!IMPORTANT]
> Se si installa una versione più recente dei cluster di big data, è necessario eseguire il backup dei dati e si elimina il vecchio cluster *prima* aggiornare **mssqlctl** e installare la nuova versione. Per altre informazioni, vedere [l'aggiornamento a una nuova versione](deployment-upgrade.md).

## <a id="windows"></a> Installazione di Windows mssqlctl

1. In un client Windows, scaricare il pacchetto di Python necessario [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Per python3.5.3 e versioni successive, pip3 viene installato anche quando si installa Python. 

   > [!TIP] 
   > Quando si installa Python3, selezionare questa opzione per aggiungere Python al **percorso**. In caso contrario, è possibile trovare in un secondo momento in cui si trova pip3 e aggiungerlo manualmente per il **percorso**.

1. Aprire una nuova sessione di Windows PowerShell in modo che ottiene il percorso più recente di Python in esso.

1. Se si dispone di tutte le versioni precedenti di **mssqlctl** installato, è importante disinstallare **mssqlctl** prima prima di installare la versione più recente.

   Se si sta disinstallando **mssqlctl** corrispondente alla versione CTP versione 2.2 o inferiore eseguire:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Per versioni da CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.0` nel comando con la versione di **mssqlctl** che si desidera disinstallare. Se la versione è precedente alla versione CTP 3.0, aggiungere un trattino prima il numero di versione (ad esempio, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Installare **mssqlctl** con il comando seguente:

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Installazione di Linux mssqlctl

In Linux, è necessario installare Python 3.5 e quindi aggiornare pip. Nell'esempio seguente mostra i comandi che altrimenti funzionerebbero per Ubuntu. Per altre piattaforme Linux, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Installare i pacchetti Python necessari:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Eseguire l'aggiornamento pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se si dispone di tutte le versioni precedenti di **mssqlctl** installato, è importante disinstallare **mssqlctl** prima prima di installare la versione più recente.

   Se si sta disinstallando **mssqlctl** corrispondente alla versione CTP versione 2.2 o inferiore eseguire:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Per versioni da CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.0` nel comando con la versione di **mssqlctl** che si desidera disinstallare. Se la versione è precedente alla versione CTP 3.0, aggiungere un trattino prima il numero di versione (ad esempio, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Installare **mssqlctl** con il comando seguente:

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > Il `--user` commutatore mssqlctl viene installato nella directory di installazione di Python utente. Si tratta in genere `~/.local/bin` in Linux. Aggiungere questa directory al percorso o passare alla directory di installazione dell'utente e quindi eseguire `./mssqlctl` da tale posizione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
