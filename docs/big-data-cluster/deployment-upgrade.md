---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come aggiornare i cluster di big data di SQL Server 2019 (anteprima) a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 67ca9b09db398538b4adeedc9008dcb2f14f258f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958403"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Come aggiornare i cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce indicazioni su come aggiornare un cluster di big data di SQL Server a una nuova versione. I passaggi descritti in questo articolo si applicano specificamente al modo in cui eseguire l'aggiornamento tra versioni di anteprima.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup ed eliminare il vecchio cluster

Attualmente, l'unico modo per aggiornare un cluster di big data a una nuova versione è manualmente, rimuovere e ricreare il cluster. Ogni versione ha una versione univoca del **mssqlctl** che non è compatibile con la versione precedente. Inoltre, se un cluster precedente è stato necessario scaricare un'immagine in un nuovo nodo, l'immagine più recente potrebbe non essere compatibile con le immagini precedenti nel cluster. Per eseguire l'aggiornamento alla versione più recente, procedere come segue:

1. Prima di eliminare il vecchio cluster, eseguire il backup dei dati nell'istanza di master di SQL Server e in HDFS. Per l'istanza master di SQL Server, è possibile usare [SQL Server backup e ripristino](data-ingestion-restore-database.md). Per un HDFS, si [possibile copiare i dati con **curl**](data-ingestion-curl.md).

1. Eliminare il vecchio cluster con il `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di **mssqlctl** che corrisponde al cluster. Non eliminare un cluster con la versione più recente di meno recente **mssqlctl**.

1. Se si dispone di tutte le versioni precedenti di **mssqlctl** installato, è importante disinstallare **mssqlctl** prima prima di installare la versione più recente.

   Per versioni da CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.0` nel comando con la versione di **mssqlctl** che si desidera disinstallare. Se la versione è precedente alla versione CTP 3.0, aggiungere un trattino prima il numero di versione (ad esempio, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Installare la versione più recente di **mssqlctl**. I seguenti comandi installano **mssqlctl** per la versione CTP 3.1:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
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
