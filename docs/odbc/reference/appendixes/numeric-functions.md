---
title: Funzioni numeriche | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47711a7e974373e9da4ac8068295029d88accaf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181300"
---
# <a name="numeric-functions"></a>Funzioni numeriche
La tabella seguente descrive le funzioni numeriche che sono inclusi nel set di funzioni scalari ODBC. Chiamando **SQLGetInfo** con un *tipo di informazioni* di SQL_NUMERIC_FUNCTIONS, un'applicazione può determinare quali funzioni numeriche sono supportate da un driver.  
  
 Tutte le funzioni numeriche restituiscono i valori del tipo di dati SQL_FLOAT tranne ABS, ROUND, TRUNCATE, SIGN, FLOOR e CEILING, che restituiscono i valori degli stessi dati digitare come parametri di input.  
  
 Gli argomenti indicati come *numeric_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare o una *numerico litera*l, dove il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL _ DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL o SQL_DOUBLE.  
  
 Gli argomenti indicati come *float_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare o una *letterali numerici*, in cui il tipo di dati sottostante può essere rappresentato come SQL_FLOAT.  
  
 Gli argomenti indicati come *integer_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare o una *letterali numerici*, in cui il tipo di dati sottostante può essere rappresentato come SQL_TINYINT, SQL _ SMALLINT SQL_INTEGER o SQL_BIGINT.  
  
 Le funzioni scalari funzione CURRENT_DATE CURRENT_TIME e CURRENT_TIMESTAMP sono stati aggiunti nella versione 3.0 di ODBC per la compatibilità con SQL-92.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**ABS(** _numeric_exp_ **)**  (ODBC 1.0)|Restituisce il valore assoluto del *numeric_exp*.|  
|**ACOS(** _float_exp_ **)**  (ODBC 1.0)|Restituisce l'arcocoseno di *float_exp* come un angolo, espresso in radianti.|  
|**ASIN(** _float_exp_ **)**  (ODBC 1.0)|Restituisce l'arcoseno di *float_exp* come un angolo, espresso in radianti.|  
|**ATAN(** _float_exp_ **)**  (ODBC 1.0)|Restituisce l'arcotangente del *float_exp* come un angolo, espresso in radianti.|  
|**ATAN2(** _float_exp1_, _float_exp2_ **)**  (ODBC 2.0)|Restituisce l'arcotangente del *x* e *y* coordinate, specificate dal *float_exp1* e *float_exp2*, rispettivamente, come un angolo espresso in radianti.|  
|**CEILING (** _numeric_exp_ **)** (1.0 ODBC)|Restituisce il più piccolo intero maggiore o uguale a *numeric_exp*. Il valore restituito è dello stesso tipo di dati come parametro di input.|  
|**COS(** _float_exp_ **)**  (ODBC 1.0)|Restituisce il coseno *float_exp*, dove *float_exp* corrisponde a un angolo espresso in radianti.|  
|**COT(** _float_exp_ **)**  (ODBC 1.0)|Restituisce la cotangente *float_exp*, dove *float_exp* corrisponde a un angolo espresso in radianti.|  
|**DEGREES(** _numeric_exp_ **)**  (ODBC 2.0)|Restituisce il numero di gradi convertito da *numeric_exp* radianti.|  
|**EXP(** _float_exp_ **)**  (ODBC 1.0)|Restituisce il valore esponenziale del *float_exp*.|  
|**FLOOR(** _numeric_exp_ **)**  (ODBC 1.0)|Restituisce l'intero massimo minore o uguale a *numeric_exp*. Il valore restituito è dello stesso tipo di dati come parametro di input.|  
|**LOG(** _float_exp_ **)**  (ODBC 1.0)|Restituisce il logaritmo naturale del *float_exp*.|  
|**LOG10(** _float_exp_ **)**  (ODBC 2.0)|Logaritmo restituisce la base 10 del *float_exp*.|  
|**MOD(** _integer_exp1_, _integer_exp2_ **)**  (ODBC 1.0)|Restituisce il resto (modulo) di *integer_exp1* diviso *integer_exp2*.|  
|**PI( )**  (ODBC 1.0)|Restituisce il valore costante di pi greco sotto forma di valore a virgola mobile.|  
|**POWER (** _numeric_exp_, _integer_exp_ **)** (ODBC 2.0)|Restituisce il valore del *numeric_exp* elevato alla potenza di *integer_exp*.|  
|**RADIANS(** _numeric_exp_ **)**  (ODBC 2.0)|Restituisce il numero di radianti convertito da *numeric_exp* gradi.|  
|**RAND(** [*integer_exp*] **)**  (ODBC 1.0)|Restituisce un valore a virgola mobile casuale utilizzando *integer_exp* come valore di inizializzazione facoltativa.|  
|**ROUND(** _numeric_exp_, _integer_exp_ **)**  (ODBC 2.0)|Restituisce *numeric_exp* arrotondato *integer_exp* posizioni a destra del separatore decimale. Se *integer_exp* è un valore negativo *numeric_exp* viene arrotondato a &#124; *integer_exp* &#124; posizioni a sinistra del separatore decimale.|  
|**SIGN(** _numeric_exp_ **)**  (ODBC 1.0)|Restituisce un indicatore di accesso di *numeric_exp*. Se *numeric_exp* è minore di zero, -1 viene restituito. Se *numeric_exp* è uguale a zero, viene restituito 0. Se *numeric_exp* è maggiore di zero, viene restituito 1.|  
|**SIN(** _float_exp_ **)**  (ODBC 1.0)|Restituisce il seno *float_exp*, dove *float_exp* corrisponde a un angolo espresso in radianti.|  
|**SQRT(** _float_exp_ **)**  (ODBC 1.0)|Restituisce la radice quadrata *float_exp*.|  
|**TAN(** _float_exp_ **)**  (ODBC 1.0)|Restituisce la tangente *float_exp*, dove *float_exp* corrisponde a un angolo espresso in radianti.|  
|**TRUNCATE(** _numeric_exp_, _integer_exp_ **)**  (ODBC 2.0)|Restituisce *numeric_exp* troncato *integer_exp* posizioni a destra del separatore decimale. Se *integer_exp* è un valore negativo *numeric_exp* viene troncato a &#124; *integer_exp* &#124; posizioni a sinistra del separatore decimale.|
