---
title: Esempio di set di risultati SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5cf62f8a95f4c91095c21a6d603317fe1f73500
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307012"
---
# <a name="example-sqlgettypeinfo-result-set"></a>Esempio di set di risultati SQLGetTypeInfo
Un'applicazione chiama **SQLGetTypeInfo** per determinare quali tipi di dati sono supportati da un'origine dati e le caratteristiche di tali tipi di dati. Nelle tabelle seguenti viene illustrato un set di risultati di esempio restituito da **SQLGetTypeInfo** per un'origine dati che supporta SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR e SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|char|SQL_CHAR|255|"'"|"'"|lunghezza|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<> null|SQL_TRUE|  
|decimale|SQL_DECIMAL|28|\<> null|\<> null|precisione<br />scala|SQL_TRUE|  
|reale|SQL_REAL|7|\<> null|\<> null|\<> null|SQL_TRUE|  
|DateTime|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<> null|SQL_TRUE|  
|"INTERVALLO ANNO () IN ANNO"|SQL_INTERVAL_YEAR|9|"'"|"'"|precisione|SQL_TRUE|  
|"INTERVALLO GIORNO () A FRAZIONE (5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|precisione|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|char|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<> null|SQL_FALSE|\<> null|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|decimale|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|reale|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|DateTime|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|"INTERVALLO ANNO () IN ANNO"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<> null|SQL_FALSE|\<> null|"INTERVALLO GIORNO () A FRAZIONE (5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<> null|\<> null|SQL_CHAR|\<> null|\<> null|\<> null|  
|**SQL_LONGVARCHAR**|\<> null|\<> null|SQL_LONGVARCHAR|\<> null|\<> null|\<> null|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<> null|10|\<> null|  
|**SQL_REAL**|\<> null|\<> null|SQL_REAL|\<> null|10|\<> null|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<> null|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<> null|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<> null|9|
