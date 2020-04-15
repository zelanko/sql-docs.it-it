---
title: 'Mapping di SQLGetStmtOption : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300601"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapping di SQLGetStmtOption
Quando un'applicazione chiama **SQLGetStmtOption** a un driver ODBC *3.x* che non lo supporta, la chiamata a  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 come segue:  
  
-   Se *fOption* indica un'opzione di istruzione definita da ODBC che restituisce una stringa, Gestione Driver chiama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione di istruzione definita da ODBC che restituisce un valore integer a 32 bit, Gestione Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indica un'opzione di istruzione definita dal driver, Gestione Driver chiama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nei tre casi precedenti, l'argomento *StatementHandle* è impostato sul valore in *hstmt*, l'argomento *Attribute* è impostato sul valore in *fOption*e l'argomento *ValuePtr* è impostato sullo stesso valore di *pvParam*.  
  
 Per le opzioni di connessione di stringa definite da ODBC, Gestione Driver imposta il *BufferLength* argomento nella chiamata a **SQLGetConnectAttr** per la lunghezza massima predefinita (SQL_MAX_OPTION_STRING_LENGTH); per un'opzione di connessione non stringa, *BufferLength* è impostato su 0.  
  
 L'opzione SQL_GET_BOOKMARK'istruzione è deprecata in ODBC *3.x*. Affinché un driver ODBC *3.x* funzioni con le applicazioni ODBC *2.x* che utilizzano SQL_GET_BOOKMARK, deve supportare SQL_GET_BOOKMARK. Affinché un driver ODBC *3.x* funzioni con le applicazioni ODBC *2.x,* deve supportare l'impostazione di SQL_USE_BOOKMARKS per SQL_UB_ON e deve esporre segnalibri a lunghezza fissa. Se un driver ODBC *3.x* supporta solo segnalibri a lunghezza variabile, non segnalibri a lunghezza fissa, deve restituire SQLSTATE HYC00 (funzionalità facoltativa non implementata) se un'applicazione ODBC *2.x* tenta di impostare SQL_USE_BOOKMARKS su SQL_UB_ON.  
  
 Per un driver ODBC *3.x,* Gestione Driver non controlla più se *Option* è tra SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX o è maggiore di SQL_CONNECT_OPT_DRVR_START. Il conducente deve controllare questo.
