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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073808"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapping di SQLGetStmtOption
Quando un'applicazione chiama **SQLGetStmtOption** a un database ODBC *3.x* driver che non la supporta, la chiamata a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 verrà generato come indicato di seguito:  
  
-   Se *fOption* indica un'opzione dell'istruzione definite da ODBC che restituisce una stringa, le chiamate di gestione Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione dell'istruzione definite da ODBC che restituisce un valore integer a 32 bit, le chiamate di gestione Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione di istruzione definiti dal driver, le chiamate di gestione Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nei tre casi precedenti, il *StatementHandle* argomento è impostato sul valore *hstmt*, il *attributo* argomento è impostato sul valore in *fOption* e il *ValuePtr* argomento è impostato sullo stesso valore come *il parametro pvParam*.  
  
 Per le opzioni di connessione di stringa definite da ODBC, gestione Driver imposta il *BufferLength* argomento nella chiamata a **SQLGetConnectAttr** alla lunghezza massima predefinita (SQL_MAX_OPTION_STRING_LENGTH); per un'opzione di connessione, non di tipo stringa *BufferLength* è impostato su 0.  
  
 L'opzione dell'istruzione SQL_GET_BOOKMARK è stata deprecata in ODBC *3.x*. Per un database ODBC *3.x* driver per lavorare con ODBC *2.x* le applicazioni che usano SQL_GET_BOOKMARK, deve supportare SQL_GET_BOOKMARK. Per un database ODBC *3.x* driver per lavorare con ODBC *2.x* applicazioni, deve supportare l'impostazione SQL_USE_BOOKMARKS su SQL_UB_ON e deve esporre segnalibri di lunghezza fissa. Se un database ODBC *3.x* driver supporta solo segnalibri di lunghezza variabile, i segnalibri non a lunghezza fissa, l'app deve restituire SQLSTATE HYC00 (funzionalità facoltativa non implementata) se un database ODBC *2.x* tenta di applicazione impostare SQL_USE_BOOKMARKS SQL_UB_ON.  
  
 Per un database ODBC *3.x* driver, gestione Driver non verifica più per vedere se *opzione* compresa tra SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX, oppure è maggiore di SQL_CONNECT_OPT_DRVR_START. Il driver necessario selezionare questa opzione.
