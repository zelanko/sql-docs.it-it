---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire l'aggiornamento di SQL Server cluster di 2019 Big Data (anteprima) a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419390"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Come aggiornare SQL Server cluster Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce indicazioni su come eseguire l'aggiornamento di un cluster SQL Server Big Data a una nuova versione. I passaggi descritti in questo articolo si applicano in modo specifico a come eseguire l'aggiornamento tra versioni di anteprima.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup ed eliminare il vecchio cluster

Attualmente, l'unico modo per aggiornare un cluster Big Data a una nuova versione consiste nel rimuovere e ricreare manualmente il cluster. Ogni versione ha una versione univoca di **azdata** che non è compatibile con la versione precedente. Inoltre, se un cluster precedente doveva scaricare un'immagine in un nuovo nodo, l'immagine più recente potrebbe non essere compatibile con le immagini precedenti del cluster. Per eseguire l'aggiornamento alla versione più recente, attenersi alla procedura seguente:

1. Prima di eliminare il vecchio cluster, eseguire il backup dei dati nell'istanza di SQL Server master e in HDFS. Per l'istanza SQL Server Master è possibile utilizzare [SQL Server backup e ripristino](data-ingestion-restore-database.md). Per HDFS, è [possibile copiare i dati con **curl**](data-ingestion-curl.md).

1. Eliminare il vecchio cluster con il `azdata delete cluster` comando.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di **azdata** che corrisponde al cluster. Non eliminare un cluster precedente con la versione più recente di **azdata**.

1. Prima della versione CTP 3,2, **azdata** è stato chiamato **mssqlctl**. Se sono installate versioni precedenti di **mssqlctl** o **azdata** , è importante disinstallarlo prima di installare la versione più recente di **azdata**.

   Per CTP 2,3 o versioni successive, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di **mssqlctl** che si sta disinstallando. Se la versione è precedente alla CTP 3,1, aggiungere un trattino prima del numero di versione (ad `ctp-2.5`esempio,).

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Installare la versione più recente di **azdata**. I comandi seguenti installano **azdata** per CTP 3,2:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Per ogni versione, il percorso di **azdata** cambia. Anche se in precedenza è stato installato **azdata** o **mssqlctl**, è necessario reinstallare dal percorso più recente prima di creare il nuovo cluster.

## <a id="azdataversion"></a>Verificare la versione di azdata

Prima di distribuire un nuovo cluster di Big data, verificare che sia in uso la versione  più recente di `--version` azdata con il parametro:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Installare la nuova versione

Dopo aver rimosso il cluster di Big Data precedente e aver installato la versione più recente di **azdata**, distribuire il nuovo cluster Big data usando le istruzioni di distribuzione correnti. Per ulteriori informazioni, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md). Ripristinare quindi i database o i file necessari.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa sono i cluster SQL Server Big Data](big-data-cluster-overview.md).
