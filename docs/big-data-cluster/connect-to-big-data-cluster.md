---
title: Connettersi al server principale e HDFS
titleSuffix: SQL Server big data clusters
description: Informazioni su come connettersi all'istanza master di SQL Server e il gateway HDFS/Spark per un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3305990935c5d4c6077caa062184b0150aa83d6b
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994061"
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
   kubectl get svc master-svc-external -n <your-cluster-name>
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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di SQL Server 2019 dei big data, vedere [quali sono i cluster di SQL Server 2019 dei big data](big-data-cluster-overview.md).