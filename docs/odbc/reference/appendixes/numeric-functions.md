---
title: Funzioni Numeriche Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299871"
---
# <a name="numeric-functions"></a>Funzioni numeriche
Nella tabella seguente vengono descritte le funzioni numeriche incluse nel set di funzioni scalari ODBC. Chiamando **SQLGetInfo** con un tipo di *informazioni* di SQL_NUMERIC_FUNCTIONS, un'applicazione può determinare quali funzioni numeriche sono supportate da un driver.  
  
 Tutte le funzioni numeriche restituiscono valori di tipo SQL_FLOAT ad eccezione di ABS, ROUND, TRUNCATE, SIGN, FLOOR e CEILING, che restituiscono valori dello stesso tipo di dati dei parametri di input.  
  
 Gli argomenti indicati come *numeric_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o una *litiera numerica,* in cui il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT SQL_REAL o SQL_DOUBLE.  
  
 Gli argomenti indicati come *float_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un *valore numerico-letterale*, in cui il tipo di dati sottostante può essere rappresentato come SQL_FLOAT.  
  
 Gli argomenti indicati come *integer_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un *valore numerico-letterale*, in cui il tipo di dati sottostante può essere rappresentato come SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER o SQL_BIGINT.  
  
 Le funzioni scalari CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP sono state aggiunte in ODBC 3.0 per allinearsi a SQL-92.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**ABS(** _numeric_exp_ **)** (ODBC 1.0)|Restituisce il valore assoluto di *numeric_exp*.|  
|**ACOS(** _float_exp_ **)** (ODBC 1.0)|Restituisce l'arcocoseno di *float_exp* come angolo, espresso in radianti.|  
|**ASIN(** _float_exp_ **)** (ODBC 1.0)|Restituisce l'arcoseno di *float_exp* come angolo, espresso in radianti.|  
|**ATAN(** _FLOAT_EXP_ **)** (ODBC 1.0)|Restituisce l'arcotangente di *float_exp* come angolo, espresso in radianti.|  
|**ATAN2(** _float_exp1_ _, float_exp2_**)** (ODBC 2.0)|Restituisce l'arcotangente delle coordinate *x* e *y,* specificate rispettivamente da *float_exp1* e *float_exp2*, come angolo, espresse in radianti.|  
|**ARROTONDA.** _numeric_exp_ **)** (ODBC 1.0)|Restituisce il numero intero più piccolo maggiore o uguale a *numeric_exp*. Il valore restituito è dello stesso tipo di dati del parametro di input.|  
|**COS(** _float_exp_ **)** (ODBC 1.0)|Restituisce il coseno di *float_exp*, dove *float_exp* è un angolo espresso in radianti.|  
|**COT(** _float_exp_ **)** (ODBC 1.0)|Restituisce la cotangente di *float_exp*, dove *float_exp* è un angolo espresso in radianti.|  
|**DEGREES(** _numeric_exp_ **)** (ODBC 2.0)|Restituisce il numero di gradi convertiti da *numeric_exp* radianti.|  
|**EXP(** _float_exp_ **)** (ODBC 1.0)|Restituisce il valore esponenziale di *float_exp*.|  
|**FLOOR(** _NUMERIC_EXP_ **)** (ODBC 1.0)|Restituisce il numero intero più grande minore o uguale a *numeric_exp.* Il valore restituito è dello stesso tipo di dati del parametro di input.|  
|**LOG(** _float_exp_ **)** (ODBC 1.0)|Restituisce il logaritmo naturale di *float_exp*.|  
|**LOG10(** _float_exp_ **)** (ODBC 2.0)|Restituisce il logaritmo in base 10 di *float_exp.*|  
|**MOD(** _integer_exp1_, _integer_exp2_**)** (ODBC 1.0)|Restituisce il resto (modulo) di *integer_exp1* diviso *per integer_exp2.*|  
|**PI( )** (ODBC 1.0)|Restituisce il valore costante di pi greco come valore a virgola mobile.|  
|**POWER(** _numeric_exp_ _, integer_exp_**)** (ODBC 2.0)|Restituisce il valore di *numeric_exp* alla potenza di *integer_exp.*|  
|**RADIANTI(** _numeric_exp_ **)** (ODBC 2.0)|Restituisce il numero di radianti convertiti da *numeric_exp* gradi.|  
|**RAND(**[*integer_exp*]**)** (ODBC 1.0)|Restituisce un valore a virgola mobile casuale utilizzando *integer_exp* come valore di seed facoltativo.|  
|**ARROTONDA(** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Restituisce *numeric_exp* arrotondato a *integer_exp* posizioni a destra della virgola decimale. Se *integer_exp* è negativo, *numeric_exp* viene arrotondato a *&#124;integer_exp*&#124; posizioni a sinistra della virgola decimale.|  
|**SEGNO(** _numeric_exp_ **)** (ODBC 1.0)|Restituisce un indicatore del segno di *numeric_exp*. Se *numeric_exp* è minore di zero, viene restituito -1. Se *numeric_exp* è uguale a zero, viene restituito 0. Se *numeric_exp* è maggiore di zero, viene restituito 1.|  
|**SIN(** _float_exp_ **)** (ODBC 1.0)|Restituisce il sine di *float_exp*, in cui *float_exp* è un angolo espresso in radianti.|  
|**SQRT(** _float_exp_ **)** (ODBC 1.0)|Restituisce la radice quadrata di *float_exp*.|  
|**TAN(** _float_exp_ **)** (ODBC 1.0)|Restituisce la tangente di *float_exp*, dove *float_exp* è un angolo espresso in radianti.|  
|**TRUNCATE(** _numeric_exp_ _, integer_exp_**)** (ODBC 2.0)|Restituisce *numeric_exp* troncato a *integer_exp* posizioni a destra del separatore decimale. Se *integer_exp* è negativo, *numeric_exp* viene troncato in *&#124;integer_exp*&#124; a sinistra del separatore decimale.|
