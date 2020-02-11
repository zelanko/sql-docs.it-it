---
title: Conformità degli attributi | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71f0da7bbd7ef1a37a1f48539c7230bff0ceda15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909908"
---
# <a name="attribute-conformance"></a>Conformità dell'attributo
Nella tabella seguente viene indicato il livello di conformità di ogni attributo dell'ambiente ODBC, in cui questo è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] si tratta di una funzionalità facoltativa che non fa parte dei livelli di conformità.  
  
 Nella tabella seguente viene indicato il livello di conformità di ogni attributo di connessione ODBC, in cui questo è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|Livello 1/livello 2 [1]|  
|SQL_ATTR_AUTO_IPD|Level 2|  
|SQL_ATTR_AUTOCOMMIT|Livello 1|  
|SQL_ATTR_CONNECTION_DEAD|Livello 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Level 2|  
|SQL_ATTR_CURRENT_CATALOG|Level 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Level 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|Level 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|Livello 1/livello 2 [2]|  
  
 [1] le applicazioni che supportano modalità asincrona a livello di connessione (obbligatorio per il livello 1) devono supportare l'impostazione di questo attributo su SQL_TRUE chiamando **SQLSetConnectAttr**; l'attributo non deve essere impostabile su un valore diverso dal valore predefinito tramite **SQLSetStmtAttr**. Le applicazioni che supportano modalità asincrona a livello di istruzione (obbligatorio per il livello 2) devono supportare l'impostazione di questo attributo su SQL_TRUE usando una delle due funzioni.  
  
 [2] per la conformità dell'interfaccia di livello 1, il driver deve supportare un valore oltre al valore predefinito definito dal driver, disponibile chiamando **SQLGetInfo** con l'opzione SQL_DEFAULT_TXN_ISOLATION. Per la conformità di interfaccia di livello 2, il driver deve supportare anche SQL_TXN_SERIALIZABLE.  
  
 Nella tabella seguente viene indicato il livello di conformità di ogni attributo di istruzione ODBC, in cui questo oggetto è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|Livello 1/livello 2 [1]|  
|SQL_ATTR_CONCURRENCY|Livello 1/livello 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|Livello 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Level 2|  
|SQL_ATTR_CURSOR_TYPE|Core/livello 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Level 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Level 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|Level 2|  
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
|SQL_ATTR_QUERY_TIMEOUT|Level 2|  
|SQL_ATTR_RETRIEVE_DATA|Livello 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|Livello 1|  
|SQL_ATTR_ROW_OPERATION_PTR|Livello 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR|Core|  
|SQL_ATTR_SIMULATE_CURSOR|Level 2|  
|SQL_ATTR_USE_BOOKMARKS|Level 2|  
  
 [1] le applicazioni che supportano modalità asincrona a livello di connessione (obbligatorio per il livello 1) devono supportare l'impostazione di questo attributo su SQL_TRUE chiamando **SQLSetConnectAttr**; l'attributo non deve essere impostabile su un valore diverso dal valore predefinito tramite **SQLSetStmtAttr**. Le applicazioni che supportano modalità asincrona a livello di istruzione (obbligatorio per il livello 2) devono supportare l'impostazione di questo attributo su SQL_TRUE usando una delle due funzioni.  
  
 [2] per la conformità dell'interfaccia di livello 2, il driver deve supportare SQL_CONCUR_READ_ONLY e almeno un altro valore.  
  
 [3] per la conformità di interfaccia di livello 1, il driver deve supportare SQL_CURSOR_FORWARD_ONLY e almeno un altro valore. Per la conformità dell'interfaccia di livello 2, il driver deve supportare tutti i valori definiti in questo documento.
