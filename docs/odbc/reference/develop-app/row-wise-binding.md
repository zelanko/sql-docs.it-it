---
description: Associazione per riga
title: Associazione per riga | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b30d2426a8fb2a2bd0f0cb89c2de5bc326b67dfa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465621"
---
# <a name="row-wise-binding"></a>Associazione per riga
Quando si utilizza l'associazione per riga, un'applicazione definisce una struttura contenente uno o due elementi, oppure, in alcuni casi, tre elementi per ogni colonna per cui devono essere restituiti i dati. Il primo elemento include il valore dei dati e il secondo elemento include il buffer di lunghezza/indicatore. Gli indicatori e i valori di lunghezza possono essere archiviati in buffer distinti impostando i campi SQL_DESC_INDICATOR_PTR e descrittore SQL_DESC_OCTET_LENGTH_PTR su valori diversi. Se questa operazione viene eseguita, la struttura contiene un terzo elemento. L'applicazione quindi alloca una matrice di queste strutture, che contiene il numero di elementi presenti nel set di righe.  
  
 L'applicazione dichiara la dimensione della struttura al driver con l'attributo SQL_ATTR_ROW_BIND_TYPE Statement e associa l'indirizzo di ogni membro nel primo elemento della matrice. Pertanto, il driver può calcolare l'indirizzo dei dati per una riga e una colonna particolari come  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 dove le righe sono numerate da 1 alla dimensione del set di righe. Ne viene sottratto uno dal numero di riga perché l'indicizzazione della matrice in C è in base zero. Nella figura seguente viene illustrato il funzionamento dell'associazione per riga. In genere, solo le colonne che verranno associate vengono incluse nella struttura. La struttura può contenere campi che non sono correlati alle colonne del set di risultati. Le colonne possono essere inserite nella struttura in qualsiasi ordine, ma sono visualizzate in ordine sequenziale per maggiore chiarezza.  
  
 ![Mostra l'associazione saggia&#45;di riga](../../../odbc/reference/develop-app/media/pr22.gif "PR22")  
  
 Il codice seguente, ad esempio, crea una struttura con gli elementi in cui restituire i dati per le colonne OrderID, SalesPerson e status, nonché la lunghezza/gli indicatori per le colonne SalesPerson e status. Alloca 10 di queste strutture e le associa alle colonne OrderID, SalesPerson e status.  
  
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
