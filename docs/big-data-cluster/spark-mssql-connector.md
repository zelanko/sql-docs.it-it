---
title: Connettere Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Informazioni su come usare il connettore Apache Spark per SQL Server e SQL Azure per le operazioni di lettura e scrittura in SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 3cb36c4bdddfaa97b9b6c08015308799d54cb0dc
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438073"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>Come leggere e scrivere in SQL Server da Spark usando il connettore Apache Spark per SQL Server e SQL Azure

Un modello di utilizzo chiave dei Big Data è l'elaborazione di grandi volumi di dati in Spark, seguito dalla scrittura dei dati in SQL Server per l'accesso alle applicazioni line-of-business. Questi modelli di utilizzo traggono vantaggio da un connettore che sfrutta le ottimizzazioni SQL chiave e fornisce un meccanismo di scrittura efficiente.

Questo articolo presenta una panoramica dell'interfaccia del connettore Apache Spark per SQL Server e SQL Azure e illustra come crearne un'istanza per l'uso con la modalità non AD e la modalità AD. È anche disponibile un esempio relativo all'uso del connettore Apache Spark per SQL Server e SQL Azure per leggere e scrivere nelle posizioni seguenti all'interno di un cluster Big Data:
1. Istanza master di SQL Server
1. Pool di dati di SQL Server

   ![Diagramma del connettore Apache Spark per SQL Server e SQL Azure](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-interface"></a>Interfaccia del connettore Apache Spark per SQL Server e SQL Azure

SQL Server 2019 fornisce il [**connettore Apache Spark per SQL Server e SQL Azure**](https://github.com/microsoft/sql-spark-connector) per i cluster Big Data, che usa le API di scrittura bulk di SQL Server per le operazioni di scrittura da Spark a SQL. Il connettore Apache Spark per SQL Server e SQL Azure è basato sulle API delle origini dati Spark e fornisce un'interfaccia familiare del connettore JDBC Spark. Per i parametri dell'interfaccia, vedere la [documentazione di Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). Al connettore Apache Spark per SQL Server e SQL Azure viene fatto riferimento con il nome **com.microsoft.sqlserver.jdbc.spark**. Il connettore Apache Spark per SQL Server e SQL Azure supporta due modalità di sicurezza per la connessione con SQL Server, ovvero la modalità non Active Directory (AD) e la modalità Active Directory (AD):
### <a name="non-ad-mode"></a>Modalità non AD:
Nella sicurezza in modalità non AD, ogni utente ha un nome utente e una password che devono essere specificati come parametri durante la creazione di un'istanza del connettore per eseguire operazioni di lettura e/o scrittura.
Di seguito è riportato un esempio di creazione di un'istanza del connettore per la modalità non AD:
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```
### <a name="ad-mode"></a>Modalità AD:
Nella sicurezza in modalità AD, dopo che un utente ha generato un file keytab, l'utente deve fornire `principal` e `keytab` come parametri durante la creazione di un'istanza del connettore.

In questa modalità, il driver carica il file keytab nei rispettivi contenitori degli esecutori. Quindi, gli esecutori usano il nome dell'entità e il keytab per generare un token usato per creare un connettore JDBC per la lettura/scrittura.

Di seguito è riportato un esempio di creazione di un'istanza del connettore per la modalità AD:
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

La tabella seguente descrive i parametri dell'interfaccia nuovi o modificati:

| Nome proprietà | Facoltativo | Descrizione |
|---|---|---|
| **isolationLevel** | Sì | Descrive il livello di isolamento della connessione. Il valore predefinito per il connettore è **READ_COMMITTED** |

Il connettore usa le API di scrittura bulk di SQL Server. I parametri di scrittura bulk possono essere passati come parametri facoltativi dall'utente e vengono passati così come sono dal connettore all'API sottostante. Per altre informazioni sulle operazioni di scrittura bulk, vedere [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-sample"></a>Esempio di connettore Apache Spark per SQL Server e SQL Azure
Nell'esempio vengono eseguite le attività seguenti:

- Lettura di un file da HDFS ed esecuzione di alcune operazioni di elaborazione di base.
- Scrittura del dataframe in un'istanza master di SQL Server come tabella SQL e quindi lettura della tabella in un dataframe.
- Scrittura del dataframe in un pool di dati di SQL Server come tabella SQL esterna e quindi lettura della tabella esterna in un dataframe.
### <a name="prerequisites"></a>Prerequisiti

- Un [cluster Big Data di SQL Server](deploy-get-started.md).

- [Azure Data Studio](https://aka.ms/getazuredatastudio).

### <a name="create-the-target-database"></a>Creare il database di destinazione

1. Aprire Azure Data Studio e [connettersi all'istanza master di SQL Server del cluster Big Data](connect-to-big-data-cluster.md).

1. Creare una nuova query ed eseguire il comando seguente per creare un database di esempio denominato **MyTestDatabase**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

### <a name="load-sample-data-into-hdfs"></a>Caricare i dati di esempio in HDFS

1. Scaricare [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) nel computer locale.

1. Avviare Azure Data Studio e [connettersi al cluster Big Data](connect-to-big-data-cluster.md).

1. Fare clic con il pulsante destro del mouse sulla cartella HDFS nel cluster Big data e scegliere **Nuova directory**. Assegnare alla directory il nome **spark_data**.

1. Fare clic con il pulsante destro del mouse sulla directory **spark_data** e scegliere **Carica file**. Caricare il file **AdultCensusIncome.csv**.

   ![File CSV AdultCensusIncome](./media/spark-mssql-connector/spark_data.png)

### <a name="run-the-sample-notebook"></a>Eseguire il notebook di esempio

Per illustrare l'uso del connettore Apache Spark per SQL Server e SQL Azure con questi dati in modalità non AD, è possibile scaricare un notebook di esempio, aprirlo in Azure Data Studio ed eseguire ogni blocco di codice. Per altre informazioni sull'uso dei notebook, vedere [Come usare i notebook in SQL Server](../azure-data-studio/notebooks-guidance.md).

1. Da una riga di comando di PowerShell o dalla shell Bash, eseguire il comando seguente per scaricare il notebook di esempio **mssql_spark_connector_non_ad_pyspark.ipynb**:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector_non_ad_pyspark.ipynb"
   ```

1. In Azure Data Studio aprire il file del notebook di esempio. Verificare che sia connesso al gateway HDFS/Spark per il cluster Big Data.

1. Eseguire ogni cella di codice nell'esempio per visualizzare l'utilizzo del connettore Apache Spark per SQL Server e SQL Azure.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Come distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Kubernetes](deployment-guidance.md)

Commenti o suggerimenti sulle funzionalità per i cluster Big Data di SQL Server? [Lasciare una nota nella pagina per l'invio di commenti e suggerimenti per i cluster Big Data di SQL Server](https://aka.ms/sql-server-bdc-feedback).
