---
title: Allocazione e liberazione di buffer | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388147de8935d36180ba9845c8353bbf3dd6edc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288079"
---
# <a name="allocating-and-freeing-buffers"></a>Allocazione e rilascio di buffer
Tutti i buffer vengano allocati e liberati dall'applicazione. Se un buffer non viene rinviato, devono esistere solo per la durata della chiamata a una funzione. Ad esempio, **SQLGetInfo** restituisce il valore associato a una particolare opzione nel buffer a cui punta il *InfoValuePtr* argomento. Questo buffer può essere liberato immediatamente dopo la chiamata a **SQLGetInfo**, come illustrato nell'esempio di codice seguente:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 Poiché buffer posticipati sono specificati in una funzione e usato in un altro, è un errore di programmazione dell'applicazione per liberare un buffer posticipato mentre il driver si prevede comunque che esista. Ad esempio, l'indirizzo del \* *ValuePtr* buffer viene passato al **SQLBindCol** per un utilizzo successivo da **SQLFetch**. Questo buffer non può essere liberato fino a quando non la colonna non è associata, ad esempio con una chiamata a **SQLBindCol** oppure **SQLFreeStmt** come illustrato nell'esempio di codice seguente:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 Questo errore sarà facilmente dichiarando il buffer in locale in una funzione; il buffer viene liberato quando l'applicazione lascia la funzione. Ad esempio, il codice seguente fa sì che il comportamento non definito e probabilmente irreversibile nel driver:  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
