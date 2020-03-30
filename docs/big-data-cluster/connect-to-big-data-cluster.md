---
title: Connettersi a cluster Big Data master e HDFS
description: Informazioni su come connettersi all'istanza master di SQL Server e al gateway HDFS/Spark per un cluster Big Data di SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c5ba08a492be621e4b1f8871bdfcb49983af26d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79285985"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Connettersi a un cluster Big Data di SQL Server con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come connettersi a un[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] da Azure Data Studio.

## <a name="prerequisites"></a>Prerequisiti

- Un [cluster Big Data di SQL Server 2019](deployment-guidance.md) distribuito.
- [Strumenti per Big Data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**
   - **azdata**

## <a name="connect-to-the-cluster"></a><a id="master"></a> Connettersi al cluster

Per connettersi a un cluster Big Data con Azure Data Studio, stabilire una nuova connessione all'istanza master di SQL Server nel cluster. Ecco come.

1. Individuare l'istanza master di SQL Server:

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > Per altre informazioni su come recuperare gli endpoint, vedere [Recuperare gli endpoint](deployment-guidance.md#endpoints).

1. In Azure Data Studio premere **F1** > **Nuova connessione**.

1. In **Tipo di connessione** selezionare **Microsoft SQL Server**.

1. Digitare il nome dell'endpoint trovato per l'istanza master di SQL Server nella casella di testo **Nome server**, ad esempio: **\<Indirizzo_IP\>, 31433**. 

1. Scegliere il tipo di autenticazione. Per l'istanza master di SQL Server in esecuzione all'interno di cluster Big Data, sono supportati solo i tipi **Autenticazione di Windows** e **Account di accesso SQL**. 

1. Se si usa l'account di accesso SQL, immettere l'account di accesso SQL: **Nome utente** e **Password**.

   > [!TIP]
   > Per impostazione predefinita, durante la distribuzione di cluster Big Data il nome utente **SA** è disabilitato. Durante la distribuzione viene eseguito il provisioning di un nuovo utente sysadmin con nome e password corrispondenti alle variabili di ambiente **AZDATA_USERNAME** e **AZDATA_PASSWORD**, impostate prima o durante a distribuzione.

1. Modificare il **Nome database** di destinazione in uno dei database relazionali.

   ![Connettersi all'istanza master](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Premere **Connetti**. Verrà visualizzata la finestra **Dashboard server**.

A partire dalla versione di febbraio 2019 di Azure Data Studio, la connessione all'istanza master di SQL Server Master consente anche di interagire con il gateway HDFS/Spark. Questo significa che non è necessario usare una connessione separata per HDFS e Spark secondo la procedura descritta nella sezione successiva.

- Esplora oggetti contiene ora un nuovo nodo **Servizi dati** con supporto per le attività del cluster Big Data tramite il pulsante destro del mouse, come la creazione di nuovi notebook o l'invio di processi Spark. 
- Il nodo **Servizi dati** contiene anche una cartella **HDFS** che consente di esplorare il contenuto del sistema HDFS e di eseguire attività comuni che interessano HDFS, ad esempio la creazione di una tabella esterna o l'apertura di un notebook per l'analisi del contenuto di HDFS.
- Nel **Dashboard server** per la connessione sono contenute anche schede per il **cluster Big Data di SQL Server** e **SQL Server 2019** quando è installata l'estensione.

   ![Nodo Servizi dati di Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
