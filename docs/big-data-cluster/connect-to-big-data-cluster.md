---
title: Connettersi al server principale e HDFS
titleSuffix: SQL Server 2019 big data clusters
description: Informazioni su come connettersi all'istanza master di SQL Server e il gateway HDFS/Spark per un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9129b436f33092054a19b858fa5bcdb8aebadec2
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241822"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Connettersi a un cluster di SQL Server i big data con Azure Data Studio

Questo articolo descrive come connettersi a un cluster di big data di SQL Server 2019 (anteprima) da Azure Data Studio.

## <a name="prerequisites"></a>Prerequisiti

- Una distribuiti [cluster di big data di SQL Server 2019](deployment-guidance.md).
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Kubectl**

## <a name="connect-to-the-cluster"></a>Connettersi al cluster

Quando ci si connette a un cluster di big data, è possibile connettersi all'istanza master di SQL Server o al gateway HDFS/Spark. Le sezioni seguenti illustrano come connettersi a ognuna.

## <a id="master"></a> Istanza master

L'istanza master di SQL Server è un'istanza di SQL Server tradizionale che contiene i database relazionali di SQL Server. I passaggi seguenti descrivono come connettersi all'istanza master usando Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP dell'istanza master con il comando seguente:

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. In Azure Data Studio, premere **F1** > **nuova connessione**.

1. Nelle **tipo di connessione**, selezionare **Microsoft SQL Server**.

1. Digitare l'indirizzo IP dell'istanza master di SQL Server nella **nome Server** (ad esempio: **\<Indirizzo IP\>, 31433**).

1. Immettere un account di accesso SQL **nome utente** e **Password**.

   > [!TIP]
   > Per impostazione predefinita, è il nome utente **SA** e, a meno che non modificato, la password corrisponde al comando il **MSSQL_SA_PASSWORD** variabile di ambiente usate durante la distribuzione.

1. Modificare la destinazione **nome del Database** a uno dei database relazionali.

   ![Connettersi all'istanza master](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Premere **Connect**e il **Dashboard di Server** dovrebbe essere visualizzato.

## <a id="hdfs"></a> Gateway HDFS/Spark

Il **gateway HDFS/Spark** consente di connettersi per funzionare con il pool di archiviazione HDFS e per eseguire processi Spark. I passaggi seguenti descrivono come connettersi con Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP del gateway di HDFS/Spark con uno dei comandi seguenti.
   
   **Distribuzioni di servizio contenitore di AZURE:**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **Le distribuzioni non-AKS**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. In Azure Data Studio, premere **F1** > **nuova connessione**.

1. Nelle **tipo di connessione**, selezionare **cluster di big data di SQL Server**.

   > [!TIP]
   > Se non viene visualizzato il **cluster di big data di SQL Server** connessione digitare, assicurarsi di avere installato la [estensione SQL Server 2019](../azure-data-studio/sql-server-2019-extension.md) e che Data Studio di Azure è stato riavviato dopo l'estensione completata l'installazione.

1. Digitare l'indirizzo IP del cluster di big data nelle **nome Server** (non specificare una porta).

1. Immettere `root` per il **utente** e specificare il **Password** per il cluster di big data.

   ![Connettersi al gateway HDFS/Spark](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > Per impostazione predefinita, è il nome utente **radice** e la password corrisponde al comando il **KNOX_PASSWORD** variabile di ambiente usate durante la distribuzione.

1. Premere **Connect**e il **Dashboard di Server** dovrebbe essere visualizzato.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data](big-data-cluster-overview.md).