---
title: Conformità del campo descrittore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 193bdadaf36e975b1f79327bfef161daaaed427b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049852"
---
# <a name="descriptor-field-conformance"></a>Conformità del campo descrittore
Nella tabella seguente indica il livello di conformità di ogni campo di intestazione ODBC descrittore, in cui si è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (per APD IPR rilasciate e IRD); Livello 1 (per ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 Nella tabella seguente indica il livello di conformità di ogni campo di record del descrittore ODBC, in cui si è ben definito.  
  
|Funzione|Livello di conformità|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Livello 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|Livello 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|Livello 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|SQL_DESC_DATETIME_INTERVAL_ CODE|Core[1]|  
|SQL_DESC_DATETIME_INTERVAL_ PRECISION|Core[1]|  
|SQL_DESC_DISPLAY_SIZE|Core|  
|SQL_DESC_FIXED_PREC_SCALE|Core|  
|SQL_DESC_INDICATOR_PTR|Core|  
|SQL_DESC_LABEL|Livello 2|  
|SQL_DESC_LENGTH|Core|  
|SQL_DESC_LITERAL_PREFIX|Core|  
|SQL_DESC_LITERAL_SUFFIX|Core|  
|SQL_DESC_LOCAL_TYPE_NAME|Core|  
|SQL_DESC_NAME|Core|  
|SQL_DESC_NULLABLE|Core|  
|SQL_DESC_OCTET_LENGTH|Core|  
|SQL_DESC_OCTET_LENGTH_PTR|Core|  
|SQL_DESC_PARAMETER_TYPE|Core/livello 2 [2]|  
|SQL_DESC_PRECISION|Core|  
|SQL_DESC_ROWVER|Livello 1|  
|SQL_DESC_SCALE|Core|  
|SQL_DESC_SCHEMA_NAME|Livello 1|  
|SQL_DESC_SEARCHABLE|Core|  
|SQL_DESC_TABLE_NAME|Livello 1|  
|SQL_DESC_TYPE|Core|  
|SQL_DESC_TYPE_NAME|Core|  
|SQL_DESC_UNNAMED|Core|  
|SQL_DESC_UNSIGNED|Core|  
|SQL_DESC_UPDATABLE|Core|  
  
 [1] supporto per questi campi di record è obbligatorio solo se il driver supporta i tipi di dati applicabile.  
  
 [2] per conformità al livello di base, il driver deve supportare SQL_PARAM_INPUT. Per la conformità di interfaccia di livello 2, il driver deve anche supportare SQL_PARAM_INPUT_OUTPUT e SQL_PARAM_OUTPUT.
