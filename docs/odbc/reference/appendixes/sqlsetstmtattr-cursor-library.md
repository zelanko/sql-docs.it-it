---
title: SQLSetStmtAttr (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d4e5bd6ec27891e80933dfcc42beec9056d2d3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735209"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetStmtAttr** funzione nella libreria di cursori. Per informazioni generali sul **SQLSetStmtAttr**, vedere [funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 La libreria di cursori supporta i seguenti attributi di istruzione con **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 La libreria di cursori supporta solo i valori dell'attributo SQL_ATTR_CURSOR_TYPE istruzione SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC.  
  
 Per i cursori forward-only, la libreria di cursori supporta il valore SQL_CONCUR_READ_ONLY l'attributo di istruzione SQL_ATTR_CONCURRENCY. Per i cursori statici, la libreria di cursori supporta i valori SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES dell'attributo di istruzione SQL_ATTR_CONCURRENCY.  
  
 La libreria di cursori supporta solo il valore SQL_SC_NON_UNIQUE l'attributo di istruzione SQL_ATTR_SIMULATE_CURSOR.  
  
 Sebbene la specifica ODBC supporta le chiamate a **SQLSetStmtAttr** con gli attributi SQL_ATTR_PARAM_BIND_TYPE o SQL_ATTR_ROW_BIND_TYPE dopo **SQLFetch** o **SQLFetchScroll**  è stato chiamato, il cursore della libreria non esiste. Prima che è possibile modificare il tipo di associazione nella libreria di cursori, l'applicazione deve chiudere il cursore. La libreria di cursori supporta la modifica SQL_ATTR_ROW_BIND_OFFSET_PTR SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e gli attributi di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR quando un cursore è aperto.  
  
 Un'applicazione può chiamare **SQLSetStmtAttr** con un **attributo** di SQL_ATTR_ROW_ARRAY_SIZE per modificare le dimensioni del set di righe mentre è aperto un cursore. La nuova dimensione di set di righe sarà effettive la volta successiva **SQLFetchScroll** oppure **SQLFetch** viene chiamato.  
  
 La libreria di cursori supporta l'impostazione dell'attributo di istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR o SQL_ATTR_ROW_BIND_OFFSET_PTR per abilitare gli offset di associazione. L'offset di associazione non verrà utilizzato per le chiamate a **SQLFetch** quando si usa la libreria di cursori con un'API ODBC 2. *x* driver.  
  
 La libreria di cursori supporta impostando l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE.
