---
title: Tipi di dati di Java supportati in SQL Server 2019 - servizi di SQL Server Machine Learning
description: Eseguire il mapping di tipi di dati da Java a SQL Server per le strutture di dati di input e output e per i parametri di input nella finestra di sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6921a40efc9af3ef94c0a53f8409891fee16127e
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432534"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipi di dati supportati di SQL Server e Java

Questo articolo esegue il mapping di tipi di dati di SQL Server in tipi di dati Java per le strutture di dati e i parametri nel [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipi di dati per i set di dati

I seguenti tipi di dati SQL e Java sono attualmente supportati per i set di dati di Input e Output.

| Tipo SQL        | Tipo di Java | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Stringa (unicode)      | | |
| nvarchar (n) | Stringa (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |

## <a name="data-types-for-input-parameters"></a>Tipi di dati per i parametri di input

I seguenti tipi di dati SQL e Java sono attualmente supportati per i parametri di input.

| Tipo SQL        | Tipo di Java | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Stringa (unicode)      | | |
| nvarchar (n) | Stringa (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |
| nvarchar(max) | Stringa (unicode)      | | |
| varbinary(max) | byte[]      | | |

## <a name="see-also"></a>Vedere anche

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Estensione del linguaggio Java in SQL Server](extension-java.md)