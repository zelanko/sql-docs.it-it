---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come aggiornare i cluster di big data di SQL Server 2019 (anteprima) a una nuova versione.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f8291eeb292226b3dfcb2bd1a89816926c53d88
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993981"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Come aggiornare i cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce indicazioni su come aggiornare un cluster di big data di SQL Server a una nuova versione. I passaggi descritti in questo articolo si applicano specificamente al modo in cui eseguire l'aggiornamento tra versioni di anteprima.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup ed eliminare il vecchio cluster

Attualmente, l'unico modo per aggiornare un cluster di big data a una nuova versione è manualmente, rimuovere e ricreare il cluster. Ogni versione ha una versione univoca del **mssqlctl** che non è compatibile con la versione precedente. Inoltre, se un cluster precedente è stato necessario scaricare un'immagine in un nuovo nodo, l'immagine più recente potrebbe non essere compatibile con le immagini precedenti nel cluster. Per eseguire l'aggiornamento alla versione più recente, procedere come segue:

1. Prima di eliminare il vecchio cluster, eseguire il backup dei dati nell'istanza di master di SQL Server e in HDFS. Per l'istanza master di SQL Server, è possibile usare [SQL Server backup e ripristino](data-ingestion-restore-database.md). Per un HDFS, si [possibile copiare i dati con **curl**](data-ingestion-curl.md).

1. Eliminare il vecchio cluster con il `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di **mssqlctl** che corrisponde al cluster. Non eliminare un cluster con la versione più recente di meno recente **mssqlctl**.

1. Se si dispone di tutte le versioni precedenti di **mssqlctl** installato, è importante disinstallare **mssqlctl** prima prima di installare la versione più recente.

   Se si sta disinstallando **mssqlctl** corrispondente a CTP 2.2 o eseguito inferiore:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Per versioni da CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp-2.4` nel comando con la versione di **mssqlctl** che si desidera disinstallare:

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt
   ```

1. Installare la versione più recente di **mssqlctl**. I seguenti comandi installano **mssqlctl** versione CTP 3.0:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > Per ogni versione e il percorso **mssqlctl** le modifiche. Anche se è installato in precedenza **mssqlctl**, è necessario reinstallare dal percorso più recente prima di creare il nuovo cluster.

## <a id="mssqlctlversion"></a> Verificare la versione mssqlctl

Prima di distribuire un nuovo cluster di big data, verificare che si stia utilizzando la versione più recente di **mssqlctl** con il `--version` parametro:

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>Installare la nuova versione

Dopo avere rimosso il cluster di big data precedente e installare la versione più recente **mssqlctl**, distribuire il nuovo cluster di big data usando le istruzioni di distribuzione corrente. Per altre informazioni, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md). Quindi, ripristinare eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [quali sono i cluster di SQL Server i big data](big-data-cluster-overview.md).
