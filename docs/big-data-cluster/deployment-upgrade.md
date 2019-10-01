---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire l'aggiornamento [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (anteprima) a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688269"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Come eseguire l'aggiornamento [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce informazioni su come eseguire l'aggiornamento di un cluster Big Data di SQL Server a una nuova versione. La procedura descritta in questo articolo fa riferimento in modo specifico all'aggiornamento tra versioni di anteprima.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup del cluster ed eliminarlo

Attualmente, l'unico modo per aggiornare un cluster Big Data a una nuova versione consiste nel rimuovere manualmente il cluster e ricrearlo. Ogni versione ha una versione univoca di `azdata` che non è compatibile con la versione precedente. Se un cluster precedente doveva scaricare un'immagine in un nuovo nodo, è possibile che l'immagine più recente non fosse compatibile con le immagini precedenti del cluster. Per eseguire l'aggiornamento alla versione più recente, seguire questa procedura:

1. Prima di eliminare il cluster precedente, eseguire il backup dei dati nell'istanza master di SQL Server e in HDFS. Per l'istanza master di SQL Server è possibile usare [Backup e ripristino di SQL Server](data-ingestion-restore-database.md). Per HDFS, è [possibile copiare i dati con `curl`](data-ingestion-curl.md).

1. Eliminare il cluster precedente con il comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di `azdata` che corrisponde al cluster. Non eliminare un cluster precedente con la versione più recente di `azdata`.

   > [!Note]
   > Se si emette un comando `azdata bdc delete`, tutti gli oggetti creati all'interno dello spazio dei nomi identificato con il nome del cluster Big Data verranno eliminati, ma non lo spazio dei nomi stesso. È possibile riutilizzare lo spazio dei nomi per le distribuzioni successive, purché sia vuoto e che non siano state create altre applicazioni all'interno di.

1. Prima della versione CTP 3,2, `azdata` veniva chiamato `mssqlctl`. Se sono installate versioni precedenti di `mssqlctl` o `azdata`, è importante disinstallare prima di installare la versione più recente di `azdata`.

   Per CTP 2.3 o versione successiva, eseguire il comando seguente. Sostituire `ctp3.1` nel comando con la versione di `mssqlctl` in cui si sta disinstallando. Se la versione è precedente a CTP 3.1, aggiungere un trattino prima del numero di versione (ad esempio, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Installare la versione più recente di `azdata`. I comandi seguenti consentono di installare `azdata` per la versione finale candidata:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Per ogni versione, viene modificato il percorso di `azdata`. Anche se in precedenza è stato installato `azdata` o `mssqlctl`, è necessario reinstallare dal percorso più recente prima di creare il nuovo cluster.

## <a id="azdataversion"></a> Verificare la versione di azdata

Prima di distribuire un nuovo cluster di Big Data, verificare di usare la versione più recente di `azdata` con il parametro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Installare la nuova versione

Dopo aver rimosso il cluster di Big Data precedente e aver installato la versione più recente `azdata`, distribuire il nuovo cluster Big Data usando le istruzioni di distribuzione correnti. Per ulteriori informazioni, vedere [How to deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on Kubernetes](deployment-guidance.md). Ripristinare quindi gli eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster Big Data, vedere [che cosa sono [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).
