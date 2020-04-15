---
title: Conformanza dell'attributo Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2880a35f4bdc997cc037cdd0d60720267ff4a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306402"
---
# <a name="attribute-conformance"></a>Conformità dell'attributo
Nella tabella seguente viene indicato il livello di conformità di ogni attributo di ambiente ODBC, in cui questo è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] Questa è una caratteristica facoltativa e come tale non fa parte dei livelli di conformità.  
  
 Nella tabella seguente viene indicato il livello di conformità di ogni attributo di connessione ODBC, in cui questo è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|Livello 1/Livello 2[1]|  
|SQL_ATTR_AUTO_IPD|Livello 2|  
|SQL_ATTR_AUTOCOMMIT|Livello 1|  
|SQL_ATTR_CONNECTION_DEAD|Livello 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Livello 2|  
|SQL_ATTR_CURRENT_CATALOG|Livello 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Livello 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|Livello 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|Livello 1/Livello 2[2]|  
  
 [1] Le applicazioni che supportano l'asincronia a livello di connessione (richiesto per il livello 1) devono supportare l'impostazione di questo attributo su SQL_TRUE chiamando **SQLSetConnectAttr**; l'attributo non deve essere impostato su un valore diverso dal valore predefinito tramite **SQLSetStmtAttr**. Le applicazioni che supportano l'asincronia a livello di istruzione (obbligatorio per il livello 2) devono supportare l'impostazione di questo attributo per SQL_TRUE utilizzando una delle due funzioni.  
  
 [2] Per la conformità dell'interfaccia di livello 1, il driver deve supportare un valore oltre al valore predefinito definito dal driver (disponibile chiamando **SQLGetInfo** con l'opzione SQL_DEFAULT_TXN_ISOLATION). Per la conformità dell'interfaccia di livello 2, il driver deve supportare anche SQL_TXN_SERIALIZABLE.  
  
 Nella tabella seguente viene indicato il livello di conformità di ogni attributo dell'istruzione ODBC, in cui questo è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|Livello 1/Livello 2[1]|  
|SQL_ATTR_CONCURRENCY|Livello 1/Livello 2[2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|Livello 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Livello 2|  
|SQL_ATTR_CURSOR_TYPE|Nucleo/Livello 2[3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Livello 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Livello 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|Livello 2|  
|SQL_ATTR_MAX_LENGTH|Livello 1|  
|SQL_ATTR_MAX_ROWS|Livello 1|  
|SQL_ATTR_METADATA_ID|Core|  
|SQL_ATTR_NOSCAN|Core|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_PARAM_BIND_TYPE|Core|  
|SQL_ATTR_PARAM_OPERATION_PTR|Core|  
|SQL_ATTR_PARAM_STATUS_PTR|Core|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|Core|  
|SQL_ATTR_PARAMSET_SIZE|Core|  
|SQL_ATTR_QUERY_TIMEOUT|Livello 2|  
|SQL_ATTR_RETRIEVE_DATA|Livello 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|Livello 1|  
|SQL_ATTR_ROW_OPERATION_PTR|Livello 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR|Core|  
|SQL_ATTR_SIMULATE_CURSOR|Livello 2|  
|SQL_ATTR_USE_BOOKMARKS|Livello 2|  
  
 [1] Le applicazioni che supportano l'asincronia a livello di connessione (richiesto per il livello 1) devono supportare l'impostazione di questo attributo su SQL_TRUE chiamando **SQLSetConnectAttr**; l'attributo non deve essere impostato su un valore diverso dal valore predefinito tramite **SQLSetStmtAttr**. Le applicazioni che supportano l'asincronia a livello di istruzione (obbligatorio per il livello 2) devono supportare l'impostazione di questo attributo per SQL_TRUE utilizzando una delle due funzioni.  
  
 [2] Per la conformità all'interfaccia di livello 2, il driver deve supportare SQL_CONCUR_READ_ONLY e almeno un altro valore.  
  
 [3] Per la conformità all'interfaccia di livello 1, il driver deve supportare SQL_CURSOR_FORWARD_ONLY e almeno un altro valore. Per la conformità dell'interfaccia di livello 2, il driver deve supportare tutti i valori definiti in questo documento.
