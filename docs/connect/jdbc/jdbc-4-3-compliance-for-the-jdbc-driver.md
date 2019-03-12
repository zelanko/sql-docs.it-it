---
title: JDBC 4.3 conformità per il Driver JDBC | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fc2fbb2b217880b255d522149dabd38701a8c0e4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579061"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformità a JDBC 4.3 per il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Le versioni precedenti a Microsoft JDBC Driver 6.4 per SQL Server sono compatibili solo con le specifiche Java Database Connectivity (JDBC) API 4.2. Questa sezione non è applicabile per la versione 6.4 e versioni precedenti.

A partire dalla versione 6.4, Microsoft JDBC Driver per SQL Server è compatibile con JAVA 9 e genera `SQLFeatureNotSupportedException` per nuove API 4.3 JDBC che hanno non implementati i metodi.

Con Microsoft JDBC Driver 7.0 per la versione di SQL Server, il driver è ora JAVA 10 compatibile e supporta riportato di seguito indicato le API. Il driver genera `SQLFeatureNotSupportedException` per altri metodi non implementate dalle specifiche di JDBC 4.3.

|Nuova API|Descrizione|Implementazione significativa|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Suggerimenti per il driver che sta iniziando una richiesta, un'unità indipendente di lavoro, per la connessione. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva i valori dei campi connessione modificabili tramite i metodi API pubblici: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Suggerimenti per il driver in una richiesta, un'unità indipendente di lavoro, è stata completata. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Chiude le istruzioni che vengono create durante l'unità di lavoro ed eseguire il rollback delle transazioni aperte. Il metodo ripristina inoltre le modifiche apportate ai campi connessione elencate in precedenza.|
