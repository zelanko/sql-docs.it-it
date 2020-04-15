---
title: SQLSetPos (libreria di cursori) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300511"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLSetPos** nella libreria di cursori. Per informazioni generali su **SQLSetPos**, vedere [Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 La libreria di cursori supporta l'operazione di SQL_POSITION solo per l'argomento *Operation* in **SQLSetPos**. Supporta il valore SQL_LOCK_NO_CHANGE solo per il *LockType* argomento.  
  
 Se il driver non supporta le operazioni bulk, la libreria di cursori restituisce SQLSTATE HYC00 (Driver non in grado) quando **SQLSetPos** viene chiamato con *RowNumber* uguale a 0. Questo comportamento del driver non è consigliato.  
  
 La libreria di cursori non supporta le operazioni SQL_UPDATE e SQL_DELETE in una chiamata a **SQLSetPos**. La libreria di cursori implementa un'istruzione SQL di aggiornamento o eliminazione posizionata creando un'istruzione di aggiornamento o eliminazione ricercata con una clausola WHERE che enumera i valori archiviati nella cache per ogni colonna associata. Per ulteriori informazioni, vedere [Elaborazione di istruzioni di aggiornamento ed eliminazione con posizione](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se il driver non supporta i cursori statici, un'applicazione che utilizza la libreria di cursori deve chiamare **SQLSetPos** solo su un set di righe recuperato da **SQLExtendedFetch** o **SQLFetchScroll**, non da **SQLFetch**. La libreria di cursori implementa **SQLExtendedFetch** e **SQLFetchScroll** effettuando chiamate ripetute di **SQLFetch** (con una dimensione del set di righe pari a 1) nel driver. La libreria di cursori passa le chiamate a **SQLFetch**, d'altra parte, al driver. Se **SQLSetPos** viene chiamato su un set di righe multiriga recuperato da **SQLFetch** quando il driver non supporta i cursori statici, la chiamata avrà esito negativo perché **SQLSetPos** non funziona con i cursori forward-only. Ciò si verifica anche se un'applicazione ha chiamato correttamente **SQLSetStmtAttr** per impostare SQL_ATTR_CURSOR_TYPE su SQL_CURSOR_STATIC, che la libreria di cursori supporta anche se il driver non supporta i cursori statici.
