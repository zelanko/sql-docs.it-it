---
title: Ottimizzare l'elaborazione JSON con OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b179a288ca7bb2722b027dff07acacde5d62527d
ms.sourcegitcommit: 0330cbd1490b63e88334a9f9e421f4bd31a6083f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2018
ms.locfileid: "52886676"
---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Ottimizzare l'elaborazione JSON con OLTP in memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SQL Server e il database SQL di Azure consentono di usare il testo formattato come JSON. Per migliorare le prestazioni delle query che elaborano dati JSON, è possibile archiviare i documenti JSON in tabelle ottimizzate per la memoria usando colonne di tipo stringa standard (tipo NVARCHAR). L'archiviazione dei dati JSON in tabelle ottimizzate per la memoria aumenta le prestazioni delle query mediante l'accesso ai dati in memoria senza blocco.

## <a name="store-json-in-memory-optimized-tables"></a>Archiviare dati JSON in tabelle ottimizzate per la memoria
Nell'esempio seguente è illustrata una tabella `Product` ottimizzata per la memoria contenente due colonne JSON, `Tags` e `Data`.

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```

## <a name="optimize-json-processing-with-additional-in-memory-features"></a>Ottimizzare l'elaborazione JSON con funzionalità in memoria aggiuntive
Le funzionalità disponibili in SQL Server e nel database SQL di Azure consentono di integrare le funzionalità JSON con le tecnologie OLTP in memoria esistenti. Ad esempio, è possibile eseguire le operazioni seguenti:
 - [Convalidare la struttura dei documenti JSON](#validate) archiviati in tabelle ottimizzate per la memoria usando vincoli CHECK compilati in modo nativo.
 - [Esporre e tipizzare i valori](#computedcol) archiviati nei documenti JSON usando colonne calcolate.
 - [Indicizzare i valori](#index) nei documenti JSON usando indici ottimizzati per la memoria.
 - [Compilare in modo nativo le query SQL](#compile) che usano valori di documenti JSON o formattano i risultati come testo JSON.

## <a name="validate"></a> Convalidare le colonne JSON
SQL Server e il database SQL di Azure consentono di aggiungere vincoli CHECK compilati in modo nativo che convalidano il contenuto dei documenti JSON archiviati in una colonna di tipo stringa. I vincoli JSON CHECK compilati in modo nativo garantiscono la corretta formattazione del testo JSON archiviato nelle tabelle ottimizzate per la memoria.

L'esempio seguente crea una tabella `Product` con una colonna JSON `Tags`. La colonna `Tags` ha un vincolo CHECK che usa la funzione `ISJSON` per convalidare il testo JSON nella colonna.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

È anche possibile aggiungere il vincolo CHECK compilato in modo nativo in una tabella esistente che contiene colonne JSON.

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

## <a name="computedcol"></a> Esporre i valori JSON usando colonne calcolate
Le colonne calcolate consentono di esporre i valori del testo JSON e di accedere ai valori senza recuperare di nuovo il valore dal testo JSON e senza rieseguire l'analisi della struttura JSON. I valori esposti sono fortemente tipizzati e fisicamente salvati in modo permanente nelle colonne calcolate. L'accesso ai valori JSON tramite colonne calcolate salvate in modo permanente è più veloce rispetto all'accesso ai valori direttamente nel documento JSON.

Nell'esempio seguente viene illustrato come esporre i due valori seguenti dalla colonna JSON `Data`:
-   paese di produzione del prodotto;
-   costo di produzione del prodotto.

Nell'esempio le colonne calcolate `MadeIn` e `Cost` vengono aggiornate a ogni modifica del documento JSON archiviato nella colonna `Data`.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

## <a name="index"></a> Indicizzare i valori nelle colonne JSON
SQL Server e il database SQL di Azure consentono di indicizzare i valori nelle colonne JSON tramite indici ottimizzati per la memoria. I valori JSON indicizzati devono essere esposti e fortemente tipizzati usando colonne calcolate, come illustrato nell'esempio precedente.

I valori nelle colonne JSON possono essere indicizzati usando sia gli indici NONCLUSTERED sia gli indici HASH standard.
-   Gli indici NONCLUSTERED ottimizzano le query che eseguono la selezione di intervalli di righe in base a un valore JSON oppure l'ordinamento dei risultati in base ai valori JSON.
-   Gli indici HASH ottimizzano le query che selezionano una singola riga o poche righe specificando un valore esatto da trovare.

L'esempio seguente crea una tabella che espone i valori JSON mediante due colonne calcolate. L'esempio crea un indice NONCLUSTERED in un valore JSON e un indice HASH in un altro.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```

## <a name="compile"></a> Compilazione nativa di query JSON
Se le procedure, le funzioni e i trigger contengono query che usano le funzioni JSON predefinite, la compilazione nativa migliora le prestazioni delle query e riduce i cicli della CPU necessari per eseguirle.

L'esempio seguente illustra una procedura compilata in modo nativo che usa diverse funzioni JSON, ovvero **JSON_VALUE**, **OPENJSON** e **JSON_MODIFY**.

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
