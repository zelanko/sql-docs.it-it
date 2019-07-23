---
title: Conformità con JDBC 4,3 per il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20cefb029a126b0a262d86a2dc0a0791959085bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956363"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformità a JDBC 4.3 per il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Le versioni precedenti a Microsoft JDBC Driver 6.4 per SQL Server sono compatibili solo con le specifiche Java Database Connectivity (JDBC) API 4.2. Questa sezione non è applicabile per la versione 6.4 e versioni precedenti.

A partire dalla versione 6,4, Microsoft JDBC Driver for SQL Server è compatibile con Java 9 `SQLFeatureNotSupportedException` e genera per le nuove API JDBC 4,3 con metodi non implementati.

Con Microsoft JDBC driver 7,0 per SQL Server versione, il driver è ora compatibile con JAVA 10 e supporta le API indicate di seguito. Il driver genera `SQLFeatureNotSupportedException` per altri metodi non implementati dalle specifiche JDBC 4,3.

|Nuova API|Descrizione|Implementazione significativa|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Suggerisce al driver che una richiesta, un'unità di lavoro indipendente, sta iniziando da questa connessione. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva i valori dei campi di connessione modificabili tramite metodi API pubblici: `databaseAutoCommitMode`, `disableStatementPooling` `serverPreparedStatementDiscardThreshold` `statementPoolingCacheSize` `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`,,,, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Suggerisce al driver che una richiesta, un'unità di lavoro indipendente, è stata completata. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Chiude le istruzioni create durante l'unità di lavoro ed esegue il rollback di tutte le transazioni aperte. Il metodo ripristina inoltre le modifiche apportate ai campi di connessione elencati in precedenza.|
