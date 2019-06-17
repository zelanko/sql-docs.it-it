---
title: Descrittori e Desktop driver di Database | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17058af1d7f0ab1e35c2d6b31c0337daed4c9e01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240392"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descrittori e driver di database desktop
Un descrittore è una struttura di dati che contiene informazioni sui dati delle colonne o parametri dinamici. **SQLGetDescField** può essere utilizzato per recuperare i descrittori supportati elencati di seguito. I descrittori di parametri di implementazione (IPD) non vengono popolate automaticamente in quanto **SQLDescribeParam** non è supportato. I campi di descrizione che non sono disponibili tramite Jet (ad esempio SQL_DESC_BASE_TABLE_NAME) non sono inoltre supportati.  
  
 Per altre informazioni sui campi di descrizione Jet supportati, vedere la *Guida per programmatori di Microsoft Jet Database Engine*.  
  
 Per altre informazioni sui descrittori, vedere gli argomenti in "Descrittori" nel *riferimento per programmatori ODBC*.  
  
|Campi di descrizione|Livello di supporto|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Supportato|  
|SQL_DESC_ARRAY_SIZE|Supportato solo per ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Supportato|  
|SQL_DESC_BIND_OFFSET_PTR|Supportato|  
|SQL_DESC_BIND_TYPE|Supportato|  
|SQL_DESC_COUNT|Supportato|  
|SQL_DESC_ROWS_PROCESSED_PTR|Supportato solo per ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Supportato|  
|SQL_DESC_BASE_COLUMN_NAME|Supportato (nuovo)|  
|SQL_DESC_BASE_TABLE_NAME|Supportato (nuovo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Non supportato|  
|SQL_DESC_CONCISE_TYPE|Supportato|  
|SQL_DESC_DATA_PTR|Supportato|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Supportato|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Supportato per i tipi di intervallo C|  
|SQL_DESC_DISPLAY_SIZE|Supportato|  
|SQL_DESC_FIXED_PREC_SCALE|Supportato (TRUE per denaro)|  
|SQL_DESC_INDICATOR_PTR|Supportato|  
|SQL_DESC_LABEL|Supportato|  
|SQL_DESC_LENGTH|Supportato|  
|SQL_DESC_LITERAL_PREFIX|Supportato|  
|SQL_DESC_LITERAL_SUFFIX|Supportato|  
|SQL_DESC_LOCAL_TYPE_NAME|(Restituisce una stringa vuota) non è supportato|  
|SQL_DESC_NAME|Supportato|  
|SQL_DESC_NULLABLE|Supportato<br /><br /> **Nota** non è supportato nelle versioni precedenti di Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Supportato|  
|SQL_DESC_OCTET_LENGTH|Supportato|  
|SQL_DESC_OCTET_LENGTH_PTR|Supportato|  
|SQL_DESC_PARAMETER_TYPE|Solo i parametri di input|  
|SQL_DESC_PRECISION|Supportato|  
|SQL_DESC_SCALE|Supportato|  
|SQL_DESC_SCHEMA_NAME|Non supportato|  
|SQL_DESC_SEARCHABLE|Supportato|  
|SQL_DESC_TABLE_NAME|Non supportato|  
|SQL_DESC_TYPE|Supportato|  
|SQL_DESC_TYPE_NAME|Supportato|  
|SQL_DESC_UNNAMED|Supportato|  
|SQL_DESC_UNSIGNED|Supportato|  
|SQL_DESC_UPDATABLE|Supportato|
