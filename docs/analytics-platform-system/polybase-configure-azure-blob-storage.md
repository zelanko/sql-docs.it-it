---
title: Configurare PolyBase per accedere a dati esterni in archiviazione Blob di Azure | Microsoft Docs
description: Viene illustrato come configurare PolyBase in Parallel Data Warehouse per la connessione a esterna Hadoop.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82c57ef57a01cabf2786c71fc53aed3660289451
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960285"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Configurare PolyBase per accedere a dati esterni in archiviazione Blob di Azure

L'articolo illustra come usare PolyBase in un'istanza di SQL Server per eseguire query sui dati esterni nell'archiviazione Blob di Azure.

> [!NOTE]
> I punti di accesso supporta attualmente solo archiviazione con ridondanza locale (LRS) Blob di Azure di standard utilizzo generico v1.

## <a name="prerequisites"></a>Prerequisiti

 - Archiviazione Blob di Azure nella sottoscrizione.
 - Un contenitore creato nella risorsa di archiviazione Blob di Azure.

### <a name="configure-azure-blob-storage-connectivity"></a>Configurare la connettività di archiviazione Blob di Azure

Innanzitutto, configurare i punti di accesso per usare l'archiviazione Blob di Azure.

1. Eseguire [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) con 'hadoop connectivity' impostato su un provider di archiviazione Blob di Azure. Per trovare il valore per i provider, vedere [Configurazione della connettività di PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Riavviare area APS usando pagina stato del servizio sul [Appliance Configuration Manager](launch-the-configuration-manager.md).
  
## <a name="configure-an-external-table"></a>Configurare una tabella esterna

Per eseguire query sui dati nell'archiviazione Blob di Azure, è necessario definire una tabella esterna da utilizzare nella query Transact-SQL. Le procedure seguenti descrivono come configurare la tabella esterna.

1. Creare una chiave master nel database. È necessario crittografare il segreto della credenziale.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Creare una credenziale con ambito database per l'archiviazione Blob di Azure.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. Creare un'origine dati esterna con [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. Creare un formato di file esterno con [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. Creare una tabella esterna che punta ai dati archiviati in Archiviazione di Azure con [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). In questo esempio i dati esterni contengono dati di sensori di auto.

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = AzureStorage,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

1. Creare statistiche per una tabella esterna.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>Query PolyBase

PolyBase è adatto per assolvere a una triplice funzione:  
  
- Query ad hoc su tabelle esterne.  
- Importazione di dati.  
- Esportazione di dati.  

Le query seguenti forniscono esempi con dati fittizi di sensori di auto.

### <a name="ad-hoc-queries"></a>Query ad hoc  

La seguente query ad hoc join relazionale con i dati nell'archiviazione Blob di Azure. Seleziona i clienti che hanno unità più veloce rispetto a 35 km/h, aggiunta ai dati dei clienti strutturati archiviati in SQL Server con dati dei sensori di auto archiviati in archiviazione Blob di Azure.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>Importazione di dati  

La query seguente importa i dati esterni in punti di accesso. In questo esempio Importa i dati per i driver veloci in punti di accesso per eseguire un'analisi più dettagliata. Per migliorare le prestazioni, sfrutta la tecnologia Columnstore in punti di accesso.  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>Esportazione di dati  

La query seguente esporta i dati dai punti di accesso all'archiviazione Blob di Azure. Può essere utilizzato per archiviare i dati relazionali in Azure Blob storage mentre si è ancora in grado di eseguire una query.

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>Visualizzare gli oggetti PolyBase in SSDT  

In SQL Server Data Tools, le tabelle esterne vengono visualizzate in una cartella distinta **le tabelle esterne**. Le origini dati esterne e i formati di file esterni si trovano nelle sottocartelle in **External Resources**.  
  
![Oggetti PolyBase in SSDT](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](../relational-databases/polybase/polybase-guide.md). 

