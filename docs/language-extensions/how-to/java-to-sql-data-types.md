---
title: Tipi di dati Java
titleSuffix: SQL Server Language Extensions
description: Eseguire il mapping di tipi di dati da Java a SQL Server per strutture di dati di input e output e per parametri di input in sp_execute_external_script.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26c5e6f344d9fb0a14a21fa195214c4460673de0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748517"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipi di dati Java e SQL Server supportati
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

In questo articolo viene eseguito il mapping di tipi di dati SQL Server a tipi di dati Java per parametri e strutture di dati in [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Sono attualmente supportati i tipi di dati SQL e Java seguenti per i set di dati di input/output e i parametri di input/output.

| Tipo di dati SQL        | Tipo di dati Java | Comment | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | float      | | |
| Bigint | long      | | |
| float | double      | | |
| nchar(n) | string      | | |
| nvarchar(n) | string      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | string      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | string | | |
| char(n) | string | Sono supportate solo stringhe UTF8 | |
| varchar(n) | string | Sono supportate solo stringhe UTF8 | |
| ntext | string | Sono supportate solo stringhe UTF8 | |
| Data | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| Datetime | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](../how-to/call-java-from-sql.md)
