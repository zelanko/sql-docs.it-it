---
title: Connettersi al server principale e HDFS
titleSuffix: SQL Server big data clusters
description: Informazioni su come connettersi all'istanza master di SQL Server e il gateway HDFS/Spark per un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed563fe6d0bfd69ce5dfb7484d4213bc9a47dd54
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860172"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Connettersi a un cluster di SQL Server i big data con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come connettersi a un cluster di big data di SQL Server 2019 (anteprima) da Azure Data Studio. Sono disponibili due endpoint di principale che consentono di interagire con un cluster di big data:

| Endpoint | Descrizione |
|---|---|
| Istanza di SQL Server Master | L'istanza master di SQL Server nel cluster che contiene i database relazionali di SQL Server. |
| Gateway HDFS/Spark | Accesso all'archiviazione HDFS nel cluster e la possibilità di eseguire processi Spark. |

> [!TIP]
> Con la versione di febbraio 2019 di Studio di Azure Data, automaticamente la connessione all'istanza master di SQL Server fornisce l'accesso dell'interfaccia utente per il gateway HDFS/Spark.

## <a name="prerequisites"></a>Prerequisiti

- Una distribuiti [cluster di big data di SQL Server 2019](deployment-guidance.md).
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Kubectl**

## <a id="master"></a> Connettersi al cluster

Per connettersi a un cluster di big data con Azure Data Studio, creare una nuova connessione all'istanza master di SQL Server nel cluster. I passaggi seguenti descrivono come connettersi all'istanza master usando Azure Data Studio.

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

Con la versione di febbraio 2019 di Studio di Azure Data, la connessione all'istanza master di SQL Server consente inoltre di interagire con il gateway HDFS/Spark. Ciò significa che non devi usare una connessione separata per HDFS e Spark che descrive la sezione successiva.

- Esplora oggetti contiene ora una nuova **Data Services** nodo con il pulsante destro del mouse supporto per le attività di cluster di big data, ad esempio la creazione di nuovi blocchi appunti o inviare processi spark. 
- Il **Data Services** nodo contiene inoltre un' **HDFS** cartella per l'esplorazione di HDFS e l'esecuzione di azioni, ad esempio Create External Table o analizza nel Notebook.
- Il **Dashboard del Server** per la connessione contiene anche le schede **cluster di big data di SQL Server** e **2019 Server SQL (anteprima)** quando l'estensione viene installata.

   ![Nodo servizi di Azure Data Studio Data](./media/connect-to-big-data-cluster/connect-data-services-node.png)

> [!IMPORTANT]
> Se viene visualizzato **errore sconosciuto** nell'interfaccia utente, potrebbe essere necessario [connettersi direttamente al gateway HDFS/Spark](#hdfs). Una delle cause di questo errore sono password diverse per l'istanza master di SQL Server e il gateway HDFS/Spark. Azure Data Studio presuppone che la stessa password viene usata per entrambi.
  
## <a id="hdfs"></a> Connettersi al gateway HDFS/Spark

Nella maggior parte dei casi, la connessione all'istanza master di SQL Server consente di accedere al HDFS e Spark anche tramite il **Data Services** nodo. Tuttavia, è comunque possibile creare una connessione dedicata per il **gateway HDFS/Spark** se necessario. I passaggi seguenti descrivono come connettersi con Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP del gateway di HDFS/Spark con uno dei comandi seguenti.

   ```
   kubectl get svc endpoint-security -n <your-cluster-name>
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