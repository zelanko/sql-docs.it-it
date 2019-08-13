---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come aggiornare cluster Big Data di SQL Server 2019 (anteprima) a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 29bdd3996112154b222ffb7d43390050c9af2d02
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731087"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Come aggiornare cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce informazioni su come eseguire l'aggiornamento di un cluster Big Data di SQL Server a una nuova versione. La procedura descritta in questo articolo fa riferimento in modo specifico all'aggiornamento tra versioni di anteprima.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup del cluster ed eliminarlo

Attualmente, l'unico modo per aggiornare un cluster Big Data a una nuova versione consiste nel rimuovere manualmente il cluster e ricrearlo. In ogni versione è presente una versione univoca di **azdata** che non è compatibile con la versione precedente. Se un cluster precedente doveva scaricare un'immagine in un nuovo nodo, è possibile che l'immagine più recente non fosse compatibile con le immagini precedenti del cluster. Per eseguire l'aggiornamento alla versione più recente, seguire questa procedura:

1. Prima di eliminare il cluster precedente, eseguire il backup dei dati nell'istanza master di SQL Server e in HDFS. Per l'istanza master di SQL Server è possibile usare [Backup e ripristino di SQL Server](data-ingestion-restore-database.md). Per HDFS, è [possibile copiare i dati con **curl**](data-ingestion-curl.md).

1. Eliminare il cluster precedente con il comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di **azdata** corrispondente al cluster in uso. Non eliminare un cluster precedente con la versione più recente di **azdata**.

1. Prima della versione CTP 3.2, **azdata** si chiamava **mssqlctl**. Se è installata una versione precedente di **mssqlctl** o **azdata**, è importante disinstallarla prima di installare la versione più recente di **azdata**.

   Per CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. Se la versione è precedente a CTP 3.1, aggiungere un trattino prima del numero di versione (ad esempio, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Installare la versione più recente di **azdata**. I comandi seguenti consentono di installare **azdata** per CTP 3.2:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Il percorso di **azdata** cambia per ogni versione. Anche se **azdata** o **mssqlctl** è già installato, è necessario reinstallarlo dal percorso più recente prima di creare il nuovo cluster.

## <a id="azdataversion"></a> Verificare la versione di azdata

Prima di distribuire un nuovo cluster Big Data, verificare che sia in uso la versione più recente di **azdata** con il parametro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Installare la nuova versione

Dopo aver rimosso il cluster Big Data precedente e aver installato la versione più recente di **azdata**, distribuire il nuovo cluster Big Data usando le istruzioni di distribuzione correnti. Per altre informazioni, vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md). Ripristinare quindi gli eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md).
