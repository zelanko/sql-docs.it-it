---
title: Installare mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Informazioni su come installare lo strumento mssqlctl per l'installazione e gestione dei cluster di big data 2019 Server SQL (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/15/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aec8f030a996e5dd86c44a5a655e98d4926988ed
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361411"
---
# <a name="install-mssqlctl-to-manage-sql-server-2019-big-data-clusters"></a>Installare mssqlctl per gestire i cluster di SQL Server 2019 dei big Data

Questo articolo descrive come installare il **mssqlctl** strumento in Windows o Linux.

**mssqlctl** è un'utilità della riga di comando scritta in Python che consente agli amministratori per avviare e gestire i cluster di big data tramite le API REST del cluster. La versione di Python minima richiesta è v3.5. È inoltre necessario disporre `pip` che consente di scaricare e installare **mssqlctl** dello strumento. Le istruzioni seguenti forniscono esempi per Windows e Ubuntu. Per l'installazione di Python in altre piattaforme, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

> [!IMPORTANT]
> Se è installata una versione precedente di **mssqlctl**, è necessario eliminare il cluster *prima* aggiornamento **mssqlctl** e installare la nuova versione. Per altre informazioni, vedere [l'aggiornamento a una nuova versione](deployment-guidance.md#upgrade).

## <a id="windows"></a> Installazione di Windows mssqlctl

1. In un client Windows, scaricare il pacchetto di Python necessario [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Per python3.5.3 e versioni successive, pip3 viene installato anche quando si installa Python. 

   > [!TIP] 
   > Quando si installa Python3, selezionare questa opzione per aggiungere Python al **percorso**. In caso contrario, è possibile trovare in un secondo momento in cui si trova pip3 e aggiungerlo manualmente per il **percorso**.

1. Aprire una nuova sessione di Windows PowerShell in modo che ottiene il percorso più recente di Python in esso.

2. Installare **mssqlctl** con il comando seguente:

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
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
   
1. Installare **mssqlctl** con il comando seguente:

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl --user
   ```
   
   > [!NOTE]
   > Il `--user` commutatore mssqlctl viene installato nella directory di installazione di Python utente. Si tratta in genere `~/.local/bin` in Linux. Aggiungere questa directory al percorso o passare alla directory di installazione dell'utente e quindi eseguire `./mssqlctl` da tale posizione.
   
## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
