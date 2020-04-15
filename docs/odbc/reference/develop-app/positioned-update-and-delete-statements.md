---
title: Istruzioni di aggiornamento ed eliminazione posizionate Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5316bee7057b30eace326b3ca82b30b75741fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282362"
---
# <a name="positioned-update-and-delete-statements"></a>Istruzioni di eliminazione e aggiornamento posizionato
Le applicazioni possono aggiornare o eliminare la riga corrente in un set di risultati con un'istruzione di aggiornamento o eliminazione posizionata. Le istruzioni di aggiornamento ed eliminazione posizionate sono supportate da alcune origini dati, ma non da tutte. Per determinare se un'origine dati supporta le istruzioni di aggiornamento ed eliminazione posizionate, un'applicazione chiama **SQLGetInfo** con il SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* (a seconda del tipo di cursore). Si noti che la libreria di cursori ODBC simula le istruzioni di aggiornamento ed eliminazione posizionate.  
  
 Per utilizzare un'istruzione update o delete posizionata, l'applicazione deve creare un set di risultati con un'istruzione **SELECT FOR UPDATE.** La sintassi di questa istruzione è:  
  
 **SELECT** [**ALL** &#124; **DISTINCT**] *elenco a discesa*  
  
 **FROM** *tabella-reference-list*  
  
 [**WHERE** *condizione di ricerca*]  
  
 **PER UPDATE DI** [*nome-colonna* [**,** *nome-colonna*]...]  
  
 L'applicazione posiziona quindi il cursore sulla riga da aggiornare o eliminare. È possibile eseguire questa operazione chiamando **SQLFetchScroll** per recuperare un set di righe contenente la riga richiesta e chiamando **SQLSetPos** per posizionare il cursore del set di righe su tale riga. L'applicazione esegue quindi l'istruzione di aggiornamento o eliminazione posizionata su un'istruzione diversa da quella utilizzata dal set di risultati. La sintassi di queste istruzioni è:  
  
 **UPDATE** *nome tabella*  
  
 **IDENTIFICATORe** *column-identifier* **=** di colonna SET -*espressione* &#124; **NULL**  
  
 [**,** *identificatore* **=** di colonna ,*espressione* &#124; **NULL...**  
  
 **WHERE CURRENT DI** *nome-cursore*  
  
 **DELETE FROM** *nome tabella* WHERE CURRENT **OF** *nome-cursore*  
  
 Si noti che queste istruzioni richiedono un nome di cursore. L'applicazione può specificare un nome di cursore con **SQLSetCursorName** prima di eseguire l'istruzione che crea il set di risultati oppure può consentire all'origine dati di generare automaticamente un nome di cursore quando viene creato il cursore. In quest'ultimo caso, l'applicazione recupera il nome del cursore da utilizzare nelle istruzioni di aggiornamento ed eliminazione posizionate chiamando **SQLGetCursorName**.  
  
 Ad esempio, il codice seguente consente a un utente di scorrere la tabella Customers ed eliminare i record dei clienti o aggiornare i propri indirizzi e numeri di telefono. Chiama **SQLSetCursorName** per specificare un nome di cursore prima di creare il set di risultati dei clienti e utilizza tre handle di istruzione: *hstmtCust* per il set di risultati, *hstmtUpdate* per un'istruzione di aggiornamento posizionato e *hstmDelete* per un'istruzione delete posizionata. Anche se il codice potrebbe associare variabili separate ai parametri nell'istruzione update posizionata, aggiorna i buffer del set di righe e associa gli elementi di questi buffer. In questo modo i buffer del set di righe vengono sincronizzati con i dati aggiornati.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
