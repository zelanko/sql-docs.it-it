---
title: 'Mapping di SQLSetStmtOption : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91264cee0dfceeb7195e2bad40d1638a88e1e01a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304902"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapping di SQLSetStmtOption
Quando un'applicazione chiama **SQLSetStmtOption** tramite un driver ODBC *3.x,* la chiamata a  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 come segue:  
  
-   Se *fOption* indica un attributo di istruzione definito da ODBC che è una stringa, Gestione Driver chiama  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica un attributo di istruzione definito da ODBC che restituisce un valore integer a 32 bit, Gestione Driver chiama  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica un attributo di istruzione definito dal driver, Gestione Driver chiama  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nei tre casi precedenti, l'argomento **StatementHandle** è impostato sul valore in *hstmt*, l'argomento *Attribute* è impostato sul valore in *fOption*e l'argomento *ValuePtr* è impostato sul valore come *vParam*.  
  
 Poiché Gestione Driver non sa se l'attributo di istruzione definita dal driver richiede una stringa o un valore integer a 32 bit, deve passare un valore valido per il *StringLength* argomento di **SQLSetStmtAttr**. Se il driver ha definito una semantica speciale per gli attributi di istruzione definita dal driver e deve essere chiamato utilizzando **SQLSetStmtOption**, deve supportare **SQLSetStmtOption**.  
  
 Se un'applicazione chiama **SQLSetStmtOption** per impostare un'opzione di istruzione specifica del driver in un driver ODBC *3.x* e l'opzione è stata definita in una versione ODBC *2.x* del driver, una nuova costante di manifesto deve essere definita per l'opzione nel driver ODBC *3.x.* Se la vecchia costante del manifesto viene utilizzata nella chiamata a **SQLSetStmtOption**, Gestione Driver chiamerà **SQLSetStmtAttr** con il *StringLength* argomento impostato su 0.  
  
 Quando un'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_USE_BOOKMARKS su SQL_UB_ON in un driver ODBC *3.x,* l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è impostato su SQL_UB_FIXED. SQL_UB_ON è la stessa costante di SQL_UB_FIXED. Gestione Driver passa SQL_UB_FIXED al driver. SQL_UB_FIXED è stata deprecata in ODBC *3.x*, ma un driver ODBC *3.x* deve implementarlo per funzionare con le applicazioni ODBC *2.x* che utilizzano segnalibri a lunghezza fissa.  
  
 Per un driver ODBC *3.x,* Gestione Driver non controlla più se *Option* è tra SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX o è maggiore di SQL_CONNECT_OPT_DRVR_START.
