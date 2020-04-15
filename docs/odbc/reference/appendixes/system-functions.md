---
title: Funzioni di sistema Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302832"
---
# <a name="system-functions"></a>Funzioni di sistema
Nella tabella seguente sono elencate le funzioni di sistema incluse nel set di funzioni scalari ODBC. Chiamando **SQLGetInfo** con un tipo di *informazioni* di SQL_SYSTEM_FUNCTIONS, un'applicazione può determinare quali funzioni di sistema sono supportate da un driver.  
  
 Gli argomenti indicati come *exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un valore letterale, in cui il tipo di dati sottostante potrebbe essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE SQL_TYPE_TIME, o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *valore* possono essere una costante letterale, in cui il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 I valori restituiti sono rappresentati come tipi di dati ODBC.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**DATABASE( )** (ODBC 1.0)|Restituisce il nome del database corrispondente all'handle di connessione. Il nome del database è disponibile anche chiamando **SQLGetConnectOption** con l'opzione di connessione SQL_CURRENT_QUALIFIER.|  
|**SENULL(** _exp_,_valore_**)** (ODBC 1.0)|Se *exp* è null, viene restituito *value.* Se *exp* non è null, *exp* viene restituito. Il tipo di dati o i tipi di *valore* possibili devono essere compatibili con il tipo di dati di *exp*.|  
|**UTENTE( )** (ODBC 1.0)|Restituisce il nome utente nel DBMS. Il nome utente è disponibile anche tramite **SQLGetInfo** specificando il tipo di informazioni: SQL_USER_NAME. Questo può essere diverso dal nome di accesso.|
