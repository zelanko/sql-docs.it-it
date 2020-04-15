---
title: File di intestazione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300191"
---
# <a name="header-files"></a>File di intestazione
Il file di intestazione Sql.h contiene prototipi per le funzioni e le funzionalità del livello di conformità dell'interfaccia ODBC Core. Il file di intestazione Sqlext.h contiene prototipi per le funzioni e le funzionalità nei livelli di conformità dell'API di livello 1 e di livello 2. Il file di intestazione Sqltypes.h contiene definizioni e indicatori di tipo per i tipi di dati SQL.  
  
 Tutti i file di intestazione contengono un **#define**, ODBCVER, che un'applicazione o un driver può impostare per essere compilato per diverse versioni di ODBC.  
  
 Per allinearsi all'interfaccia della riga di comando ISO e all'interfaccia della riga di comando Apri gruppo, i file di intestazione contengono alias per i tipi di informazioni utilizzati nelle chiamate a **SQLGetInfo.** Nella tabella seguente la colonna "Nome ODBC" indica il nome ODBC per il tipo di informazioni in [Riferimento all'API ODBC.](../../../odbc/reference/syntax/odbc-api-reference.md) La colonna "Alias nel file di intestazione" indica il nome utilizzato nell'interfaccia della riga di comando ISO e nell'interfaccia della riga di comando Apri gruppo. Il valore numerico effettivo di questi nomi di manifesto è lo stesso sia in ODBC che nelle Interfacce di codice standard. Questi alias consentono la compilazione con i file di intestazione ODBC *3.x* con un'applicazione o un driver conforme agli standard.  
  
 Questi alias includono espansioni di abbreviazioni nei nomi ODBC in modo che i nomi siano più comprensibili. "MAX" viene espanso in "MAXIMUM", "LEN" a "LENGTH", "MULT" a "MULTIPLE", "OJ" a "OUTER_JOIN" e "TXN" a "TRANSACTION".  
  
|Nome ODBC|Alias nel file di intestazione|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
