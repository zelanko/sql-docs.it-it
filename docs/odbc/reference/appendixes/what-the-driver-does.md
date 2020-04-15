---
title: Scopo del driver Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301392"
---
# <a name="what-the-driver-does"></a>Funzionamento del driver
Nella tabella seguente vengono riepilogate le funzioni e gli attributi di istruzione che un driver ODBC *3.x* deve implementare per i cursori a blocchi e scorrevoli.  
  
|Funzione o<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Imposta l'indirizzo della matrice di stato della riga compilata da **SQLFetch** e **SQLFetchScroll**. Questa matrice viene riempita anche da **SQLSetPos** se **SQLSetPos** viene chiamato nello stato di istruzione S6. Se **SQLSetPos** viene chiamato nello stato S7, questa matrice non viene riempita ma la matrice a cui fa riferimento l'argomento *RowStatusArray* di **SQLExtendedFetch** viene compilata. Per ulteriori informazioni, vedere [Transizioni](../../../odbc/reference/appendixes/statement-transitions.md) di istruzioni nell'Appendice B: tabelle di transizione dello stato ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Imposta l'indirizzo del buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate. Se **SQLExtendedFetch** viene chiamato, questo buffer non viene riempito, ma il *RowCountPtr* argomento punta al numero di righe recuperate.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta la dimensione del set di righe utilizzata da **SQLFetch** e **SQLFetchScroll.**|  
|SQL_ROWSET_SIZE|Imposta la dimensione del set di righe utilizzata da **SQLExtendedFetch**. I driver ODBC *3.x* implementano questo se desiderano utilizzare le applicazioni ODBC *2.x* che chiamano **SQLExtendedFetch** o **SQLSetPos**.|  
|**Sqlbulkoperations**|Se un driver ODBC *3.x* deve funzionare con le applicazioni ODBC *2.x* che utilizzano **SQLSetPos** con *un'operazione* di SQL_ADD, il driver deve supportare **SQLSetPos** con *un'operazione* di SQL_ADD oltre a **SQLBulkOperations** con *un'operazione* di SQL_ADD.|  
|**Sqlextendedfetch**|Restituisce il set di righe specificato. I driver ODBC *3.x* implementano questo se desiderano utilizzare le applicazioni ODBC *2.x* che chiamano **SQLExtendedFetch** o **SQLSetPos**. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Il driver recupera la dimensione del set di righe dal valore dell'attributo di istruzione SQL_ROWSET_SIZE.<br />- Il driver recupera l'indirizzo della matrice di stato della riga dall'argomento *RowStatusArray,* non dall'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR. *L'argomento RowStatusArray* in una chiamata a **SQLExtendedFetch** non deve essere un puntatore null. Si noti che in ODBC *3.x*l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR può essere un puntatore null.<br />- Il driver recupera l'indirizzo delle righe recuperate buffer dal *RowCountPtr* argomento, non il SQL_ATTR_ROWS_FETCHED_PTR attributo di istruzione.<br />- Il driver restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore durante il recupero delle righe da una chiamata a **SQLExtendedFetch**. Un driver ODBC *3.x* deve restituire SQLSTATE 01S01 (errore nella riga) solo quando **sqlExtendedFetch** viene chiamato, non quando **SQLFetch** o **SQLFetchScroll** viene chiamato. Per mantenere la compatibilità con le versioni precedenti, quando SQLSTATE 01S01 (Errore nella riga) viene restituito da **SQLExtendedFetch**, Gestione Driver non ordina i record di stato nella coda degli errori in base alle regole indicate nella sezione "Sequenza di record di stato" di [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Restituisce il set di righe successivo. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Il driver recupera la dimensione del set di righe dal valore dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.<br />- Il driver recupera l'indirizzo della matrice di stato della riga dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR.<br />- Il driver recupera l'indirizzo delle righe recuperate buffer dall'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR.<br />- L'applicazione può combinare chiamate tra **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** restituisce i segnalibri se la colonna 0 è associata.<br />-   **SQLFetch** può essere chiamato per restituire più di una riga.<br />- Il driver non restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore durante il recupero delle righe da una chiamata a **SQLFetch**.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Il driver recupera la dimensione del set di righe dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.<br />- Il driver recupera l'indirizzo della matrice di stato della riga dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR.<br />- Il driver recupera l'indirizzo delle righe recuperate buffer dall'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR.<br />- L'applicazione può combinare chiamate tra **SQLFetchScroll** e **SQLFetch**.<br />- Il driver non restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore durante il recupero delle righe da una chiamata a **SQLFetchScroll**.|  
|**SQLSetPos**|Esegue varie operazioni posizionate. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Questo può essere chiamato in stati di dichiarazione S6 o S7. Per ulteriori informazioni, vedere [Transizioni](../../../odbc/reference/appendixes/statement-transitions.md) di istruzioni nell'Appendice B: tabelle di transizione dello stato ODBC.<br />- Se viene chiamato nello stato dell'istruzione S5 o S6, il driver recupera la dimensione del set di righe dall'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR e l'indirizzo della matrice di stato della riga dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR.<br />- Se viene chiamato nello stato dell'istruzione S7, il driver recupera la dimensione del set di righe dall'attributo dell'istruzione SQL_ROWSET_SIZE e l'indirizzo della matrice di stato della riga dall'argomento *RowStatusArray* di **SQLExtendedFetch**.<br />- Il driver restituisce SQLSTATE 01S01 (errore nella riga) solo per indicare che si è verificato un errore durante il recupero delle righe da una chiamata a **SQLSetPos** per eseguire un'operazione in blocco quando la funzione viene chiamata nello stato S7. Per mantenere la compatibilità con le versioni precedenti, se SQLSTATE 01S01 (Errore nella riga) viene restituito da **SQLSetPos**, Gestione Driver non ordina i record di stato nella coda degli errori in base alle regole indicate nella sezione "Sequenza di record di stato" di [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />- Se il driver deve funzionare con le applicazioni ODBC *2.x* che chiamano **SQLSetPos** con un argomento *Operation* di SQL_ADD, il driver deve supportare **SQLSetPos** con un argomento *Operation* di SQL_ADD.|
