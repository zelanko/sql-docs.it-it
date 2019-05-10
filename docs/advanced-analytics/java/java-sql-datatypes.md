---
title: Tipi di dati di Java supportati in SQL Server 2019 - estensioni del linguaggio SQL Server
description: Eseguire il mapping di tipi di dati da Java a SQL Server per le strutture di dati di input e output e per i parametri di input nella finestra di sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14a2bc5594b16610dfb8278ab82a9e7b8b22fea6
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774997"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipi di dati supportati di SQL Server e Java

Questo articolo esegue il mapping di tipi di dati di SQL Server in tipi di dati Java per le strutture di dati e i parametri nel [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipi di dati per i set di dati

I seguenti tipi di dati SQL e Java sono attualmente supportati per i set di dati di Input e Output.


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

## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Estensione del linguaggio Java in SQL Server](extension-java.md)
