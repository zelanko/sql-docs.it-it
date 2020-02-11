---
title: Mapping di SQLGetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2973455ff4ee7e8dc51b2cd07a6423c9b1c36346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68073808"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapping di SQLGetStmtOption
Quando un'applicazione chiama **SQLGetStmtOption** a un driver ODBC *3. x* che non la supporta, la chiamata a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 il risultato è il seguente:  
  
-   Se *fOption* indica un'opzione di istruzione definita da ODBC che restituisce una stringa, gestione driver chiama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione di istruzione definita da ODBC che restituisce un valore integer a 32 bit, gestione driver chiama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione di istruzione definita dal driver, gestione driver chiama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nei tre casi precedenti, l'argomento *statementHandle* è impostato sul valore in *HSTMT*, l'argomento *attribute* è impostato sul valore in *fOption*e l'argomento *ValuePtr* è impostato sullo stesso valore di *pvParam*.  
  
 Per le opzioni di connessione stringa definite da ODBC, gestione driver imposta l'argomento *bufferLength* nella chiamata a **SQLGetConnectAttr** sulla lunghezza massima predefinita (SQL_MAX_OPTION_STRING_LENGTH); per un'opzione di connessione non stringa, *bufferLength* è impostato su 0.  
  
 L'opzione dell'istruzione SQL_GET_BOOKMARK è stata deprecata in ODBC *3. x*. Affinché un driver ODBC *3. x* funzioni con le applicazioni ODBC *2. x* che usano SQL_GET_BOOKMARK, deve supportare SQL_GET_BOOKMARK. Affinché un driver ODBC *3. x* funzioni con le applicazioni ODBC *2. x* , deve supportare l'impostazione SQL_USE_BOOKMARKS per SQL_UB_ON ed esporre segnalibri a lunghezza fissa. Se un driver ODBC *3. x* supporta solo segnalibri a lunghezza variabile, non segnalibri a lunghezza fissa, deve restituire SQLSTATE HYC00 (funzionalità facoltativa non implementata) se un'applicazione ODBC *2. x* tenta di impostare SQL_USE_BOOKMARKS su SQL_UB_ON.  
  
 Per un driver ODBC *3. x* , gestione driver non verifica più se l' *opzione* è compresa tra SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX oppure è maggiore di SQL_CONNECT_OPT_DRVR_START. Il driver deve verificare questa operazione.
