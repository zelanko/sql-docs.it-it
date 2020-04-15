---
title: 'Mapping di SQLSetScrollOptions : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77050df283b10abd17ba62a48bd366d6c1b3f601
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300501"
---
# <a name="sqlsetscrolloptions-mapping"></a>Mapping di SQLSetScrollOptions
Quando un'applicazione chiama **SQLSetScrollOptions** tramite un driver ODBC *3.x* e il driver non supporta **SQLSetScrollOptions**, la chiamata a  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 come segue:  
  
-   Una chiamata a  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     con l'argomento *InfoType* impostato su uno dei valori riportati nella tabella seguente, a seconda del valore dell'argomento *KeysetSize* in **SQLSetScrollOptions**.  
  
    |*Argomento KeysetSize*|*Argomento InfoType*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Un valore maggiore dell'argomento *RowsetSize*|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se il valore dell'argomento *KeysetSize* non è elencato nella tabella precedente, la chiamata a **SQLSetScrollOptions** restituisce SQLSTATE S1107 (valore riga non compreso nell'intervallo) e non viene eseguita alcuna delle operazioni seguenti.  
  
     Gestione Driver verifica quindi se il bit appropriato è impostato nel valore*Di InfoValuePtr* restituito dalla chiamata a **SQLGetInfo**, in base al valore dell'argomento *Concurrency* in **SQLSetScrollOptions**.  
  
    |*Argomento Concorrenza*|*Impostazione InfoType*|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se il *Concurrency* argomento non è uno dei valori nella tabella precedente, la chiamata a **SQLSetScrollOptions** restituisce SQLSTATE S1108 (opzione di concorrenza non compresa nell'intervallo) e nessuno dei passaggi seguenti vengono eseguiti. Se il bit appropriato (come indicato nella tabella precedente) non è impostato in *, InfoValuePtr* su uno dei valori corrispondenti all'argomento *Concorrenza,* la chiamata a **SQLSetScrollOptions** restituisce SQLSTATE S1C00 (Driver non compatibile) e nessuno dei passaggi seguenti viene eseguito.  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     con * \*ValuePtr* impostato su uno dei valori nella tabella seguente, in base al valore dell'argomento *KeysetSize* in **SQLSetScrollOptions**.  
  
    |*Argomento KeysetSize*|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Un valore maggiore dell'argomento *RowsetSize*|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     con * \*ValuePtr* impostato sull'argomento *Concorrenza* in **SQLSetScrollOptions**.  
  
-   Se l'argomento *KeysetSize* nella chiamata a **SQLSetScrollOptions** è positivo,  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     con * \*ValuePtr* impostato sull'argomento *KeysetSize* in **SQLSetScrollOptions**.  
  
-   Una chiamata a  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     con * \*ValuePtr* impostato sull'argomento *RowsetSize* in **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando Gestione Driver esegue il mapping di **SQLSetScrollOptions** per un'applicazione che utilizza un driver ODBC *3.x* che non supporta **SQLSetScrollOptions**, Gestione Driver imposta l'opzione di istruzione SQL_ROWSET_SIZE, non l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE , per il *RowsetSize* argomento **SQLSetScrollOption**. Di conseguenza, **SQLSetScrollOptions** non può essere utilizzato da un'applicazione durante il recupero di più righe da una chiamata a **SQLFetch** o **SQLFetchScroll**. e può essere utilizzato solo quando si recuperano più righe mediante una chiamata a **SQLExtendedFetch**.
