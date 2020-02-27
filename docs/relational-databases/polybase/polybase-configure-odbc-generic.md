---
title: 'Accedere ai dati esterni: Tipi ODBC generici - PolyBase'
ms.date: 02/19/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: ddee333a437ca7250252fb3938ee248bb28269f3
ms.sourcegitcommit: 87b932dc4b603a35a19f16e2c681b6a8d4df1fec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77507582"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurare PolyBase per l'accesso a dati esterni in SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

PolyBase in SQL Server 2019 consente di connettersi alle origini dati compatibili ODBC tramite il connettore ODBC.

Questo articolo fornisce alcuni esempi che usano un driver ODBC. Per esempi specifici, rivolgersi al provider ODBC. Per determinare le opzioni appropriate per la stringa di connessione, vedere la documentazione del driver ODBC per l'origine dati. Gli esempi in questo articolo potrebbero non essere applicabili a un driver ODBC specifico.

## <a name="prerequisites"></a>Prerequisites

>[!NOTE]
>Questa funzionalità richiede SQL Server in Windows.

* [Installazione di PolyBase](polybase-installation.md).

* Prima di creare credenziali con ambito database, è necessario creare una [chiave master](../../t-sql/statements/create-master-key-transact-sql.md).

## <a name="install-the-odbc-driver"></a>Installare il driver ODBC

Prima di tutto scaricare e installare il driver ODBC dell'origine dati a cui ci si vuole connettere in ogni nodo PolyBase. Una volta installato correttamente il driver, è possibile visualizzare e testare il driver da **Amministratore origine dati ODBC**.

![Gruppi con scalabilità orizzontale di PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

Nell'esempio precedente il nome del driver è racchiuso in un cerchio rosso. Usare questo nome quando si crea l'origine dati esterna.

> [!IMPORTANT]
> Per migliorare le prestazioni delle query, abilitare il pool di connessioni. Questa operazione può essere eseguita da **Amministratore origine dati ODBC**.

## <a name="create-an-external-table"></a>Creare una tabella esterna

Per eseguire query sui dati da un'origine dati ODBC, è necessario creare tabelle esterne per fare riferimento ai dati esterni. In questa sezione è disponibile codice di esempio per creare tabelle esterne.

In questa sezione vengono usati i comandi Transact-SQL seguenti:

* [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
* [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Creare le credenziali con ambito database per l'accesso all'origine ODBC.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    L'esempio seguente crea una credenziale denominata `credential_name`, con l'identità `username` e una password complessa.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. Creare un'origine dati esterna con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    L'esempio seguente crea un'origine dati esterna:
    * Denominata `external_data_source_name`
    * Contenuta in `SERVERNAME` e sulla porta `4444` ODBC
    * Connessa con `CData ODBC Driver For SAP 2015`, ovvero il driver creato in [Installare il driver ODBC](#install-the-odbc-driver)
    * Sulla porta `5555` di `ServerNode` `sap_server_node`
    * Configurata per l'elaborazione propagata al server (`PUSHDOWN = ON`)
    * Che usa la credenziale `credential_name`

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://SERVERNAME:4444,
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```

1. **Facoltativo:** Creare statistiche per una tabella esterna.

    Per garantire prestazioni ottimali delle query, è consigliabile creare le statistiche sulle colonne delle tabelle esterne, in particolare quelle usate per join, filtri e aggregazioni.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT]
>Dopo aver creato un'origine dati esterna, usare il comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) per creare una tabella disponibile per query su tale origine.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](polybase-guide.md).
