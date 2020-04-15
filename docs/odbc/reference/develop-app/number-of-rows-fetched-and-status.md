---
title: Numero di righe recuperate e stato Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302362"
---
# <a name="number-of-rows-fetched-and-status"></a>Numero di righe recuperate e stato
Se l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR è stato impostato, specifica un buffer che restituisce il numero di righe recuperate dalla chiamata a **SQLFetch** o **SQLFetchScroll**e alle righe di errore. Questo numero è un conteggio di tutte le righe che non hanno lo stato SQL_ROW_NO_ROWS. Dopo una chiamata a **SQLBulkOperations** o **SQLSetPos**, il buffer contiene il numero di righe interessate da un'operazione in blocco eseguita dalla funzione. Se è stato impostato l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** o **SQLFetchScroll** restituisce la matrice di stato della *riga,* che fornisce lo stato di ogni riga restituita. Entrambi i buffer a cui puntano questi campi vengono allocati dall'applicazione e popolati dal driver. Un'applicazione deve assicurarsi che questi puntatori rimangano validi fino alla chiusura del cursore.  
  
 Le voci nella matrice di stato della riga indicano se ogni riga è stata recuperata correttamente, se è stata aggiornata, aggiunta o eliminata dall'ultimo recupero e se si è verificato un errore durante il recupero della riga. Se **SQLFetch** o **SQLFetchScroll** rileva un errore durante il recupero di una riga di un set di righe multiriga o se **SQLBulkOperations** con *un* operation argomento di SQL_FETCH_BY_BOOKMARK rileva un errore durante l'esecuzione di un recupero bulk, imposta il valore corrispondente nella matrice di stato della riga per SQL_ROW_ERROR, continua il recupero di righe e restituisce SQL_SUCCESS_WITH_INFO. Per altre informazioni sulla gestione degli errori e sulla matrice di stato delle righe, vedere le descrizioni delle funzioni SQLFetch e [SQLFetchScroll.For](../../../odbc/reference/syntax/sqlfetchscroll-function.md) more information about error handling and the row status array, see the [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) and SQLFetchScroll function descriptions.
