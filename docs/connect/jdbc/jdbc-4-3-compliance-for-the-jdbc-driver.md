---
title: Conformità con JDBC 4.3 per il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 099664892564a6b38e270f934cb3208029fdd05f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928354"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformità con JDBC 4.3 per il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Le versioni precedenti a Microsoft JDBC Driver 6.4 per SQL Server sono compatibili solo con le specifiche Java Database Connectivity (JDBC) API 4.2. Questa sezione non è applicabile per la versione 6.4 e versioni precedenti.

A partire dalla versione 6.4, Microsoft JDBC Driver per SQL Server è compatibile con JAVA 9 e genera `SQLFeatureNotSupportedException` per le nuove API JDBC 4.3 con metodi non implementati.

Con la versione 7.0 di Microsoft JDBC driver per SQL Server, il driver è ora compatibile con JAVA 10 e supporta le API indicate di seguito. Il driver genera `SQLFeatureNotSupportedException` per altri metodi non implementati dalle specifiche JDBC 4.3.

|Nuova API|Descrizione|Implementazione significativa|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Indica al driver che una richiesta, un'unità di lavoro indipendente, sta iniziando in questa connessione. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva i valori dei campi di connessione modificabili tramite metodi API pubblici: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Indica al driver che una richiesta, un'unità di lavoro indipendente, è stata completata. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Chiude le istruzioni create durante l'unità di lavoro ed esegue il rollback di tutte le transazioni aperte. Il metodo ripristina anche le modifiche apportate ai campi di connessione elencati in precedenza.|
