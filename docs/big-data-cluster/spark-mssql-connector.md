---
title: Connettere Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Informazioni su come usare il connettore Spark MSSQL in Spark per leggere e scrivere in SQL Server.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 12343c2000bca3ae90e62c8702636859a808a580
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994182"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>Come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL

Un modello di utilizzo principali dei big data è l'elaborazione dati di volumi elevati in Spark, seguita dalla scrittura dei dati a SQL Server per l'accesso alle applicazioni line-of-business. Questi modelli di utilizzo trarre vantaggio da un connettore che utilizza ottimizzazioni principali di SQL e fornisce un meccanismo efficiente di scrittura.

I cluster di big Data offre un nuovo connettore MSSQL Spark che Usa SQL Server in blocco scrittura delle API per un efficiente Spark in scrittura SQL. Questo articolo fornisce un esempio di come leggere e scrivere in SQL Server da Spark usando il connettore Spark MSSQL. In questo esempio, i dati vengono letti da HDFS in un cluster di big data, di elaborazione Spark e quindi scritto per l'istanza master di SQL Server nel cluster usando il nuovo connettore Spark MSSQL.

## <a name="mssql-spark-connector-interface"></a>Interfaccia Connector Spark MSSQL

Connettore Spark MSSQL è basato sull'origine dati di Spark le API e offre un'interfaccia familiare di connettore JDBC Spark. Per i parametri dell'interfaccia, vedere [documentazione di Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). Il connettore Spark per MSSQL fa riferimento il nome **com.microsoft.sqlserver.jdbc.spark**.

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

1. In Azure Data Studio, fare doppio clic sulla cartella HDFS nel cluster di big data e selezionare **nuova directory**. Nome della directory **spark_data**.

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