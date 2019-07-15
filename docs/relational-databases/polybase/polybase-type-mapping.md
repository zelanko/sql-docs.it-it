---
title: Mapping dei tipi con PolyBase | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
manager: craigg
ms.openlocfilehash: 67ecc3a75da04849d6b23d0b07f6e650c2825b0b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731797"
---
# <a name="type-mapping-with-polybase"></a>Mapping dei tipi con PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive il mapping tra le origini dati esterne PolyBase e SQL Server. È possibile usare queste informazioni per definire correttamente le tabelle esterne con il comando Transact-SQL [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

## <a name="overview"></a>Panoramica

Quando si crea una tabella esterna con PolyBase, le definizioni di colonna, inclusi i tipi di dati e il numero di colonne, devono corrispondere ai dati nei file esterni. In caso di mancata corrispondenza, le righe di file vengono rifiutate quando si eseguono query sui dati effettivi.  
  
Per le tabelle esterne che fanno riferimento a file in origini dati esterne, è necessario eseguire il mapping delle definizioni di colonna e di tipo allo schema esatto del file esterno. Quando si definiscono i tipi di dati che fanno riferimento ai dati archiviati in Hadoop/Hive, usare i mapping seguenti tra i tipi di dati SQL e Hive ed eseguire il cast del tipo in un tipo di dati SQL quando si effettua una selezione. Se non specificato diversamente, i tipi includono tutte le versioni di Hive.

> [!NOTE]  
> SQL Server non supporta il valore di dati Hive *infinity* in alcuna conversione. PolyBase avrà esito negativo con un errore di conversione del tipo di dati.

## <a name="hadoop-type-mapping-reference"></a>Informazioni di riferimento per i mapping dei tipi Hadoop

| Tipo di dati SQL | Tipo di dati .NET            | Tipo di dati Hive | Tipo di dati Hadoop/Java | Commenti                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| TINYINT       | Byte                      | TINYINT        | ByteWritable          | Solo per numeri non firmati.     |
| SMALLINT      | Int16                     | SMALLINT       | ShortWritable         |
| INT           | Int32                     | INT            | IntWritable           |
| BIGINT        | Int64                     | BIGINT         | LongWritable          |
| bit           | Boolean                   | boolean        | BooleanWritable       |
| FLOAT         | Double                    | double         | DoubleWritable        |
| REAL          | Single                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | String<br /><br /> Char[] | string         | Varchar               |
| NVARCHAR      | String<br /><br /> Char[] | string         | Varchar               |
| char          | String<br /><br /> Char[] | string         | Varchar               |
| varchar       | String<br /><br /> Char[] | string         | Varchar               |
| BINARY        | Byte[]                    | BINARY         | BytesWritable         | Si applica a Hive 0.8 e versioni successive. |
| varbinary     | Byte[]                    | BINARY         | BytesWritable         | Si applica a Hive 0.8 e versioni successive. |
| Data          | DateTime                  | TIMESTAMP      | TimestampWritable     |
| smalldatetime | DateTime                  | TIMESTAMP      | TimestampWritable     |
| datetime2     | DateTime                  | TIMESTAMP      | TimestampWritable     |
| DATETIME      | DateTime                  | TIMESTAMP      | TimestampWritable     |
| time          | TimeSpan                  | TIMESTAMP      | TimestampWritable     |
| Decimal       | Decimal                   | Decimal        | BigDecimalWritable    | Si applica a Hive 0.11 e versioni successive. |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Informazioni di riferimento per i mapping dei tipi Oracle

| Tipo di dati Oracle | Tipo di SQL Server | 
| -------------    | --------------- |
|float             |float            |
|NUMBER            |Decimal          |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

**Tipo non corrispondente** 

**Float:** Oracle supporta la precisione a virgola mobile 126, inferiore rispetto alla precisione supportata da SQL Server (53). È quindi possibile il mapping diretto di **Float (1-53)** , ma per valori superiori si verifica una perdita di dati a causa di troncamento.

**Timestamp:** Timestamp e Timestamp with local timezone in Oracle supportano una precisione frazionaria pari a 9 secondi, mentre DateTime2 in SQL Server supporta una precisione frazionaria pari a 7 secondi. 




## <a name="mongodb-type-mapping"></a>Mapping dei tipi MongoDB

| Tipo di dati BSON     | Tipo di SQL Server |
| ------------------ | --------------- |
| Double             | float           |
| String             | nvarchar        |
| Dati binari        | nvarchar        |
| ID dell'oggetto.          | nvarchar        |
| Boolean            | bit             |
| date               | Datetime2       |
| Intero a 32 bit     | Int             |
| Timestamp          | nvarchar        |
| Intero a 64 bit     | BigInt          |
|Decimal 128         | Decimal         | 
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| Max Key            | nvarchar        |
| Min Key            | nvarchar        |
| Simbolo             | nvarchar        |
| Espressione regolare | nvarchar        |
| Non definito/NULL     | nvarchar        |


MongoDB Usa documenti BSON per archiviare i record dei dati. A differenza di allo scenario precedente, BSON è senza schema e supporta l'incorporamento di documenti e matrici all'interno di altri documenti. Questo comportamento offre maggiore flessibilità all'utente. 


## <a name="teradata-type-mapping-reference"></a>Informazioni di riferimento per i mapping dei tipi Teradata

| Tipo di dati Teradata | Tipo di SQL Server | 
| -------------      | -------------   |
|INTEGER             |Int              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |Binario           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |date             |
|timestamp           |Datetime2        |
|TIME                |Time             |
|TIME WITH TIME ZONE |Time             |
|TIMESTAMP WITH TIME ZONE|Time         |

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come usare questa funzionalità, vedere l'articolo di riferimento per Transact-SQL per [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
