---
title: C Struttura dell'intervallo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c86ebe24a0e12531e355f95185b01f3089a31b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292153"
---
# <a name="c-interval-structure"></a>Struttura C Interval
Ognuno dei tipi di dati dell'intervallo C elencati nella sezione [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) utilizza la stessa struttura per contenere i dati dell'intervallo. Quando vengono chiamate **SQLFetch**, **SQLFetchScroll**o **SQLGetData** , il driver restituisce dati nella struttura SQL_INTERVAL_STRUCT, utilizza il valore specificato dall'applicazione per i tipi di dati C (nella chiamata a **SQLBindCol**, **SQLGetData**o **SQLBindParameter**) per interpretare il contenuto di SQL_INTERVAL_STRUCT e popola il campo *interval_type* della struttura con il valore *di enumerazione* corrispondente al tipo C. Si noti che i driver non leggono il campo *interval_type* per determinare il tipo di intervallo; recuperano il valore del campo descrittore SQL_DESC_CONCISE_TYPE. Quando la struttura viene utilizzata per i dati dei parametri, il driver utilizza il valore specificato dall'applicazione nel campo SQL_DESC_CONCISE_TYPE dell'Oggetto APD per interpretare il contenuto di SQL_INTERVAL_STRUCT, anche se l'applicazione imposta il valore del campo *interval_type* su un valore diverso.  
  
 Questa struttura è definita come segue:  
  
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
  
 Il *interval_type* campo della SQL_INTERVAL_STRUCT indica all'applicazione quale struttura è detenuta nell'unione e anche quali sono rilevanti i membri della struttura. Il campo *interval_sign* ha il valore SQL_FALSE se il campo intere dell'intervallo è senza segno; se è SQL_TRUE, il campo iniziale è negativo. Il valore nel campo iniziale stesso è sempre senza segno, indipendentemente dal valore di *interval_sign*. Il campo *interval_sign* funge da bit di segno.
