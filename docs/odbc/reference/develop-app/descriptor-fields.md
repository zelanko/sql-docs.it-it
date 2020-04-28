---
title: Campi del descrittore | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94e70de7d237c2eca9aee81979cb19d5295561b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305922"
---
# <a name="descriptor-fields"></a>Campi del descrittore
I descrittori contengono campi di *intestazione* e *record* che descrivono completamente colonne o parametri.  
  
 Un descrittore contiene una sola copia dei campi di intestazione seguenti. La modifica di un campo di intestazione influiscono su tutte le colonne o i parametri.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Un descrittore contiene zero o più record di descrittori. Ogni record descrive una colonna o un parametro, a seconda del tipo di descrittore. Quando viene associata una nuova colonna o un nuovo parametro, al descrittore viene aggiunto un nuovo record. Quando una colonna o un parametro non è associato, un record viene rimosso dal descrittore. Ogni record contiene una sola copia dei campi seguenti:  
  
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
  
 Molti attributi di istruzione corrispondono al campo di intestazione di un descrittore. L'impostazione di questi attributi tramite una chiamata a **SQLSetStmtAttr** e l'impostazione del campo di intestazione del descrittore corrispondente chiamando **SQLSetDescField** hanno lo stesso effetto. Lo stesso vale per **SQLGetStmtAttr** e **SQLGetDescField**, che recuperano entrambe le stesse informazioni. La chiamata alle funzioni dell'istruzione invece che alle funzioni descrittore ha il vantaggio di non dover recuperare un handle del descrittore.  
  
 I campi di intestazione seguenti possono essere impostati impostando gli attributi dell'istruzione:  
  
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
