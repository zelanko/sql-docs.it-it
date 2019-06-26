---
title: Connettere Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Informazioni su come usare il connettore Spark MSSQL in Spark per leggere e scrivere in SQL Server.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8172bc1d2b831d0cbeaab72bead283853b22cc
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388626"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>Come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL

Un modello di utilizzo principali dei big data è l'elaborazione dati di volumi elevati in Spark, seguita dalla scrittura dei dati a SQL Server per l'accesso alle applicazioni line-of-business. Questi modelli di utilizzo trarre vantaggio da un connettore che utilizza ottimizzazioni principali di SQL e fornisce un meccanismo efficiente di scrittura.

Questo articolo fornisce un esempio di come usare il connettore MSSQL Spark per leggere e scrivere nelle posizioni seguenti all'interno di un cluster di big data:

1. L'istanza master di SQL Server
1. Il pool di dati di SQL Server

   ![Diagramma di connettore Spark MSSQL](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

L'esempio esegue le attività seguenti:

- Leggere un file da HDFS ed eseguire alcune operazioni di elaborazione di base.
- Scrivere il frame di dati in un'istanza di SQL Server master come una tabella SQL e quindi leggere la tabella in un frame di dati.
- Scrivere il frame di dati in un pool di dati di SQL Server come una tabella esterna a SQL e quindi leggere la tabella esterna a un dataframe.

## <a name="mssql-spark-connector-interface"></a>Interfaccia Connector Spark MSSQL

Anteprima di SQL Server 2019 fornisce il **connettore Spark MSSQL** per big data cluster che usa bulk di SQL Server scrittura delle API per Spark e di scritture SQL. Connettore Spark MSSQL è basato sull'origine dati di Spark le API e offre un'interfaccia familiare di connettore JDBC Spark. Per i parametri dell'interfaccia, vedere [documentazione di Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). Il connettore Spark per MSSQL fa riferimento il nome **com.microsoft.sqlserver.jdbc.spark**.

Nella tabella seguente vengono descritti i parametri dell'interfaccia che sono state modificate o sono nuovi:

| Nome proprietà | Facoltativo | Descrizione |
|---|---|---|
| **isolationLevel** | Yes | Descrive il livello di isolamento della connessione. Il valore predefinito per il connettore MSSQLSpark è **READ_COMMITTED** |

Il connettore Usa SQL Server Bulk scrittura delle API. Le operazioni di scrittura in blocco i parametri possono essere passati come parametri facoltativi dall'utente e vengono passati come-sia dal connettore all'API sottostante. Per altre informazioni sul blocco di operazioni di scrittura, vedere [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="prerequisites"></a>Prerequisiti

- Oggetto [cluster di big data di SQL Server](deploy-get-started.md).

- [Azure Data Studio](../azure-data-studio/download.md).

## <a name="create-the-target-database"></a>Creare il database di destinazione

1. Aprire Azure Data Studio, e [connettersi all'istanza master di SQL Server del cluster di big data](connect-to-big-data-cluster.md).

1. Creare una nuova query ed eseguire il comando seguente per creare un database di esempio denominato **MyTestDatabase**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>Caricare i dati di esempio in HDFS

1. Scaricare [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) nel computer locale.

1. Avviare Data Studio di Azure, e [connettersi al cluster di big data](connect-to-big-data-cluster.md).

1. Pulsante destro del mouse sulla cartella HDFS nel cluster di big data e selezionare **nuova directory**. Nome della directory **spark_data**.

1. Fare clic con il pulsante destro sul **spark_data** directory, quindi selezionare **caricare file**. Caricare il **AdultCensusIncome.csv** file.

   ![File CSV AdultCensusIncome](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>Eseguire il notebook di esempio

Per illustrare l'uso del connettore Spark MSSQL con questi dati, è possibile scaricare un notebook di esempio, aprirlo in Azure Data Studio ed eseguire ogni blocco di codice. Per altre informazioni sull'uso di notebook, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md).

1. Dalla riga di comando di PowerShell o bash, eseguire il comando seguente per scaricare il **mssql_spark_connector.ipynb** notebook di esempio:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark_to_sql/mssql_spark_connector.ipynb"
   ```

1. In Azure Data Studio, aprire il file di notebook di esempio. Verificare che sia connesso al Gateway HDFS/Spark per il cluster di big data.

1. Eseguire ogni cella di codice nell'esempio per visualizzare l'utilizzo del connettore Spark MSSQL.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md)