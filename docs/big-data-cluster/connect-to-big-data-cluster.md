---
title: Connettersi al server principale e HDFS
titleSuffix: SQL Server big data clusters
description: Informazioni su come connettersi all'istanza master di SQL Server e il gateway HDFS/Spark per un cluster di big data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d4eebad10a18b98ecc5d62ab981dcb3955ae2d29
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729082"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Connettersi a un cluster di SQL Server i big data con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come connettersi a un cluster di big data di SQL Server 2019 (anteprima) da Azure Data Studio.

## <a name="prerequisites"></a>Prerequisiti

- Una distribuiti [cluster di big data di SQL Server 2019](deployment-guidance.md).
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

## <a id="master"></a> Connettersi al cluster

Per connettersi a un cluster di big data con Azure Data Studio, creare una nuova connessione all'istanza master di SQL Server nel cluster. I passaggi seguenti descrivono come connettersi all'istanza master usando Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP dell'istanza master con il comando seguente:

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Valore predefinito è nome del cluster di big data **mssql-cluster** a meno che non il nome in un file di configurazione di distribuzione personalizzato. Per altre informazioni, vedere [configurare le impostazioni di distribuzione per i cluster di big data](deployment-custom-configuration.md#clustername).

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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data](big-data-cluster-overview.md).