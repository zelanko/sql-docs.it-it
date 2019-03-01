---
title: Tipi di dati di Java supportati in SQL Server 2019 - servizi di SQL Server Machine Learning
description: Eseguire il mapping di tipi di dati da Java a SQL Server per le strutture di dati di input e output e per i parametri di input nella finestra di sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c0f691b8bb389c2da2001d19f0684b7f928f707
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017817"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipi di dati supportati di SQL Server e Java

Questo articolo esegue il mapping di tipi di dati di SQL Server in tipi di dati Java per le strutture di dati e i parametri nel [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipi di dati per i set di dati

I seguenti tipi di dati SQL e Java sono attualmente supportati per i set di dati di Input e Output.

| Tipo di dati SQL        | Tipo di dati Java | Commento | |
| ------------- |-------------|-|
| bit      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | INT      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String  | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | String | |
| varbinary(max) | byte[] | |
| UNIQUEIDENTIFIER | String | |
| char(n) | String | Solo le stringhe UTF8 supportati |
| varchar(n) | String | Solo le stringhe UTF8 supportati |
| ntext | String | Solo le stringhe UTF8 supportati |

## <a name="data-types-for-input-parameters"></a>Tipi di dati per i parametri di input

I seguenti tipi di dati SQL e Java sono attualmente supportati per i parametri di input.

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
| char(n) | String | Solo le stringhe UTF8 supportati | |
| varchar(n) | String | Solo le stringhe UTF8 supportati | |
| ntext | String | Solo le stringhe UTF8 supportati | |

## <a name="see-also"></a>Vedere anche

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Estensione del linguaggio Java in SQL Server](extension-java.md)