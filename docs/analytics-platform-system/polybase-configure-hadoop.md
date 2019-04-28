---
title: Configurare PolyBase per l'accesso a dati esterni in Hadoop | Microsoft Docs
description: Viene illustrato come configurare PolyBase in Parallel Data Warehouse per la connessione a esterna Hadoop.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 94c8d399f7b6ba36b48b4c5aa7f35bbd67ce6909
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678645"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Configurare PolyBase per l'accesso a dati esterni in Hadoop

L'articolo illustra come usare PolyBase in un'appliance APS per eseguire query sui dati esterni in Hadoop.

## <a name="prerequisites"></a>Prerequisiti

PolyBase supporta due provider di Hadoop, Hortonworks Data Platform (HDP) e Cloudera Distributed Hadoop (CDH). Hadoop segue il modello "principale.secondaria.versione" per le nuove versioni e sono supportate tutte le versioni all'interno di una versione principale e secondaria supportata. Sono supportati i provider Hadoop seguenti:
 - Hortonworks HDP 1.3 su Linux/Windows Server  
 - Hortonworks HDP 2.1-2.6 su Linux
 - Hortonworks HDP 2.1 - 2.3 su Windows Server  
 - Cloudera CDH 4.3 su Linux  
 - Cloudera CDH 5.1-5.5, 5.9-5.13 su Linux

### <a name="configure-hadoop-connectivity"></a>Configurare la connettività Hadoop

Innanzitutto, configurare i punti di accesso per l'uso di specifici provider di Hadoop.

1. Eseguire [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) con 'hadoop connectivity' e impostare un valore appropriato per il provider. Per trovare il valore per il provider, vedere [Configurazione della connettività di PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md). 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Riavviare area APS usando pagina stato del servizio sul [Appliance Configuration Manager](launch-the-configuration-manager.md).
  
## <a id="pushdown"></a> Abilitare il calcolo con distribuzione  

Per migliorare le prestazioni delle query, abilitare il calcolo con distribuzione nel cluster Hadoop:  
  
1. Aprire una connessione desktop remoto al nodo di controllo di PDW.

2. Trovare il file **yarn-Site. XML** nel nodo di controllo. In genere il percorso è:  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. Nel computer Hadoop trovare il file analogo nella directory di configurazione Hadoop. Nel file trovare e copiare il valore della chiave di configurazione yarn.application.classpath.  
  
4. Nel nodo di controllo, nel **file yarn.site.xml** trovare il **CLASSPATH** proprietà. Incollare il valore dal computer Hadoop nell'elemento valore.  
  
5. Per tutte le versioni di CDH 5.X sarà necessario aggiungere i parametri di configurazione mapreduce.application.classpath alla fine del file yarn.site.xml o nel file mapred-site.xml. HortonWorks include queste configurazioni all'interno delle configurazioni yarn.application.classpath. Vedere [Configurazione di PolyBase](../relational-databases/polybase/polybase-configuration.md) per alcuni esempi.

## <a name="configure-an-external-table"></a>Configurare una tabella esterna

Per eseguire query sui dati nell'origine dati Hadoop, è necessario definire una tabella esterna da usare in query Transact-SQL. Le procedure seguenti descrivono come configurare la tabella esterna.

1. Creare una chiave master nel database. È necessario crittografare il segreto della credenziale.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. Creare credenziali con ambito database per i cluster Hadoop con protezione Kerberos.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. Creare un'origine dati esterna con [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

4. Creare un formato di file esterno con [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. Creare una tabella esterna che punta ai dati archiviati in Hadoop con [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). In questo esempio i dati esterni contengono dati di sensori di auto.

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
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. Creare statistiche per una tabella esterna.

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

La query ad hoc seguente crea un join relazionale con dati Hadoop. Seleziona i clienti che hanno unità più veloce rispetto a 35 km/h, aggiunta ai dati dei clienti strutturati archiviati nella piattaforma di strumenti analitici con dati dei sensori di auto archiviati in Hadoop.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
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

La query seguente esporta i dati dai punti di accesso ad Hadoop. Può essere utilizzato per archiviare dati relazionali di Hadoop while comunque in grado di eseguire una query.

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
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

Per vedere le impostazioni di sicurezza Hadoop [configurare la sicurezza Hadoop](polybase-configure-hadoop-security.md).<br>
Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](../relational-databases/polybase/polybase-guide.md). 
 
