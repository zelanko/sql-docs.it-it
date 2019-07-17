---
title: Numero di righe recuperate e stato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc1f556873221faa3f86c5272120a786f6f25025
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086328"
---
# <a name="number-of-rows-fetched-and-status"></a>Numero di righe recuperate e stato
Se è stato impostato l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR, specifica un buffer che restituisce il numero di righe recuperate dalla chiamata a **SQLFetch** oppure **SQLFetchScroll**e le righe di errore. (Questo numero è un conteggio di tutte le righe che non è stato SQL_ROW_NO_ROWS). Dopo una chiamata a **SQLBulkOperations** oppure **SQLSetPos**, il buffer contiene il numero di righe interessate da un'operazione bulk eseguita dalla funzione. Se è stato impostato l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** oppure **SQLFetchScroll** restituisce il *matrice di stato di riga,* che fornisce lo stato di ogni riga restituita. Entrambi i buffer a cui fa riferimento a questi campi vengono allocati dall'applicazione e popolati dal driver. Un'applicazione deve assicurarsi che questi puntatori rimangono validi fino a quando il cursore è chiuso.  
  
 Voci nello stato di matrice di stato di riga se ogni riga è stata recuperata correttamente, se è stato aggiornato, aggiunto o eliminato dopo l'ultimo recupero e se si è verificato un errore durante il recupero della riga. Se **SQLFetch** oppure **SQLFetchScroll** rileva un errore durante il recupero di una riga di un set di righe a riga multipla, oppure se **SQLBulkOperations** con un *operazione*  argomento di SQL_FETCH_BY_BOOKMARK rileva un errore durante l'esecuzione di un'operazione di recupero di massa, imposta il valore corrispondente nella matrice di stato di riga per SQL_ROW_ERROR, continua il recupero di righe e viene restituito SQL_SUCCESS_WITH_INFO. Per altre informazioni sulla gestione degli errori e la matrice di stato di riga, vedere la [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) e [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) funzione descrizioni.
