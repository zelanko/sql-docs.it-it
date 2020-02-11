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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086328"
---
# <a name="number-of-rows-fetched-and-status"></a>Numero di righe recuperate e stato
Se è stato impostato l'attributo SQL_ATTR_ROWS_FETCHED_PTR Statement, viene specificato un buffer che restituisce il numero di righe recuperate dalla chiamata a **SQLFetch** o **SQLFetchScroll**e le righe di errore. (Questo numero è un conteggio di tutte le righe che non hanno lo stato SQL_ROW_NO_ROWS.) Dopo una chiamata a **SQLBulkOperations** o **SQLSetPos**, il buffer contiene il numero di righe interessate da un'operazione bulk eseguita dalla funzione. Se è stato impostato l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR, **SQLFetch** o **SQLFetchScroll** restituisce la *matrice di stato della riga,* che fornisce lo stato di ogni riga restituita. Entrambi i buffer a cui puntano questi campi vengono allocati dall'applicazione e popolati dal driver. Un'applicazione deve assicurarsi che questi puntatori rimangano validi fino alla chiusura del cursore.  
  
 Le voci nella matrice di stato della riga determinano se ogni riga è stata recuperata correttamente, se è stata aggiornata, aggiunta o eliminata dall'ultimo recupero e se si è verificato un errore durante il recupero della riga. Se **SQLFetch** o **SQLFetchScroll** rileva un errore durante il recupero di una riga di un set di righe più righe o se **SQLBulkOperations** con un argomento *Operation* di SQL_FETCH_BY_BOOKMARK rileva un errore durante l'esecuzione di un recupero bulk, imposta il valore corrispondente nella matrice di stato della riga su SQL_ROW_ERROR, continua il recupero delle righe e restituisce SQL_SUCCESS_WITH_INFO. Per ulteriori informazioni sulla gestione degli errori e sulla matrice di stato della riga, vedere le descrizioni della funzione [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) e [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .
