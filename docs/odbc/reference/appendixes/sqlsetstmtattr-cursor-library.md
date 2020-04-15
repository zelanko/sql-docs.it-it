---
title: SQLSetStmtAttr (libreria di cursori) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300491"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLSetStmtAttr** nella libreria di cursori. Per informazioni generali su **SQLSetStmtAttr**, vedere [Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 La libreria di cursori supporta i seguenti attributi di istruzione con **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 La libreria di cursori supporta solo i valori SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC dell'attributo di istruzione SQL_ATTR_CURSOR_TYPE.  
  
 Per i cursori forward-only, la libreria di cursori supporta il valore SQL_CONCUR_READ_ONLY dell'attributo di istruzione SQL_ATTR_CONCURRENCY. Per i cursori statici, la libreria di cursori supporta i valori SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES dell'attributo di istruzione SQL_ATTR_CONCURRENCY.  
  
 La libreria di cursori supporta solo il valore SQL_SC_NON_UNIQUE dell'attributo di istruzione SQL_ATTR_SIMULATE_CURSOR.  
  
 Sebbene la specifica ODBC supporti le chiamate a **SQLSetStmtAttr** con gli attributi SQL_ATTR_PARAM_BIND_TYPE o SQL_ATTR_ROW_BIND_TYPE dopo la chiamata a **SQLFetch** o **SQLFetchScroll,** la libreria di cursori non lo supporta. Prima di poter modificare il tipo di associazione nella libreria di cursori, l'applicazione deve chiudere il cursore. La libreria di cursori supporta la modifica degli attributi di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_PARAMS_PROCESSED_PTR quando un cursore è aperto.  
  
 Un'applicazione può chiamare **SQLSetStmtAttr** con un **attributo** di SQL_ATTR_ROW_ARRAY_SIZE per modificare la dimensione del set di righe mentre è aperto un cursore. La nuova dimensione del set di righe avrà effetto alla successiva chiamata a **SQLFetchScroll** o **SQLFetch.**  
  
 La libreria di cursori supporta l'impostazione dell'attributo di istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR o SQL_ATTR_ROW_BIND_OFFSET_PTR per abilitare gli offset di associazione. L'offset di associazione non verrà utilizzato per le chiamate a **SQLFetch** quando la libreria di cursori viene utilizzata con un ODBC 2. *driver x.*  
  
 La libreria di cursori supporta l'impostazione dell'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE.
