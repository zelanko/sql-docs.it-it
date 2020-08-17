---
description: Descrittori e driver di database desktop
title: Descrittori e driver di database desktop | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80565f912ef3136dc03cf7216ff3f997ee3eeba3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340797"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descrittori e driver di database desktop
Un descrittore è una struttura di dati che include informazioni sui parametri dinamici o sui dati della colonna. **SQLGetDescField** può essere usato per recuperare i descrittori supportati elencati di seguito. I descrittori di parametri di implementazione (dpi) non vengono popolati automaticamente perché **SQLDescribeParam** non è supportato. Non sono inoltre supportati i campi di descrizione che non sono disponibili tramite Jet, ad esempio SQL_DESC_BASE_TABLE_NAME.  
  
 Per ulteriori informazioni sui campi di descrizione supportati da Jet, vedere *Microsoft jet motore di database Programmer ' s Guide*.  
  
 Per ulteriori informazioni sui descrittori, vedere gli argomenti in "descrittori" in *ODBC Programmer ' s Reference*.  
  
|Campi del descrittore|Livello di supporto|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Funzionalità supportata|  
|SQL_DESC_ARRAY_SIZE|Supportato solo per ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Funzionalità supportata|  
|SQL_DESC_BIND_OFFSET_PTR|Funzionalità supportata|  
|SQL_DESC_BIND_TYPE|Funzionalità supportata|  
|SQL_DESC_COUNT|Funzionalità supportata|  
|SQL_DESC_ROWS_PROCESSED_PTR|Supportato solo per ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Funzionalità supportata|  
|SQL_DESC_BASE_COLUMN_NAME|Supportato (nuovo)|  
|SQL_DESC_BASE_TABLE_NAME|Supportato (nuovo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Non supportate|  
|SQL_DESC_CONCISE_TYPE|Funzionalità supportata|  
|SQL_DESC_DATA_PTR|Funzionalità supportata|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Funzionalità supportata|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Supportato per i tipi di intervallo C|  
|SQL_DESC_DISPLAY_SIZE|Funzionalità supportata|  
|SQL_DESC_FIXED_PREC_SCALE|Supportato (TRUE per Money)|  
|SQL_DESC_INDICATOR_PTR|Funzionalità supportata|  
|SQL_DESC_LABEL|Funzionalità supportata|  
|SQL_DESC_LENGTH|Funzionalità supportata|  
|SQL_DESC_LITERAL_PREFIX|Funzionalità supportata|  
|SQL_DESC_LITERAL_SUFFIX|Funzionalità supportata|  
|SQL_DESC_LOCAL_TYPE_NAME|Non supportato (restituisce una stringa vuota)|  
|SQL_DESC_NAME|Funzionalità supportata|  
|SQL_DESC_NULLABLE|Funzionalità supportata<br /><br /> **Nota** Non supportato nelle versioni precedenti a Jet 4,0|  
|SQL_DESC_NUM_PREC_RADIX|Funzionalità supportata|  
|SQL_DESC_OCTET_LENGTH|Funzionalità supportata|  
|SQL_DESC_OCTET_LENGTH_PTR|Funzionalità supportata|  
|SQL_DESC_PARAMETER_TYPE|Solo parametri di input|  
|SQL_DESC_PRECISION|Funzionalità supportata|  
|SQL_DESC_SCALE|Funzionalità supportata|  
|SQL_DESC_SCHEMA_NAME|Non supportate|  
|SQL_DESC_SEARCHABLE|Funzionalità supportata|  
|SQL_DESC_TABLE_NAME|Non supportate|  
|SQL_DESC_TYPE|Funzionalità supportata|  
|SQL_DESC_TYPE_NAME|Funzionalità supportata|  
|SQL_DESC_UNNAMED|Funzionalità supportata|  
|SQL_DESC_UNSIGNED|Funzionalità supportata|  
|SQL_DESC_UPDATABLE|Funzionalità supportata|
