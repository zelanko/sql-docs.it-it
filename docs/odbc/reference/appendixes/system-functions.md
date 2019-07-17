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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070088"
---
# <a name="system-functions"></a>Funzioni di sistema
La tabella seguente elenca le funzioni di sistema inclusi nel set di funzioni scalari ODBC. Chiamando **SQLGetInfo** con un *tipo di informazioni* di SQL_SYSTEM_FUNCTIONS, un'applicazione può determinare le funzioni di sistema supportate da un driver.  
  
 Gli argomenti indicati come *exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare o un valore letterale, in cui il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL _BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *valore* può essere una valore letterale costante, in cui il tipo di dati sottostante può essere rappresentato come SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 Valori restituiti sono rappresentati come tipi di dati ODBC.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**DATABASE( )**  (ODBC 1.0)|Restituisce il nome del database corrispondente all'handle di connessione. (Il nome del database è disponibile anche tramite la chiamata **SQLGetConnectOption** con l'opzione di connessione SQL_CURRENT_QUALIFIER.)|  
|**IFNULL (** _exp_,_valore_ **)** (1.0 ODBC)|Se *exp* è null, *valore* viene restituito. Se *exp* non è null, *exp* viene restituito. Il tipo di dati o i tipi di *valore* deve essere compatibile con il tipo di dati *exp*.|  
|**USER( )**  (ODBC 1.0)|Restituisce il nome utente nel sistema DBMS. (Il nome utente è anche disponibile tramite **SQLGetInfo** specificando il tipo di informazioni: SQL_USER_NAME.) Ciò può essere diverso dal nome di account di accesso.|
