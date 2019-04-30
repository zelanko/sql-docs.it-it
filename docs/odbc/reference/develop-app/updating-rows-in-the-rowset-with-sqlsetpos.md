---
title: Aggiornamento delle righe nel set di righe con SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfb57a6512245c9adb36a511ce48721dd901995c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313096"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>Aggiornamento delle righe nel set di righe con SQLSetPos
L'operazione di aggiornamento dei **SQLSetPos** consente all'origine dati di aggiornare uno o più righe selezionate di una tabella, utilizzando i dati nei buffer dell'applicazione per ogni colonna associata (a meno che il valore nel buffer di lunghezza/indicatore SQL_COLUMN_IGNORE). Le colonne che non sono associate non verranno aggiornate.  
  
 Per aggiornare le righe contenenti **SQLSetPos**, l'applicazione esegue le operazioni seguenti:  
  
1.  Inserisce i nuovi valori di dati nei buffer di set di righe. Per informazioni su come inviare dati di tipo long con **SQLSetPos**, vedere [dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna in base alle esigenze. Questa è la lunghezza in byte dei dati o SQL_NTS per le colonne associate ai buffer di stringa, la lunghezza in byte dei dati delle colonne associate a buffer binario e SQL_NULL_DATA per tutte le colonne da impostare su NULL.  
  
3.  Imposta il valore nel buffer di lunghezza/indicatore di tali colonne che non devono essere aggiornate a SQL_COLUMN_IGNORE. Anche se l'applicazione è possibile ignorare questo passaggio e inviare nuovamente i dati esistenti, questo è inefficiente e rischi in termini di invio di valori all'origine dati che sono stati troncati quando essi sono stati letti.  
  
4.  Le chiamate **SQLSetPos** con *operazione* impostato su SQL_UPDATE e *RowNumber* impostato sul numero della riga da aggiornare. Se *RowNumber* è 0, vengono aggiornate tutte le righe nel set di righe.  
  
 Dopo aver **SQLSetPos** viene restituito, la riga corrente è impostata sulla riga aggiornata.  
  
 Quando si aggiornano tutte le righe del set di righe (*RowNumber* è uguale a 0), un'applicazione può disabilitare l'aggiornamento di alcune righe, impostando gli elementi corrispondenti della matrice operazione riga (a cui punta il SQL_ATTR_ROW_OPERATION_PTR attributo di istruzione) a SQL_ROW_IGNORE. La matrice di operazione riga corrispondente nella dimensione e il numero di elementi nella matrice di stato di riga (a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR). Per aggiornare solo le righe nel set di risultati che sono stati correttamente recuperate e non sono state eliminate dal set di righe, l'applicazione usa la matrice di stato di riga dalla funzione di cui recuperata il set di righe della matrice di operazione riga per **SQLSetPos**.  
  
 Per ogni riga che viene inviata all'origine dati sotto forma di aggiornamento, i buffer dell'applicazione devono avere dei dati delle righe valido. Se sono stati compilati i buffer dell'applicazione mediante il recupero e se è stata mantenuta una matrice di stato di riga, i valori in ognuna di queste posizioni di riga non devono essere SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.  
  
 Ad esempio, il codice seguente consente all'utente di scorrere la tabella Customers e aggiornare, eliminare o aggiungere nuove righe. Inserisce i nuovi dati nei buffer di set di righe prima di chiamare **SQLSetPos** per aggiornare o aggiungere nuove righe. Una riga aggiuntiva viene allocata alla fine del buffer di set di righe per contenere nuove righe; Ciò impedisce che i dati esistenti verranno sovrascritte al momento i dati per una nuova riga viene inseriti nel buffer.  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
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
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
