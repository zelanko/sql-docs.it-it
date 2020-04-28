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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300191"
---
# <a name="header-files"></a>File di intestazione
Il file di intestazione SQL. h contiene prototipi per le funzioni e le funzionalità del livello di conformità dell'interfaccia ODBC di base. Il file di intestazione sqlext. h contiene prototipi per le funzioni e le funzionalità nei livelli di conformità dell'API di livello 1 e 2. Il file di intestazione SqlTypes. h contiene le definizioni e gli indicatori di tipo per i tipi di dati SQL.  
  
 Tutti i file di intestazione contengono un **#define**, ODBCVer, che un'applicazione o un driver può impostare per la compilazione per versioni diverse di ODBC.  
  
 Per l'allineamento con l'interfaccia della riga di comando ISO e l'interfaccia della riga di comando Apri gruppo, i file di intestazione contengono alias per i tipi di informazioni usati nelle chiamate a **SQLGetInfo**. Nella tabella seguente la colonna "nome ODBC" indica il nome ODBC per il tipo di informazioni nel [riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md). La colonna "alias in file di intestazione" indica il nome usato nell'interfaccia della riga di comando ISO e nell'interfaccia della riga di comando del gruppo aperto. Il valore numerico effettivo di questi nomi di manifesto è lo stesso sia in ODBC che nel interfacce della riga standard. Questi alias consentono a un'applicazione o un driver conforme agli standard di compilare con i file di intestazione ODBC *3. x* .  
  
 Questi alias includono espansioni delle abbreviazioni nei nomi ODBC in modo che i nomi siano più comprensibili. "MAX" viene espanso in "MAXIMum", "LEN" in "LENGTH", "MULT" in "MULTIPLE", "OJ" in "OUTER_JOIN" e "transazione" in "TRANSACTION".  
  
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
