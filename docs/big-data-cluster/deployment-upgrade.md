---
title: Eseguire l'aggiornamento a una nuova versione
titleSuffix: SQL Server Big Data Clusters
description: Informazioni su come aggiornare cluster Big Data di SQL Server a una nuova versione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 776c54ef7475b1ff7c5679f98e994a1b42784262
ms.sourcegitcommit: 52925f1928205af15dcaaf765346901e438ccc25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80607834"
---
# <a name="how-to-upgrade-big-data-clusters-2019"></a>Come aggiornare [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Il percorso di aggiornamento dipende dalla versione corrente del cluster Big Data di SQL Server (BDC). L'aggiornamento da una versione supportata, tra cui l'aggiornamento pubblico (GDR), l'aggiornamento cumulativo (CU) o l'aggiornamento QFE (Quick Fix Engineering), può essere eseguito sul posto. L'aggiornamento sul posto da una versione CTP (Customer Technology Preview) o dalla versione finale candidata di BDC non è supportato. È necessario rimuovere e ricreare il cluster. Le sezioni seguenti descrivono i passaggi per ogni scenario:

- [Aggiornamento dalla versione supportata](#upgrade-from-supported-release)
- [Aggiornamento di una distribuzione BDC da una versione CTP o una versione finale candidata](#update-a-bdc-deployment-from-ctp-or-release-candidate)

>[!NOTE]
>La prima versione supportata dei cluster Big Data è SQL Server 2019 GDR1.

## <a name="upgrade-release-notes"></a>Note sulla versione dell'aggiornamento

Prima di procedere, consultare le [note sulla versione dell'aggiornamento per verificare la presenza di problemi noti](release-notes-big-data-cluster.md#known-issues).

## <a name="upgrade-from-supported-release"></a>Aggiornamento dalla versione supportata

In questa sezione viene illustrato come aggiornare BDC per SQL Server da una versione supportata (a partire da SQL Server 2019 GDR1) a una versione supportata più recente.

1. Eseguire un backup dell'istanza master di SQL Server.
2. Eseguire un backup di HDFS.

   ```
   azdata bdc hdfs cp --from-path <path> --to-path <path>
   ```
   
   Ad esempio: 

   ```
   azdata bdc hdfs cp --from-path hdfs://user/hive/warehouse/%%D --to-path ./%%D
   ```

3. Aggiornare `azdata`.

   Seguire le istruzioni per l'installazione di `azdata`. 
   - [Windows Installer](deploy-install-azdata-installer.md)
   - [Linux con apt](deploy-install-azdata-linux-package.md)
   - [Linux con yum](deploy-install-azdata-yum.md)
   - [Linux con zypper](deploy-install-azdata-zypper.md)

   >[!NOTE]
   >Se `azdata` è stato installato con `pip` è necessario rimuoverlo manualmente prima di eseguire l'installazione con Windows Installer o la gestione pacchetti di Linux.

1. Aggiornare il cluster Big Data.

   ```
   azdata bdc upgrade -n <clusterName> -t <imageTag> -r <containerRegistry>/<containerRepository>
   ```

   Ad esempio, lo script seguente il tag immagine `2019-CU4-ubuntu-16.04`:

   ```
   azdata bdc upgrade -n bdc -t 2019-CU4-ubuntu-16.04 -r mcr.microsoft.com/mssql/bdc
   ```

>[!NOTE]
>I tag immagine più recenti sono disponibili nelle [note sulla versione dei cluster Big Data di SQL Server 2019](release-notes-big-data-cluster.md).

>[!IMPORTANT]
>Se si usa un repository privato per eseguire preventivamente il pull delle immagini per la distribuzione o l'aggiornamento di BDC, verificare che le immagini di compilazione correnti e le immagini di compilazione di destinazione si trovino nel repository privato. Questo consente di ripristinare correttamente lo stato precedente, se necessario. Se le credenziali del repository privato sono state modificate dopo la distribuzione originale, inoltre, aggiornare le variabili di ambiente corrispondenti DOCKER_PASSWORD e DOCKER_USERNAME. L'aggiornamento con diversi repository privati per le compilazioni correnti e di destinazione non è supportato.

### <a name="increase-the-timeout-for-the-upgrade"></a>Aumentare il timeout per l'aggiornamento

È possibile che si verifichi un timeout se alcuni componenti non vengono aggiornati nel tempo allocato. Il codice seguente illustra il possibile aspetto dell'errore:

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

Per aumentare i timeout per un aggiornamento, usare i parametri **--controller-timeout** e **--component-timeout** per specificare valori più elevati quando si esegue l'aggiornamento. Questa opzione è disponibile solo a partire da SQL Server 2019 CU2. Ad esempio:

   ```bash
   azdata bdc upgrade -t 2019-CU4-ubuntu-16.04 --controller-timeout=40 --component-timeout=40 --stability-threshold=3
   ```
**--controller-timeout** indica il numero di minuti di attesa del completamento dell'aggiornamento del controller o del database del controller.
**--component-timeout** definisce la quantità di tempo disponibile per il completamento di ogni fase successiva dell'aggiornamento.

Per aumentare i timeout per un aggiornamento prima della versione SQL Server 2019 CU2, modificare la mappa di configurazione dell'aggiornamento. Per modificare la mappa di configurazione dell'aggiornamento:

Eseguire il comando seguente:

   ```bash
   kubectl edit configmap controller-upgrade-configmap
   ```

Modificare i campi seguenti:

   **controllerUpgradeTimeoutInMinutes** Indica il numero di minuti di attesa del completamento dell'aggiornamento del controller o del database del controller. Il valore predefinito è 5. Per l'aggiornamento impostare almeno 20.
   **totalUpgradeTimeoutInMinutes**: Definisce la combinazione del tempo impiegato dal controller e il tempo impiegato dal database del controller per completare l'aggiornamento (aggiornamento controller + database del controller). Il valore predefinito è 10. Per l'aggiornamento impostare almeno 40.
   **componentUpgradeTimeoutInMinutes**: Definisce la quantità di tempo disponibile per il completamento di ogni fase successiva dell'aggiornamento. L'impostazione predefinita è 30. Per l'aggiornamento impostare su 45.

Salvare e uscire.

## <a name="update-a-bdc-deployment-from-ctp-or-release-candidate"></a>Aggiornamento di una distribuzione BDC da una versione CTP o una versione finale candidata

L'aggiornamento sul posto da una compilazione CTP o di una versione finale candidata dei cluster Big Data di SQL Server non è supportato. Nella sezione seguente viene illustrato come rimuovere manualmente il cluster e ricrearlo.

### <a name="backup-and-delete-the-old-cluster"></a>Eseguire il backup del cluster ed eliminarlo

Non è disponibile alcun aggiornamento sul posto per i cluster Big Data distribuiti prima del rilascio di SQL Server 2019 GDR1. L'unico modo per eseguire l'aggiornamento a una nuova versione è rimuovere manualmente il cluster e ricrearlo. In ogni versione è presente una versione univoca di `azdata` che non è compatibile con la versione precedente. Inoltre, se un'immagine del contenitore più recente viene scaricata in un cluster distribuito con un'altra versione precedente, l'immagine più recente potrebbe non essere compatibile con quelle meno recenti nel cluster. Il pull dell'immagine più recente viene eseguito se si usa il tag di immagine `latest` nel file di configurazione della distribuzione per le impostazioni del contenitore. Per impostazione predefinita, ogni versione include un tag di immagine specifico corrispondente alla versione di SQL Server. Per eseguire l'aggiornamento alla versione più recente, seguire questa procedura:

1. Prima di eliminare il cluster precedente, eseguire il backup dei dati nell'istanza master di SQL Server e in HDFS. Per l'istanza master di SQL Server è possibile usare [Backup e ripristino di SQL Server](data-ingestion-restore-database.md). Per HDFS, è [possibile copiare i dati con `curl`](data-ingestion-curl.md).

1. Eliminare il cluster precedente con il comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Usare la versione di `azdata` corrispondente al cluster in uso. Non eliminare un cluster di una versione precedente con la versione più recente di `azdata`.

   > [!Note]
   > L'invio di un comando `azdata bdc delete` comporterà l'eliminazione di tutti gli oggetti creati all'interno dello spazio dei nomi identificato con il nome del cluster Big Data, ma non lo spazio dei nomi stesso. È possibile riutilizzare lo spazio dei nomi per le distribuzioni successive, purché sia vuoto e non siano state create altre applicazioni al suo interno.

1. Disinstallare la versione precedente di `azdata`.

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

### <a name="verify-the-azdata-version"></a><a id="azdataversion"></a> Verificare la versione di azdata

Prima di distribuire un nuovo cluster Big Data, assicurarsi di usare la versione più recente di `azdata` con il parametro `--version`:

```bash
azdata --version
```

### <a name="install-the-new-release"></a>Installare la nuova versione

Dopo aver rimosso il cluster Big Data precedente e aver installato la versione più recente di `azdata`, distribuire il nuovo cluster Big Data usando le istruzioni di distribuzione correnti. Per altre informazioni, vedere [Come distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Kubernetes](deployment-guidance.md). Ripristinare quindi gli eventuali file o database necessari.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md)
