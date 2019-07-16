---
title: L'associazione per riga | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aab33f8805741083fd42e9fbcb25d67a416be319
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061626"
---
# <a name="row-wise-binding"></a>Associazione per riga
Quando si usa l'associazione per riga, un'applicazione definisce una struttura che contiene uno o due, o in alcuni casi, tre, gli elementi per ogni colonna per cui sono necessario restituire i dati. Il primo elemento contiene il valore dei dati e il secondo elemento contiene il buffer di lunghezza/indicatore. I valori di lunghezza e gli indicatori possono essere archiviati nei buffer separato impostando i campi di descrizione SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR su valori diversi; Se questa operazione viene eseguita, la struttura contiene un terzo elemento. Quindi, l'applicazione consente di allocare una matrice delle strutture, che contiene tutti gli elementi poiché sono presenti righe nel set di righe.  
  
 L'applicazione dichiara le dimensioni della struttura per il driver con l'attributo di istruzione SQL_ATTR_ROW_BIND_TYPE e associa l'indirizzo di ogni membro nel primo elemento della matrice. Di conseguenza, il driver può calcolare l'indirizzo dei dati per una particolare riga e colonna come  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 in cui le righe sono numerate da 1 per le dimensioni del set di righe. (Uno viene sottratto dal numero di riga perché è in base zero in matrice di indicizzazione in C.) La figura seguente mostra funzionamento dell'associazione per riga. In genere, solo le colonne che verranno associate sono inclusi nella struttura. La struttura può contenere i campi non correlati per le colonne del set di risultati. Le colonne possono essere inserite nella struttura in qualsiasi ordine, ma vengono visualizzate in ordine sequenziale per maggiore chiarezza.  
  
 ![Mostra riga&#45;associazione saggia](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 Ad esempio, il codice seguente crea una struttura con elementi in cui si desidera ottenere dati per le colonne OrderID, venditore e lo stato e lunghezza/indicatori per le colonne di venditore e lo stato. Alloca 10 delle strutture e li associa le colonne OrderID, venditore e stato.  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
