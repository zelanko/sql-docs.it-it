---
title: Mapping di SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06b6b0f982b5c8d864e5024c8544f1f8e9af75ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091702"
---
# <a name="sqlsetscrolloptions-mapping"></a>Mapping di SQLSetScrollOptions
Quando un'applicazione chiama **SQLSetScrollOptions** tramite un database ODBC *3.x* e il driver non supporta **SQLSetScrollOptions**, la chiamata a  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 verrà generato come indicato di seguito:  
  
-   Una chiamata a  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     con il *InfoType* argomento impostato su uno dei valori nella tabella seguente, in base al valore di *KeysetSize* argomento nel **SQLSetScrollOptions**.  
  
    |*Argomento KeysetSize*|*Argomento InfoType*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Un valore maggiore di *RowsetSize* argomento|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se il valore della *KeysetSize* argomento non è elencato nella tabella precedente, la chiamata a **SQLSetScrollOptions** restituisce SQLSTATE S1107 (valore non compreso nell'intervallo di righe) e nessuna delle operazioni seguenti eseguita.  
  
     The Driver Manager verifica quindi se è impostato il bit appropriato **InfoValuePtr* valore restituito dalla chiamata a **SQLGetInfo**, a seconda del valore della *concorrenza* nell'argomento **SQLSetScrollOptions**.  
  
    |*Concorrenza* argomento|*InfoType* impostazione|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se il *concorrenza* argomento non è uno dei valori nella tabella precedente, la chiamata a **SQLSetScrollOptions** restituisce SQLSTATE S1108 (opzione di concorrenza non compreso nell'intervallo) e nessuna delle operazioni seguenti eseguita. Se il bit appropriato (come indicato nella tabella precedente) non è impostato **InfoValuePtr* a uno dei valori corrispondenti per il *concorrenza* argomento, la chiamata a  **SQLSetScrollOptions** restituisce SQLSTATE S1C00 (Driver non valido) e nessuno dei passaggi seguenti vengono eseguite.  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     con *\*ValuePtr* impostato su uno dei valori nella tabella seguente, in base al valore del *KeysetSize* argomento **SQLSetScrollOptions**.  
  
    |*KeysetSize* argomento|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Un valore maggiore di *RowsetSize* argomento|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     con  *\*ValuePtr* impostata il *concorrenza* argomento nella **SQLSetScrollOptions**.  
  
-   Se il *KeysetSize* argomento nella chiamata a **SQLSetScrollOptions** è positivo, una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     con *\*ValuePtr* impostato sul *KeysetSize* argomento **SQLSetScrollOptions**.  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     con *\*ValuePtr* impostato sul *RowsetSize* argomento **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando esegue il mapping di gestione Driver **SQLSetScrollOptions** per un'applicazione che utilizza un database ODBC *3.x* driver che non supporta **SQLSetScrollOptions**, il Driver Manager imposta l'opzione dell'istruzione SQL_ROWSET_SIZE, non l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul *RowsetSize* nell'argomento **SQLSetScrollOption**. Ne consegue **SQLSetScrollOptions** non può essere utilizzato da un'applicazione durante il recupero di più righe da una chiamata a **SQLFetch** oppure **SQLFetchScroll**. Può essere utilizzato solo quando più durante il recupero di righe da una chiamata a **SQLExtendedFetch**.
