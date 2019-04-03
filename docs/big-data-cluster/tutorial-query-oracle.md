---
title: Eseguire query sui dati esterni in Oracle
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come eseguire query sui dati di Oracle da un cluster di big data di SQL Server 2019 (anteprima). Creare una tabella esterna su dati in Oracle e quindi eseguire una query.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 139c5dd5ade04c3d1a71412060f823d492843ecb
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58859982"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>Esercitazione: Eseguire una query Oracle da un cluster di big data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come eseguire query sui dati di Oracle da un cluster di big data di SQL Server 2019. Per eseguire questa esercitazione, è necessario avere accesso a un server Oracle. Se non si ha accesso, in questa esercitazione può avere un'idea del funzionamento della virtualizzazione dei dati per origini dati esterne in cluster di big data di SQL Server.

In questa esercitazione, apprenderà come:

> [!div class="checklist"]
> * Creare una tabella esterna per i dati in un database Oracle esterno.
> * Aggiungere i dati con dati di valore elevato nell'istanza master.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi in questa esercitazione. Per istruzioni, vedere la [esempi di dati di virtualizzazione](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) su GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare i dati di esempio in cluster i big Data](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Creare una tabella Oracle

La procedura seguente crea una tabella di esempio denominata `INVENTORY` in Oracle.

1. Connettersi a un'istanza di Oracle e il database che si desidera usare per questa esercitazione.

1. Eseguire l'istruzione seguente per creare il `INVENTORY` tabella:

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. Importare il contenuto del **inventory.csv** file in questa tabella. Questo file è stato creato con gli script di creazione di esempio nel [prerequisiti](#prereqs) sezione.

## <a name="create-an-external-data-source"></a>Creare un'origine dati esterna

Il primo passaggio consiste nel creare un'origine dati esterna che possa accedere al server Oracle.

1. In Azure Data Studio, connettersi all'istanza master di SQL Server del cluster di big data. Per altre informazioni, vedere [connettersi all'istanza master di SQL Server](connect-to-big-data-cluster.md#master).

1. Fare doppio clic sulla connessione nel **server** finestra per visualizzare il dashboard di server per l'istanza master di SQL Server. Selezionare **nuova Query**.

   ![Query di istanza master di SQL Server](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. Eseguire il comando Transact-SQL seguente per modificare il contesto per il **Sales** database nell'istanza master.

   ```sql
   USE Sales
   GO
   ```

1. Creare una credenziale con ambito database per la connessione al server Oracle. Fornire le credenziali appropriate per il server Oracle nell'istruzione seguente.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Creare un'origine dati esterna che punta al server Oracle.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>Creare una tabella esterna

Successivamente, creare una tabella esterna denominata **iventory_ora** tramite il `INVENTORY` tabella sul server Oracle.

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> I nomi di tabella e i nomi delle colonne useranno ANSI SQL identificatore delimitato tra virgolette durante l'esecuzione di query su Oracle. Di conseguenza, i nomi sono tra maiuscole e minuscole. È importante specificare il nome nella definizione della tabella esterna che corrisponda esattamente del caso di nomi della tabella e colonna nei metadati di Oracle.

## <a name="query-the-data"></a>Eseguire query sui dati

Eseguire la query seguente per aggiungere i dati nel `iventory_ora` tabella esterna con le tabelle in locale `Sales` database.

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>Pulizia

Usare il comando seguente per rimuovere gli oggetti di database creati in questa esercitazione.

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come inserire dati nel pool di dati:
> [!div class="nextstepaction"]
> [Caricare dati nel pool di dati](tutorial-data-pool-ingest-sql.md)
