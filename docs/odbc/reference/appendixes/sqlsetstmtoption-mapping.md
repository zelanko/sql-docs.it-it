---
title: SQLSetStmtOption Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad53ba3fa02107d4902c43084beadda7a420e586
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735302"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapping di SQLSetStmtOption
Quando un'applicazione chiama **SQLSetStmtOption** tramite un'applicazione ODBC 3*x* driver, la chiamata a  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 verrà generato come indicato di seguito:  
  
-   Se *fOption* indica un attributo di istruzione definite da ODBC che è una stringa, le chiamate di gestione Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica un attributo di istruzione definite da ODBC che restituisce un valore integer a 32 bit, le chiamate di gestione Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica un attributo di istruzione definiti dal driver, le chiamate di gestione Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nei tre casi precedenti, il **StatementHandle** argomento è impostato sul valore *hstmt*, il *attributo* argomento è impostato sul valore in *fOption* e il *ValuePtr* è impostato sul valore come argomento *vParam*.  
  
 Poiché gestione Driver non sa se l'attributo di istruzione definiti dal driver è necessaria una stringa o un valore integer a 32 bit, deve passare un valore valido per il *StringLength* argomento di **SQLSetStmtAttr**. Se il driver è definita la semantica speciale per gli attributi di istruzione definiti dal driver e deve essere chiamato usando **SQLSetStmtOption**, deve supportare **SQLSetStmtOption**.  
  
 Se un'applicazione chiama **SQLSetStmtOption** per impostare un'opzione di istruzione specifici del driver in un'applicazione ODBC 3 *. x* driver e l'opzione è stata definita in un'API ODBC 2. *x* versione del driver, una nuova costante manifesto deve essere definito per l'opzione in ODBC 3*x* driver. Se la costante manifesto precedente viene usata nella chiamata a **SQLSetStmtOption**, il Driver Manager chiamerà **SQLSetStmtAttr** con il *StringLength* argomento impostato su 0.  
  
 Quando un'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_USE_BOOKMARKS SQL_UB_ON in un'applicazione ODBC 3*x* driver, l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è impostato su SQL_UB_FIXED. SQL_UB_ON è la costante stessa come SQL_UB_FIXED. Gestione Driver restituisce SQL_UB_FIXED tramite il driver. SQL_UB_FIXED è stata deprecata in ODBC 3 *. x*, ma un'applicazione ODBC 3 *. x* driver deve implementare per poterlo utilizzare con l'API ODBC 2. *x* le applicazioni che usano i segnalibri di lunghezza fissa.  
  
 Per un'applicazione ODBC 3 *. x* driver, gestione Driver non controlla se *opzione* compresa tra SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX, oppure è maggiore di SQL_CONNECT_OPT_DRVR_START.
