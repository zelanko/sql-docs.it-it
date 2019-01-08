---
title: Installare mssqlctl per la gestione dei cluster di SQL 2019 dei big Data | Microsoft Docs
description: Informazioni su come installare lo strumento mssqlctl per l'installazione e gestione dei cluster di big data 2019 Server SQL (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/13/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 5133134a45a4110abc0a1a7a3eebe1c5ac7b6ebd
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432104"
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
   sudo apt-get install -y python3-pip && /
   sudo -H pip3 install --upgrade pip
   ```

1. Installare **mssqlctl** con il comando seguente:

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
   ```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
