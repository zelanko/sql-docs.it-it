---
description: Aggiornamento delle righe nel set di righe con SQLSetPos
title: Aggiornamento di righe nel set di righe con SQLSetPos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1b1b50007a03ee1973d92acafbe8f2be1022f52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471216"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>Aggiornamento delle righe nel set di righe con SQLSetPos
L'operazione di aggiornamento di **SQLSetPos** consente all'origine dati di aggiornare una o più righe selezionate di una tabella, usando i dati nei buffer dell'applicazione per ogni colonna associata, a meno che il valore nel buffer di lunghezza/indicatore non sia SQL_COLUMN_IGNORE. Le colonne non associate non verranno aggiornate.  
  
 Per aggiornare le righe con **SQLSetPos**, l'applicazione esegue le operazioni seguenti:  
  
1.  Inserisce i nuovi valori dei dati nei buffer del set di righe. Per informazioni su come inviare dati Long con **SQLSetPos**, vedere [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna, se necessario. Si tratta della lunghezza in byte dei dati o SQL_NTS per le colonne associato ai buffer di stringa, la lunghezza in byte dei dati per le colonne associato ai buffer binari e SQL_NULL_DATA per le colonne da impostare su NULL.  
  
3.  Imposta il valore nel buffer di lunghezza/indicatore delle colonne che non devono essere aggiornate per SQL_COLUMN_IGNORE. Sebbene l'applicazione possa ignorare questo passaggio e inviare nuovamente i dati esistenti, questo è inefficiente e rischia di inviare valori all'origine dati troncati durante la lettura.  
  
4.  Chiama **SQLSetPos** con *Operation* impostato su SQL_UPDATE e *RowNumber* impostato sul numero della riga da aggiornare. Se *RowNumber* è 0, vengono aggiornate tutte le righe del set di righe.  
  
 Dopo la restituzione di **SQLSetPos** , la riga corrente viene impostata sulla riga aggiornata.  
  
 Quando si aggiornano tutte le righe del set di righe (*RowNumber* è uguale a 0), un'applicazione può disabilitare l'aggiornamento di determinate righe impostando gli elementi corrispondenti della matrice dell'operazione di riga (a cui fa riferimento l'attributo SQL_ATTR_ROW_OPERATION_PTR Statement) per SQL_ROW_IGNORE. La matrice dell'operazione Row corrisponde alla dimensione e al numero di elementi nella matrice di stato della riga (a cui fa riferimento l'attributo SQL_ATTR_ROW_STATUS_PTR Statement). Per aggiornare solo le righe del set di risultati recuperate correttamente e che non sono state eliminate dal set di righe, l'applicazione utilizza la matrice di stato della riga dalla funzione che ha recuperato il set di righe come matrice dell'operazione di riga a **SQLSetPos**.  
  
 Per ogni riga inviata all'origine dati come aggiornamento, i buffer dell'applicazione devono contenere dati di riga validi. Se i buffer dell'applicazione sono stati riempiti tramite il recupero e se è stata mantenuta una matrice di stato della riga, i relativi valori in ognuna di queste posizioni delle righe non devono essere SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.  
  
 Il codice seguente, ad esempio, consente a un utente di scorrere la tabella Customers e di aggiornare, eliminare o aggiungere nuove righe. Inserisce i nuovi dati nei buffer del set di righe prima di chiamare **SQLSetPos** per aggiornare o aggiungere nuove righe. Alla fine dei buffer del set di righe viene allocata una riga aggiuntiva per memorizzare le nuove righe; in questo modo si impedisce la sovrascrittura dei dati esistenti quando si posizionano i dati di una nuova riga nei buffer.  
  
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
