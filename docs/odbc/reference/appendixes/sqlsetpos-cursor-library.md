---
title: SQLSetPos (libreria di cursori) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b41fad0f609b16640bfa28ab36f29f364e067b73
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297421"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetPos** funzione nella libreria di cursori. Per informazioni generali sul **SQLSetPos**, vedere [funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 La libreria di cursori supporta l'operazione SQL_POSITION solo per i *operazione* nell'argomento **SQLSetPos**. Supporta il valore SQL_LOCK_NO_CHANGE solo per i *LockType* argomento.  
  
 Se il driver non supporta operazioni bulk, la libreria di cursori restituisce SQLSTATE HYC00 (Driver non è in grado) quando **SQLSetPos** viene chiamato con *RowNumber* uguale a 0. Questo comportamento del driver non è consigliato.  
  
 La libreria di cursori non supporta le operazioni SQL_UPDATE e SQL_DELETE in una chiamata a **SQLSetPos**. Implementa libreria il cursore posizionato un'istruzione update o delete SQL mediante la creazione di una ricerca istruzione update o delete con una clausola WHERE che enumera i valori memorizzati nella cache per ogni colonna associata. Per altre informazioni, vedere [istruzioni di eliminazione e l'elaborazione di aggiornamento posizionato](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se il driver non supporta i cursori statici, è necessario chiamare un'applicazione che utilizza la libreria di cursori **SQLSetPos** solo in un set di righe recuperate dalle **SQLExtendedFetch** o **SQLFetchScroll** , non da **SQLFetch**. La libreria di cursori implementa **SQLExtendedFetch** e **SQLFetchScroll** eseguendo chiamate ripetute del **SQLFetch** (con una dimensione di set di righe pari a 1) nel driver. La libreria di cursori passa le chiamate a **SQLFetch**, su altro canto, tramite il driver. Se **SQLSetPos** viene chiamato su un set di righe a riga multipla recuperate dalle **SQLFetch** quando il driver non supporta i cursori statici, la chiamata avrà esito negativo perché **SQLSetPos** non funziona con cursori forward-only. Ciò si verifica anche se un'applicazione ha chiamato correttamente **SQLSetStmtAttr** impostare SQL_ATTR_CURSOR_TYPE su SQL_CURSOR_STATIC, quale la libreria di cursori supporta anche se il driver non supporta i cursori statici.
