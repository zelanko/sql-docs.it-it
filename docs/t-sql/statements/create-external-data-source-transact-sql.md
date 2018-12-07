---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b3375af07fc7231321c96c2aa03d95dbbdc6709f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506406"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea un'origine dati esterna per PolyBase o query di database elastico. La sintassi presenta numerose differenze a seconda dello scenario. Un'origine dati esterna creata per PolyBase non può essere usata per query di database elastico.  Analogamente, un'origine dati esterna creata per le query di database elastico non può essere usata per PolyBase e così via. 
  
> [!NOTE]  
>  PolyBase è supportata solo in SQL Server 2016 (o versioni successive), Azure SQL Data Warehouse e Parallel Data Warehouse. Le query di database elastico sono supportate solo nel database SQL di Azure v12 o versioni successive.  
  
 Per gli scenari di PolyBase, l'origine dati esterna è un file system Hadoop (HDFS), un contenitore del BLOB di archiviazione di Azure o Azure Data Lake Store. Per altre informazioni, vedere [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Introduzione a PolyBase).  
  
 Per gli scenari di query di database elastico, l'origine esterna è un gestore mappe partizioni (nel database SQL di Azure) o un database remoto (nel database SQL di Azure).  Usare [sp_execute_remote &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) dopo aver creato un'origine dati esterna. Per altre informazioni, vedere [Query di database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  L'origine dati esterna dell'archiviazione BLOB di Azure supporta la sintassi di `BULK INSERT` e `OPENROWSET` ed è diversa dall'archiviazione BLOB di Azure per PolyBase.
    
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Azure Data Lake Store Gen 2
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE ABFS 
WITH
(
              TYPE=HADOOP,
              LOCATION='abfs://<container>@<AzureDataLake account_name>.dfs.core.windows.net',
              CREDENTIAL=ABFS_Credemt
);
GO


-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]
        [, CREDENTIAL = credential_name]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source   
-- (on Parallel Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argomenti  
 *data_source_name* Specifica il nome definito dall'utente per l'origine dati. Il nome deve essere univoco all'interno del database in SQL Server, nel database SQL di Azure e in Azure SQL Data Warehouse. Il nome deve essere univoco all'interno del server in Parallel Data Warehouse.
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Specifica il tipo dell'origine dati. Usare HADOOP quando l'origine dati esterna è Hadoop o l'archiviazione BLOB di Azure per Hadoop. Usare SHARD_MAP_MANAGER durante la creazione di un'origine dati esterna per una query di database elastico per il partizionamento orizzontale nel database SQL di Azure. Usare RDBMS con le origini dati esterne per le query tra database con query di database elastico nel database SQL di Azure.  Usare BLOB_STORAGE durante l'esecuzione di operazioni bulk con [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
LOCATION = \<location_path> **HADOOP**    
Per HADOOP, specifica l'URI (Uniform Resource Indicator) per un cluster Hadoop.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: nome o indirizzo IP del computer del cluster Hadoop Namenode.  
port: porta IPC di Namenode. È indicata dal parametro di configurazione fs.default.name in Hadoop. Se il valore non è specificato, viene usato il valore 8020 per impostazione predefinita.  
Esempio: `LOCATION = 'hdfs://10.10.10.10:8020'`

Per l'archiviazione BLOB di Azure con Hadoop, specifica l'URI per la connessione all'archiviazione BLOB di Azure.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]: specifica il protocollo dell'archiviazione BLOB di Azure. [s] è facoltativa e specifica una connessione SSL protetta; i dati inviati da SQL Server sono crittografati in modo sicuro tramite il protocollo SSL. È consigliabile usare 'wasbs' anziché 'wasb'. Si noti che il percorso può usare asv[s] anziché wasb[s]. La sintassi asv[s] è deprecata e verrà rimossa da una delle prossime versioni.  
container: specifica il nome del contenitore dell'archiviazione BLOB di Azure. Per specificare il contenitore radice dell'account di archiviazione di un dominio, usare il nome di dominio anziché il nome del contenitore. Poiché i contenitori radice sono di sola lettura, i dati non possono essere riscritti nel contenitore.  
account_name: nome di dominio completo (FQDN) dell'account di archiviazione di Azure.  
Esempio: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Per Azure Data Lake Store, il percorso specifica l'URI per la connessione ad Azure Data Lake Store.



**SHARD_MAP_MANAGER**   
 Per SHARD_MAP_MANAGER, specifica il nome del server logico che ospita il gestore mappe partizioni nel database SQL di Azure o in un database SQL Server in una macchina virtuale di Azure.
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

Per un'esercitazione dettagliata, vedere [Getting started with elastic queries for sharding (horizontal partitioning)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/) (Introduzione alle query di database elastico per il partizionamento orizzontale).
  
**RDBMS**   
Per RDBMS, specifica il nome del server logico del database remoto nel database SQL di Azure.  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
Per un'esercitazione dettagliata su RDBMS, vedere [Introduzione alle query tra database (partizionamento verticale)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Questo tipo viene usato solo per le operazioni bulk. `LOCATION` deve essere l'URL valido del contenitore e dell'archivio BLOB di Azure. Non inserire **/**, nome file o parametri di firma per l'accesso condiviso alla fine dell'URL `LOCATION`. `CREADENTIAL` è obbligatorio se l'oggetto BLOB non è pubblico. Ad esempio 
```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH (  TYPE = BLOB_STORAGE, 
        LOCATION = 'https://****************.blob.core.windows.net/invoices', 
        CREDENTIAL= MyAzureBlobStorageCredential    --> CREDENTIAL is not required if a blob has public access!
);
```
La credenziale usata deve essere creata con `SHARED ACCESS SIGNATURE` come identità, non deve avere `?` iniziale nel token di firma di accesso condiviso, deve avere almeno un'autorizzazione di lettura per il file da caricare (ad esempio, `srt=o&sp=r`), e il periodo di scadenza deve essere valido. Tutte le date sono in formato UTC. Ad esempio
```sql
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';
```

Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Per un esempio di accesso all'archiviazione BLOB, vedere l'esempio F di [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 
>[!NOTE] 
>Per caricare dati dall'archiviazione BLOB di Azure in SQL Data Warehouse, il segreto deve essere la chiave di archiviazione di Azure.

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 Specifica il percorso di gestione risorse di Hadoop. Quando specificato, Query Optimizer può effettuare una scelta in base ai costi e pre-elaborare i dati di una query PolyBase usando le funzionalità di calcolo di Hadoop con MapReduce. Il pushdown dei predicati può ridurre notevolmente il volume dei dati trasferiti tra Hadoop e SQL e pertanto migliorare le prestazioni delle query.  
  
 Quando non viene specificato, il push del calcolo in Hadoop è disabilitato per le query PolyBase.  
 
Se la porta non è specificata, il valore predefinito viene determinato mediante l'impostazione corrente della configurazione 'hadoop connectivity'.

|Connettività Hadoop|Porta di gestione risorse predefinita|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Per un elenco completo delle distribuzioni di Hadoop e delle versioni supportate da ogni valore di connettività, vedere [Configurazione della connettività di PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  Il valore RESOURCE_MANAGER_LOCATION è una stringa e non viene convalidato quando si crea l'origine dati esterna. L'immissione di un valore non corretto può causare ritardi futuri durante l'accesso al percorso.  
  
 Esempi di Hadoop:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. 2.3 in Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 in Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2, 2.3 in Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Hortonworks HDP 1.3 in Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Cloudera 4.3 in Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Cloudera 5.1 - 5.11 in Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 Specifica una credenziale con ambito database per l'autenticazione nell'origine dati esterna. Per un esempio, vedere [C. Creare un'origine dati esterna dell'archiviazione BLOB di Azure](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Per creare una credenziale, vedere [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Si noti che CREDENTIAL non è obbligatorio per i set di dati pubblici che consentono l'accesso anonimo. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 Nome del database che svolge la funzione di gestore mappe partizioni (per SHARD_MAP_MANAGER) o di database remoto (per RDBMS).  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Solo per SHARD_MAP_MANAGER. Nome della mappa partizioni. Per altre informazioni sulla creazione di una mappa partizioni, vedere [Introduzione alla query di database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>Note specifiche su PolyBase  
Per un elenco completo delle origini dati esterne supportate, vedere [Configurazione della connettività di PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Per usare PolyBase, è necessario creare i tre oggetti seguenti:  
  
-   Un'origine dati esterna.  
  
-   Un formato di file esterno e  
  
-   Una tabella esterna che fa riferimento all'origine dati esterna e al formato di file esterno.  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione CONTROL nel database in SQL DW, SQL Server, APS 2016 e nel database SQL.

> [!IMPORTANT]  
>  Nelle versioni precedenti di PDW creare le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE richieste dell'origine dati esterna.
  
  
## <a name="error-handling"></a>Gestione degli errori  
 Se le origini dati Hadoop esterne non sono coerenti nella definizione di RESOURCE_MANAGER_LOCATION, si verifica un errore di runtime. Per questa ragione, non è possibile specificare due origini dati esterne che fanno riferimento allo stesso cluster Hadoop e specificare un percorso di gestione delle risorse solo per una delle due origini dati.  
  
 Il motore SQL non verifica l'esistenza dell'origine dati esterna quando viene creato l'oggetto origine dati esterna. Se l'origine dati non esiste durante l'esecuzione di query, si verifica un errore.  
  
## <a name="general-remarks"></a>Osservazioni generali  
Per PolyBase, l'origine dati esterna è con ambito database in SQL Server e SQL Data Warehouse. In Parallel Data Warehouse è con ambito server.
  
Per PolyBase, quando viene definito RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION, Query Optimizer prenderà in considerazione l'ottimizzazione di ogni query avviando un processo di riduzione delle mappe nell'origine Hadoop esterna ed eseguendo il pushdown del calcolo. Questa decisione è interamente basata sui costi.  

Per garantire l'esito positivo delle query di PolyBase in caso di failover del NameNode di Hadoop, può essere utile usare un indirizzo IP virtuale per il NameNode del cluster Hadoop. Se non si usa un indirizzo IP virtuale per il NameNode di Hadoop, in caso di failover del NameNode di Hadoop sarà necessario eseguire ALTER EXTERNAL DATA SOURCE in modo che l'oggetto punti alla nuova posizione.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 Tutte le origini dati definite nello stesso percorso di cluster Hadoop devono usare la stessa impostazione per RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION. Se è presente un'incoerenza, si verifica un errore di runtime.  
  
 Se il cluster Hadoop è configurato con un nome e l'origine dati esterna usa l'indirizzo IP per il percorso del cluster, PolyBase deve essere comunque in grado di risolvere il nome del cluster quando viene usata l'origine dati. Per risolvere il nome, è necessario abilitare un server d'inoltro DNS.  
  
## <a name="locking"></a>Utilizzo di blocchi  
 Acquisisce un blocco condiviso sull'oggetto EXTERNAL DATA SOURCE.  
  
##  <a name="examples"></a> Esempi: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Creare un'origine dati esterna per fare riferimento a Hadoop  
Per creare un'origine dati esterna per fare riferimento al cluster Hortonworks o Cloudera Hadoop, specificare il nome del computer o l'indirizzo IP del Namenode Hadoop e la porta.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Creare un'origine dati esterna per fare riferimento a Hadoop con il pushdown abilitato  
Specificare l'opzione RESOURCE_MANAGER_LOCATION per abilitare il push-down del calcolo in Hadoop per le query PolyBase. Dopo l'abilitazione, PolyBase usa una decisione basata sui costi per determinare se eseguire il push del calcolo delle query in Hadoop o spostare tutti i dati per elaborare la query in SQL Server.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Creare un'origine dati esterna per fare riferimento a Hadoop con protezione Kerberos  
Per verificare se il cluster Hadoop è protetto tramite Kerberos, controllare il valore della proprietà hadoop.security.authentication nel file core-site.xml di Hadoop. Per fare riferimento a un cluster Hadoop protetto tramite Kerberos, è necessario specificare una credenziale con ambito database che contiene il nome utente e la password di Kerberos. La chiave master del database viene usata per crittografare il segreto della credenziale con ambito database. 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Creare un'origine dati esterna per fare riferimento all'archiviazione BLOB di Azure
Per creare un'origine dati esterna per fare riferimento al contenitore dell'archiviazione BLOB di Azure, specificare l'URI dell'archiviazione BLOB di Azure e una credenziale con ambito database che contiene la chiave dell'account di archiviazione di Azure.

In questo esempio, l'origine dati esterna è un contenitore dell'archiviazione BLOB di Azure denominato dailylogs nell'account di archiviazione di Azure denominato myaccount. L'origine dati esterna dell'archiviazione di Azure è destinata al solo trasferimento dei dati e non supporta il pushdown dei predicati.

Questo esempio illustra come creare la credenziale con ambito database per l'autenticazione nell'archiviazione di Azure. Specificare la chiave dell'account di archiviazione di Azure nel segreto della credenziale di database. È possibile specificare qualsiasi stringa nell'identità della credenziale con ambito database, poiché non viene usata per l'autenticazione nell'archiviazione di Azure. La credenziale viene quindi usata nell'istruzione che crea un'origine dati esterna.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Esempi: database SQL di Azure

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Creare un'origine dati esterna del gestore mappe partizioni
Per creare un'origine dati esterna per fare riferimento a SHARD_MAP_MANAGER, specificare il nome del server logico che ospita il gestore mappe partizioni nel database SQL di Azure o in un database SQL Server in una macchina virtuale di Azure.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. Creare un'origine dati esterna RDBMS
Per creare un'origine dati esterna per fare riferimento a un RDBMS, specificare il nome del server logico del database remoto nel database SQL di Azure.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>Esempi: Azure SQL Data Warehouse

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. Creare un'origine dati esterna per fare riferimento ad Azure Data Lake Store
La connettività di Azure Data Lake Store è basata sull'URI ADLS e sul servizio dell'applicazione di Azure Active Directory. La documentazione relativa alla creazione di questa applicazione è disponibile in [Autenticazione da servizio a servizio con Data Lake Store tramite Azure Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>Esempi: Parallel Data Warehouse

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. Creare un'origine dati esterna per fare riferimento a Hadoop con il pushdown abilitato
Specificare l'opzione JOB_TRACKER_LOCATION per abilitare il push-down del calcolo in Hadoop per le query PolyBase. Dopo l'abilitazione, PolyBase usa una decisione basata sui costi per determinare se eseguire il push del calcolo delle query in Hadoop o spostare tutti i dati per elaborare la query in SQL Server. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. Creare un'origine dati esterna per fare riferimento all'archiviazione BLOB di Azure
Per creare un'origine dati esterna per fare riferimento al contenitore dell'archiviazione BLOB di Azure, specificare l'URI dell'archiviazione BLOB di Azure come LOCATION dell'origine dati esterna. Aggiungere la chiave dell'account di archiviazione di Azure al file core-site.xml di PDW per l'autenticazione.

In questo esempio, l'origine dati esterna è un contenitore dell'archiviazione BLOB di Azure denominato dailylogs nell'account di archiviazione di Azure denominato myaccount. L'origine dati esterna dell'archiviazione di Azure è destinata al solo trasferimento dei dati e non supporta il pushdown dei predicati.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Esempi: operazioni bulk   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. Creare un'origine dati esterna per le operazioni bulk che recuperano i dati dall'archiviazione BLOB di Azure.   
**Si applica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Usare l'origine dati seguente per le operazioni bulk che usano [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). La credenziale usata deve essere creata con `SHARED ACCESS SIGNATURE` come identità, non deve avere `?` iniziale nel token di firma di accesso condiviso, deve avere almeno un'autorizzazione di lettura per il file da caricare (ad esempio, `srt=o&sp=r`), e il periodo di scadenza deve essere valido. Tutte le date sono in formato UTC. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '(REMOVE ? FROM THE BEGINNING)******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Per visualizzare l'esempio di utilizzo, vedere [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage).
  
## <a name="see-also"></a>Vedere anche
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

