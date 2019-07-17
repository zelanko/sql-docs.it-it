---
title: File di intestazione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d20f2535038b13eac0b8d5ca20dfa77bfc12588
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139032"
---
# <a name="header-files"></a>File di intestazione
Il file di intestazione SQL. h contiene prototipi per le funzioni e funzionalità del livello di conformità di interfaccia ODBC Core. Il file di intestazione Sqlext. h contiene prototipi per le funzioni e le funzionalità del livello 1 e livelli di conformità API di livello 2. Il file di intestazione Sqlext contiene le definizioni dei tipi e gli indicatori per i tipi di dati SQL.  
  
 I file di intestazione contengono tutti un **#define**, ODBCVER, che un'applicazione o driver può impostare da compilare per versioni diverse di ODBC.  
  
 Per allineare con la CLI ISO e aprire interfaccia CLI di gruppo, i file di intestazione contengono alias per i tipi di informazioni usati nelle chiamate a **SQLGetInfo**. Nella tabella seguente, la colonna "Nome ODBC" indica il nome ODBC per il tipo di informazioni nella [riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). La colonna "Alias nel file di intestazione" indica il nome che viene utilizzato la CLI di ISO e l'interfaccia CLI di gruppo aprire. Il valore numerico effettivo di questi nomi di manifesto è lo stesso in ODBC sia la CLI di standard. Questi alias abilitare un'applicazione conforme agli standard o un driver per la compilazione con ODBC *3.x* i file di intestazione.  
  
 Questi alias includono le espansioni di abbreviazioni nei nomi di ODBC in modo che i nomi sono più comprensibili. "MAX" viene espanso alle "Massimo", "LEN" a "LENGTH", "MULT" a "MULTIPLE", "GU" a "OUTER_JOIN" e "TXN" a "Transazione".  
  
|Nome di ODBC|Alias nel file di intestazione|  
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
