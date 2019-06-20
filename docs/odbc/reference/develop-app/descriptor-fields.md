---
title: I campi di descrizione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b512ff83d0002ef4a7c79b48cd8829fc2dbb9ba3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049777"
---
# <a name="descriptor-fields"></a>Campi del descrittore
Contengono i descrittori *intestazione* e *record* campi che descrivono completamente le colonne o parametri.  
  
 Un descrittore contiene una sola copia dei seguenti campi di intestazione. La modifica di un campo di intestazione influisce su tutte le colonne o parametri.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Un descrittore contiene zero o più record del descrittore. Ogni record descrive una colonna o parametro, a seconda del tipo di descrittore. Quando è associato una nuova colonna o parametro, viene aggiunto un nuovo record per il descrittore. Quando una colonna o parametro non è associato, un record viene rimosso dal descrittore. Ogni record contiene una sola copia dei campi seguenti:  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 Numero di attributi di istruzione corrisponde al campo di intestazione di un descrittore. L'impostazione di questi attributi tramite una chiamata a **SQLSetStmtAttr** e impostando il campo di intestazione corrispondente descrittore chiamando **SQLSetDescField** hanno lo stesso effetto. Lo stesso vale per **SQLGetStmtAttr** e **SQLGetDescField**, entrambi di cui recuperare le stesse informazioni. Chiamare le funzioni di istruzione anziché le funzioni di descrittore ha il vantaggio che un handle di descrittore non devono essere recuperati.  
  
 Impostando gli attributi di istruzione, è possono impostare i campi di intestazione seguente:  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Conteggio record](../../../odbc/reference/develop-app/record-count.md)  
  
-   [Record del descrittore associato](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [Campi posticipati](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [Verifica della coerenza](../../../odbc/reference/develop-app/consistency-check.md)
