---
title: Tipi di dati Java supportati in SQL Server 2019
titleSuffix: SQL Server Language Extensions
description: Eseguire il mapping di tipi di dati da Java a SQL Server per strutture di dati di input e output e per parametri di input in sp_execute_external_script.
author: dphansen
ms.author: davidph
ms.date: 09/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9daca9c607befe077fcccec20385a36c82b04c6f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "73588835"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipi di dati Java e SQL Server supportati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo articolo viene eseguito il mapping di tipi di dati SQL Server a tipi di dati Java per parametri e strutture di dati in [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Sono attualmente supportati i tipi di dati SQL e Java seguenti per i set di dati di input/output e i parametri di input/output.

| Tipo di dati SQL        | Tipo di dati Java | Commento | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | Sono supportate solo stringhe UTF8 | |
| varchar(n) | String | Sono supportate solo stringhe UTF8 | |
| ntext | String | Sono supportate solo stringhe UTF8 | |
| Data | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](../how-to/call-java-from-sql.md)
