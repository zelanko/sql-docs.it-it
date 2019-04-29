---
title: Come funziona il Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 685f67c9f24593a5c50097de426b76fef068d6e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735019"
---
# <a name="what-the-driver-does"></a>Funzionamento del driver
La tabella seguente riepiloga le funzioni e gli attributi delle istruzioni un'applicazione ODBC 3*x* driver devono implementare per blocchi e i cursori scorrevoli.  
  
|Funzione o<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Imposta l'indirizzo della matrice di stato di riga vengono immesse **SQLFetch** e **SQLFetchScroll**. Questa matrice viene inoltre compilata **SQLSetPos** se **SQLSetPos** viene chiamato nello stato istruzione S6. Se **SQLSetPos** viene chiamato nello stato S7, questa matrice non è compilata, ma la matrice a cui punta il *RowStatusArray* argomento del **SQLExtendedFetch** viene riempita. Per altre informazioni, vedere [transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md) nell'appendice b: Tabelle della transizione di stato ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Imposta l'indirizzo del buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate. Se **SQLExtendedFetch** viene chiamato, questo buffer non è compilato, ma il *RowCountPtr* argomento fa riferimento al numero di righe recuperate.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta le dimensioni del set di righe utilizzata da **SQLFetch** e **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Imposta le dimensioni del set di righe utilizzata da **SQLExtendedFetch**. ODBC 3 *. x* i driver di implementano questo se vogliono lavorare con l'API ODBC 2. *x* applicazioni che chiamano **SQLExtendedFetch** oppure **SQLSetPos**.|  
|**SQLBulkOperations**|Se un'applicazione ODBC 3 *. x* driver dovrebbero funzionare con l'API ODBC 2. *x* applicazioni che usano **SQLSetPos** con un *operazione* di SQL_ADD, deve supportare il driver **SQLSetPos** con un  *Operazione* di SQL_ADD oltre a **SQLBulkOperations** con un *operazione* di SQL_ADD.|  
|**SQLExtendedFetch**|Restituisce il set di righe specificato. ODBC 3 *. x* i driver di implementano questo se vogliono lavorare con l'API ODBC 2. *x* applicazioni che chiamano **SQLExtendedFetch** oppure **SQLSetPos**. Di seguito sono i dettagli di implementazione:<br /><br /> -Il driver recupera la dimensione del set di righe rispetto a quello dell'attributo di istruzione SQL_ROWSET_SIZE.<br />-Il driver recupera l'indirizzo della matrice di stato di riga dal *RowStatusArray* argomento, non l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR. Il *RowStatusArray* argomento nella chiamata a **SQLExtendedFetch** non deve essere un puntatore null. (Si noti che in ODBC 3*x*, l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR può essere un puntatore null.)<br />-Il driver recupera l'indirizzo del buffer di recupero di righe dal *RowCountPtr* argomento, non l'attributo SQL_ATTR_ROWS_FETCHED_PTR dell'istruzione.<br />-Il driver restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore mentre le righe sono state recuperate da una chiamata a **SQLExtendedFetch**. Un'applicazione ODBC 3 *. x* driver deve restituire SQLSTATE 01S01 (errore nella riga) solo quando **SQLExtendedFetch** viene chiamato, non quando **SQLFetch** o **SQLFetchScroll** viene chiamato. Per mantenere la compatibilità con le versioni precedenti, quando SQLSTATE 01S01 (errore nella riga) viene restituito dagli **SQLExtendedFetch**, gestione Driver non ordina i record di stato nella coda degli errori in base alle regole affermato di "sequenza di stato Sezione dei record di "del [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Restituisce il successivo set di righe. Di seguito sono i dettagli di implementazione:<br /><br /> -Il driver recupera la dimensione del set di righe rispetto a quello dell'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.<br />-Il driver recupera l'indirizzo della matrice di stato di riga dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.<br />-Il driver recupera l'indirizzo delle righe recuperate buffer dall'attributo SQL_ATTR_ROWS_FETCHED_PTR istruzione.<br />-L'applicazione può combinare le chiamate tra **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** restituisce segnalibri se colonna 0 è associato.<br />-   **SQLFetch** può essere chiamata per restituire più righe.<br />-Il driver non restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore mentre le righe sono state recuperate da una chiamata a **SQLFetch**.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono i dettagli di implementazione:<br /><br /> -Il driver recupera la dimensione del set di righe dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.<br />-Il driver recupera l'indirizzo della matrice di stato di riga dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.<br />-Il driver recupera l'indirizzo delle righe recuperate buffer dall'attributo SQL_ATTR_ROWS_FETCHED_PTR istruzione.<br />-L'applicazione può combinare le chiamate tra **SQLFetchScroll** e **SQLFetch**.<br />-Il driver non restituisce SQLSTATE 01S01 (errore nella riga) per indicare che si è verificato un errore mentre le righe sono state recuperate da una chiamata a **SQLFetchScroll**.|  
|**SQLSetPos**|Consente di eseguire varie operazioni posizionate. Di seguito sono i dettagli di implementazione:<br /><br /> -Può essere richiamata in S6 o S7 gli stati di istruzione. Per altre informazioni, vedere [transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md) nell'appendice b: Tabelle della transizione di stato ODBC.<br />-Se questo viene chiamato nello stato istruzione S5 o S6, il driver recupera la dimensione del set di righe dall'attributo SQL_ATTR_ROWS_FETCHED_PTR istruzione e l'indirizzo della matrice di stato di riga dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.<br />-Se questo viene chiamato nello stato istruzione S7, il driver recupera la dimensione del set di righe dall'attributo di istruzione SQL_ROWSET_SIZE e l'indirizzo della matrice di stato di riga dal *RowStatusArray* argomento di  **SQLExtendedFetch**.<br />-Il driver restituisce SQLSTATE 01S01 (errore nella riga) solo per indicare che si è verificato un errore mentre le righe sono state recuperate da una chiamata a **SQLSetPos** per eseguire un'operazione bulk quando la funzione viene chiamata in stato S7. Per mantenere la compatibilità con le versioni precedenti, se SQLSTATE 01S01 (errore nella riga) viene restituito dagli **SQLSetPos**, gestione Driver non ordina i record di stato nella coda degli errori in base alle regole riportate "Sequenza di record di stato" sezione di [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Se il driver dovrebbe funzionare con l'API ODBC 2. *x* le applicazioni che chiamano **SQLSetPos** con un *operazione* argomento di SQL_ADD, il driver deve supportare **SQLSetPos** con un  *Operazione* argomento di SQL_ADD.|
