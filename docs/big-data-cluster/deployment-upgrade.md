---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server Big Data Clusters
description: Informazioni su come aggiornare cluster Big Data di SQL Server a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f44ef17a712d0d5a19707cf94e7d3e4196a2aba3
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706304"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Come aggiornare [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce informazioni su come eseguire l'aggiornamento di un cluster Big Data di SQL Server a una nuova versione. La procedura descritta in questo articolo fa riferimento in modo specifico all'aggiornamento da una versione di anteprima alla versione di aggiornamento del servizio SQL Server 2019.

## <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup del cluster ed eliminarlo

Attualmente non è disponibile alcun aggiornamento sul posto per i cluster Big Data e l'unico modo per eseguire l'aggiornamento a una nuova versione consiste nel rimuovere manualmente il cluster e quindi ricrearlo. In ogni versione è presente una versione univoca di `azdata` che non è compatibile con la versione precedente. Inoltre, se un cluster di una versione precedente deve scaricare un'immagine del contenitore in un nuovo nodo, l'immagine più recente potrebbe non essere compatibile con quelle meno recenti nel cluster. Si noti che l'immagine più recente viene ottenuta solo se si usa il tag di immagine `latest` nel file di configurazione della distribuzione per le impostazioni del contenitore. Per impostazione predefinita, ogni versione include un tag di immagine specifico corrispondente alla versione di SQL Server. Per eseguire l'aggiornamento alla versione più recente, seguire questa procedura:

1. Prima di eliminare il cluster precedente, eseguire il backup dei dati nell'istanza master di SQL Server e in HDFS. Per l'istanza master di SQL Server è possibile usare [Backup e ripristino di SQL Server](data-ingestion-restore-database.md). Per HDFS, è [possibile copiare i dati con `curl`](data-ingestion-curl.md).

1. Eliminare il cluster precedente con il comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di `azdata` corrispondente al cluster in uso. Non eliminare un cluster di una versione precedente con la versione più recente di `azdata`.

   > [!Note]
   > L'invio di un comando `azdata bdc delete` comporterà l'eliminazione di tutti gli oggetti creati all'interno dello spazio dei nomi identificato con il nome del cluster Big Data, ma non lo spazio dei nomi stesso. È possibile riutilizzare lo spazio dei nomi per le distribuzioni successive, purché sia vuoto e non siano state create altre applicazioni al suo interno.

1. Disinstallare la versione precedente di `azdata`

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Installare la versione più recente di `azdata`. I comandi seguenti installano `azdata` dalla versione più recente:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Il percorso della versione `n-1` di `azdata` cambia per ogni versione. Anche se `azdata` è già stato installato, è necessario reinstallarlo dal percorso più recente prima di creare il nuovo cluster.

## <a id="azdataversion"></a> Verificare la versione di azdata

Prima di distribuire un nuovo cluster Big Data, assicurarsi di usare la versione più recente di `azdata` con il parametro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Installare la nuova versione

Dopo aver rimosso il cluster Big Data precedente e aver installato la versione più recente di `azdata`, distribuire il nuovo cluster Big Data usando le istruzioni di distribuzione correnti. Per altre informazioni, vedere [Come distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Kubernetes](deployment-guidance.md). Ripristinare quindi gli eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md)
