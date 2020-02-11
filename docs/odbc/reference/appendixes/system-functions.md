---
title: Funzioni di sistema | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0c7817d37e14ad07b9cc64f59691c27cf665177
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070088"
---
# <a name="system-functions"></a>Funzioni di sistema
Nella tabella seguente sono elencate le funzioni di sistema incluse nel set di funzioni scalari ODBC. Chiamando **SQLGetInfo** con un *tipo di informazioni* SQL_SYSTEM_FUNCTIONS, un'applicazione può determinare quali funzioni di sistema sono supportate da un driver.  
  
 Gli argomenti identificati come *Exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un valore letterale, in cui il tipo di dati sottostante potrebbe essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti denotati come *valore* possono essere una costante letterale, in cui il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 I valori restituiti sono rappresentati come tipi di dati ODBC.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**Database ()** (ODBC 1,0)|Restituisce il nome del database corrispondente all'handle di connessione. Il nome del database è disponibile anche chiamando **SQLGetConnectOption** con l'opzione di connessione SQL_CURRENT_QUALIFIER.|  
|**IFNULL (** _Exp_,_valore_**)** (ODBC 1,0)|Se *Exp* è null, viene restituito *value* . Se *Exp* non è null, viene restituito *Exp* . Il tipo di dati o i tipi di *valore* possibili devono essere compatibili con il tipo di dati di *Exp*.|  
|**Utente ()** (ODBC 1,0)|Restituisce il nome utente nel sistema DBMS. (Il nome utente è disponibile anche per mezzo di **SQLGetInfo** specificando il tipo di informazioni: SQL_USER_NAME.) Questo può essere diverso dal nome dell'account di accesso.|
