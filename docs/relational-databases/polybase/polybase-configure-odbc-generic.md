---
title: Configurare PolyBase per l'accesso a dati esterni con i tipi generici ODBC | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: b07d97563406a464bfdb38dba7b3aa1d51e27c34
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874786"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurare PolyBase per l'accesso a dati esterni in SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

PolyBase in SQL Server 2019 consente di connettersi alle origini dati compatibili ODBC tramite il connettore ODBC. 

## <a name="prerequisites"></a>Prerequisites

Nota = la funzionalità può essere usata solo in SQL Server in Windows. 

Se PolyBase non è stato installato, vedere [Installazione di PolyBase](polybase-installation.md).

 Prima di creare credenziali con ambito database, è necessario creare una [chiave master](../../t-sql/statements/create-master-key-transact-sql.md). 

Prima di tutto scaricare e installare il driver ODBC dell'origine dati a cui si desidera connettersi su ciascuno dei nodi PolyBase. Una volta installato correttamente il driver, è possibile visualizzare e testare il driver dall'"Amministratore origine dati ODBC".

![Gruppi con scalabilità orizzontale di PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **IMPORTANTE**
> 
> Per migliorare le prestazioni della query assicurarsi che il pool di connessioni del driver sia attivato. Ciò può essere eseguito dall'"Amministratore origine dati ODBC".
> 
> **Nota**
> 
> Durante la creazione dell'origine dati esterni (passaggio 3 riportato di seguito) dovrà essere specificato il nome del driver (esempio indicato sopra con un cerchio).

## <a name="create-an-external-table"></a>Creare una tabella esterna

Per eseguire query sui dati da un'origine dati ODBC, è necessario creare tabelle esterne per fare riferimento ai dati esterni. In questa sezione è disponibile codice di esempio per creare tabelle esterne.

In questa sezione vengono usati i comandi Transact-SQL seguenti:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Creare le credenziali con ambito database per l'accesso all'origine ODBC.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. Creare un'origine dati esterna con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_nam );
    ```

1. **Facoltativo:** Creare statistiche per una tabella esterna.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Per garantire prestazioni ottimali delle query, è consigliabile creare le statistiche sulle colonne delle tabelle esterne, in particolare quelle usate per join, filtri e aggregazioni.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Dopo aver creato un'origine dati esterna, è possibile usare il comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) per creare una tabella disponibile per query su tale origine. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](polybase-guide.md).
