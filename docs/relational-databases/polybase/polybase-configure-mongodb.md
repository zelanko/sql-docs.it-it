---
title: Configurare PolyBase per l'accesso a dati esterni in MongoDB | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c4ccf371cdcac99d50c3142ec42641380623501
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044497"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>Configurare PolyBase per l'accesso a dati esterni in MongoDB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'articolo illustra come usare PolyBase in un'istanza di SQL Server per eseguire query sui dati esterni in MongoDB.

## <a name="prerequisites"></a>Prerequisites

Se PolyBase non è stato installato, vedere [Installazione di PolyBase](polybase-installation.md).

## <a name="configure-an-external-table"></a>Configurare una tabella esterna

Per eseguire query sui dati da un'origine dati MongoDB, è necessario creare tabelle esterne per fare riferimento ai dati esterni. In questa sezione è disponibile codice di esempio per creare queste tabelle esterne.

In questa sezione verranno creare questi oggetti:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL)
- CREATE EXTERNAL TABLE (Transact-SQL)
- CREATE STATISTICS (Transact-SQL)

1. Creare una chiave master nel database, se non esiste già. Questo passaggio è necessario per crittografare il segreto delle credenziali.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>Argomenti
    PASSWORD ='password'

    Password utilizzata per crittografare la chiave master nel database. password deve soddisfare i requisiti per i criteri password di Windows del computer che esegue l'hosting dell'istanza di SQL Server.

1.   Creare una credenziale con ambito database per l'accesso all'origine di MongoDB.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1.  Creare un'origine dati esterna con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
     /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (
    LOCATION = mongodb://<server>[:<port>],
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );
     ```

1.  Creare tabelle esterne che rappresentano i dati archiviati nel sistema esterno MongoDB [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

     ```sql
     /*  LOCATION: MongoDB table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customers(
     [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='customer',
     DATA_SOURCE= external_data_source_name
     );
     ```

1. **Facoltativo:** Creare statistiche per una tabella esterna.

    È consigliabile creare le statistiche sulle colonne delle tabelle esterne, in particolare quelle usate per join, filtri e aggregazioni, per prestazioni ottimali delle query.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```


## <a name="flattening"></a>Rendere flat
 L'impostazione per l'appiattimento è abilitata per i dati nidificati e ripetuti delle raccolte di documenti MongoDB. L'utente deve abilitare `create an external table` e specificare in modo esplicito uno schema relazionale per le raccolte di documenti MongoDB che possono avere dati nidificati e/o ripetuti. Il rilevamento automatico dello schema per le raccolte di documenti Mongo verrà abilitato in attività cardine future.
I tipi di dati JSON nidificati/ripetuti verranno appiattiti come indicato di seguito

* Oggetto: raccolta chiave/valore non ordinata racchiusa tra parentesi graffe (nidificata)

   - Si creerà una colonna di tabella per ogni chiave oggetto

     * Nome colonna: objectname_keyname

* Matrice: valori ordinati, separati da virgole, racchiusi tra parentesi quadre (ripetute)

   - Si aggiungerà una nuova riga della tabella per ogni elemento della matrice

   - Si creerà una colonna per ogni matrice per archiviare l'indice dell'elemento matrice

     * Nome colonna: arrayname_index

     * Tipo di dati: bigint

Questa tecnica può originare vari problemi, tra cui i due seguenti:

* Un campo ripetuto vuoto maschererà i dati contenuti nei campi flat dello stesso record

* La presenza di più campi ripetuti può comportare una crescita esponenziale del numero di righe prodotte

A titolo di esempio viene valutata la raccolta di ristoranti del dataset di esempio MongoDB archiviata in formato JSON non relazionale. Ogni ristorante dispone di un campo indirizzo nidificato e di una matrice di valutazioni che sono state assegnate in giorni diversi. La figura seguente illustra un ristorante con l'indirizzo nidificato e le valutazioni nidificate ripetute.

![Appiattimento MongoDB](../../relational-databases/polybase/media/mongo-flattening.png "Appiattimento ristoranti MongoDB")

L'indirizzo dell'oggetto verrà appiattito (reso flat) come indicato di seguito:

* Il campo nidificato restaurant.address.building diventa restaurant.address_building
* Il campo nidificato restaurant.address.coord diventa restaurant.address_coord
* Il campo nidificato restaurant.address.street diventa restaurant.address_street
* Il campo nidificato restaurant.address.zipcode diventa restaurant.address_zipcode

Le valutazioni della matrice vengono appiattite come indicato di seguito:

| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |Un |2|
|1378857600000|Un |6|
|135898560000 |Un |10|
|1322006400000|Un |9|
|1299715200000 |B |14|

## <a name="cosmos-db-connection"></a>Connessione Cosmos DB

Usando l'api di Mongo Cosmos DB e il connettore di Mongo DB PolyBase è possibile creare una tabella esterna di un'**istanza di Cosmos DB**. Questa operazione viene eseguita seguendo gli stessi passaggi elencati in precedenza. Assicurarsi che la credenziale con ambito database, l'indirizzo server, la porta e la stringa di posizione riflettano quelli del server di Cosmos DB. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](polybase-guide.md).
