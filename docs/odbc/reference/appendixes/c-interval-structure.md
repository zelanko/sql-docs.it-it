---
title: Struttura C Interval | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbd920b77fd44eaf4765f0983d7d16feb31a4d91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026586"
---
# <a name="c-interval-structure"></a>Struttura C Interval
Ognuno dei tipi di dati di intervallo C elencati nella [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) sezione Usa la stessa struttura per contenere i dati di intervallo. Quando **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** viene chiamato, il driver restituisce i dati nella struttura SQL_INTERVAL_STRUCT, utilizza il valore specificato per il applicazione per i tipi di dati C (nella chiamata a **SQLBindCol**, **SQLGetData**, o **SQLBindParameter**) per interpretare il contenuto di SQL_INTERVAL_STRUCT e popolare la *interval_type* campo della struttura con i *enum* valore corrispondente al tipo C. Si noti che i driver non leggono i *interval_type* campo per determinare il tipo dell'intervallo; si recupera il valore del campo descrittore SQL_DESC_CONCISE_TYPE. Quando la struttura viene utilizzata per i dati dei parametri, il driver Usa il valore specificato dall'applicazione nel campo SQL_DESC_CONCISE_TYPE di APD per interpretare il contenuto di SQL_INTERVAL_STRUCT, anche se l'applicazione imposta il valore della  *interval_type* campo su un valore diverso.  
  
 Questa struttura viene definita come segue:  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 Il *interval_type* campo del SQL_INTERVAL_STRUCT indica all'applicazione struttura viene mantenuto nell'unione e anche quali membri della struttura sono rilevanti. Il *interval_sign* campo ha il valore SQL_FALSE se l'intervallo iniziale campo è senza segno; in caso affermativo SQL_TRUE il campo iniziale è negativo. Il valore nel campo di leader stesso è sempre non firmato, indipendentemente dal valore della *interval_sign*. Il *interval_sign* campo agisce come un bit di segno.
