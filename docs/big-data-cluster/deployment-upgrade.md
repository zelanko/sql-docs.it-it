---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] l'aggiornamento (anteprima) a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 867729b7d638960a2dbf2cb5f7544fecf698c94d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652339"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Come eseguire l'aggiornamento[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

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

Dopo aver rimosso il cluster Big Data precedente e aver installato la versione più recente di **azdata**, distribuire il nuovo cluster Big Data usando le istruzioni di distribuzione correnti. Per ulteriori informazioni, vedere [la pagina relativa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] alla modalità di distribuzione in Kubernetes](deployment-guidance.md). Ripristinare quindi gli eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster Big Data, vedere [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)la pagina relativa a.
