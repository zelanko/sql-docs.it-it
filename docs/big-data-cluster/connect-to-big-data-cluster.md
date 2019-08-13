---
title: Connettersi all'istanza master e a HDFS
titleSuffix: SQL Server big data clusters
description: Informazioni su come connettersi all'istanza master di SQL Server e al gateway HDFS/Spark per un cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f09763b210427c84efe75d693fee302d7048db7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958649"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Connettersi a un cluster Big Data di SQL Server con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come eseguire la connessione a un cluster Big Data di SQL Server 2019 (anteprima) da Azure Data Studio.

## <a name="prerequisites"></a>Prerequisites

- Un [cluster Big Data di SQL Server 2019](deployment-guidance.md) distribuito.
- [Strumenti per Big Data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

## <a id="master"></a> Connettersi al cluster

Per connettersi a un cluster Big Data con Azure Data Studio, stabilire una nuova connessione all'istanza master di SQL Server nel cluster. Questa procedura descrive come connettersi all'istanza master usando Azure Data Studio.

1. Dalla riga di comando trovare l'indirizzo IP dell'istanza master con il comando seguente:

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Per impostazione predefinita, il nome del cluster Big data è **mssql-cluster**, a meno che il nome non sia stato personalizzato in un file di configurazione della distribuzione. Per altre informazioni, vedere [Configurare le impostazioni di distribuzione per cluster Big Data](deployment-custom-configuration.md#clustername).

1. In Azure Data Studio premere **F1** > **Nuova connessione**.

1. In **Tipo di connessione** selezionare **Microsoft SQL Server**.

1. Digitare l'indirizzo IP dell'istanza master di SQL Server in **Nome server** (ad esempio: **\<Indirizzo IP\>,31433**).

1. Immettere il **Nome utente** e la **Password** di un account di accesso SQL.

   > [!TIP]
   > Per impostazione predefinita, il nome utente è **SA** e, se non è stata modificata, la password corrisponde alla variabile di ambiente **MSSQL_SA_PASSWORD** usata durante la distribuzione.

1. Modificare il **Nome database** di destinazione in uno dei database relazionali.

   ![Connettersi all'istanza master](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Premere **Connetti**. Verrà visualizzata la finestra **Dashboard server**.

A partire dalla versione di febbraio 2019 di Azure Data Studio, la connessione all'istanza master di SQL Server Master consente anche di interagire con il gateway HDFS/Spark. Questo significa che non è necessario usare una connessione separata per HDFS e Spark secondo la procedura descritta nella sezione successiva.

- Esplora oggetti contiene ora un nuovo nodo **Servizi dati** con supporto per le attività del cluster Big Data tramite il pulsante destro del mouse, come la creazione di nuovi notebook o l'invio di processi Spark. 
- Il nodo **Servizi dati** contiene anche una cartella **HDFS** per l'esplorazione del gateway HDFS e l'esecuzione di azioni come la creazione di una tabella esterna o l'analisi nel notebook.
- Nel **Dashboard server** per la connessione sono contenute anche schede per il **cluster Big Data di SQL Server** e **SQL Server 2019 (anteprima)** quando è installata l'estensione.

   ![Nodo Servizi dati di Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server 2019, vedere [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md).