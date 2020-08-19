---
description: Uso di SQLBindCol
title: Uso di SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f68aa647f600709dd1a4b989cdab8153775f0aaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421445"
---
# <a name="using-sqlbindcol"></a>Uso di SQLBindCol
L'applicazione associa le colonne chiamando **SQLBindCol**. Questa funzione associa una colonna alla volta. Con esso, l'applicazione specifica quanto segue:  
  
-   Numero di colonna. La colonna 0 è la colonna del segnalibro; Questa colonna non è inclusa in alcuni set di risultati. Tutte le altre colonne sono numerate a partire dal numero 1. Si è verificato un errore durante l'associazione di una colonna con un numero maggiore di colonne nel set di risultati. Questo errore non può essere rilevato fino a quando non viene creato il set di risultati, pertanto viene restituito da **SQLFetch**, non da **SQLBindCol**.  
  
-   Il tipo di dati C, l'indirizzo e la lunghezza in byte della variabile associata alla colonna. Non è possibile specificare un tipo di dati C a cui non è possibile convertire il tipo di dati SQL della colonna. Questo errore potrebbe non essere rilevato fino a quando non viene creato il set di risultati, pertanto viene restituito da **SQLFetch**, non da **SQLBindCol**. Per un elenco delle conversioni supportate, vedere [conversione di dati da SQL ai tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in Appendice D: tipi di dati. Per informazioni sulla lunghezza in byte, vedere [lunghezza del buffer dei dati](../../../odbc/reference/develop-app/data-buffer-length.md).  
  
-   Indirizzo di un buffer di lunghezza/indicatore. Il buffer di lunghezza/indicatore è facoltativo. Viene utilizzato per restituire la lunghezza in byte dei dati di tipo binary o character oppure restituire SQL_NULL_DATA se i dati sono NULL. Per ulteriori informazioni, vedere [utilizzo di valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Quando viene chiamato **SQLBindCol** , il driver associa queste informazioni all'istruzione. Quando viene recuperata ogni riga di dati, vengono utilizzate le informazioni per inserire i dati per ogni colonna nelle variabili dell'applicazione associata.  
  
 Il codice seguente, ad esempio, associa le variabili alle colonne SalesPerson e CustID. I dati per le colonne verranno restituiti in *venditori* e *CustID*. Poiché il *venditore* è un buffer di caratteri, l'applicazione ne specifica la lunghezza in byte (11), in modo che il driver possa determinare se troncare i dati. La lunghezza in byte del titolo restituito, o se è NULL, verrà restituita in *SalesPersonLenOrInd*.  
  
 Poiché *CustID* è una variabile di tipo integer con lunghezza fissa, non è necessario specificarne la lunghezza in byte; il driver presuppone che sia **sizeof (** SQLUINTEGER **)**. La lunghezza in byte dei dati ID cliente restituiti, o se è NULL, verrà restituita in *CustIDInd*. Si noti che l'applicazione è interessata solo se lo stipendio è NULL, perché la lunghezza in byte è sempre **sizeof (** SQLUINTEGER **)**.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLUINTEGER   CustID;  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLRETURN     rc;  
SQLHSTMT      hstmt;  
  
// Bind SalesPerson to the SalesPerson column and CustID to the   
// CustID column.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),  
            &SalesPersonLenOrInd);  
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);  
  
// Execute a statement to get the sales person/customer of all orders.  
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",  
               SQL_NTS);  
  
// Fetch and print the data. Print "NULL" if the data is NULL. Code to   
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (SalesPersonLenOrInd == SQL_NULL_DATA)   
            printf("NULL                     ");  
   else   
            printf("%10s   ", SalesPerson);  
   if (CustIDInd == SQL_NULL_DATA)   
         printf("NULL\n");  
   else   
            printf("%d\n", CustID);  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 Il codice seguente esegue un'istruzione **Select** immessa dall'utente e stampa ogni riga di dati nel set di risultati. Poiché l'applicazione non è in grado di stimare la forma del set di risultati creato dall'istruzione **Select** , non è in grado di associare variabili hardcoded al set di risultati come nell'esempio precedente. Al contrario, l'applicazione alloca un buffer che include i dati e un buffer di lunghezza/indicatore per ogni colonna della riga. Per ogni colonna, viene calcolato l'offset all'inizio della memoria per la colonna e tale offset viene regolato in modo che i buffer di dati e di lunghezza/indicatore per la colonna inizino sui limiti di allineamento. Associa quindi la memoria a partire dall'offset alla colonna. Dal punto di vista del driver, l'indirizzo di questa memoria non è distinguibile dall'indirizzo di una variabile associata nell'esempio precedente. Per ulteriori informazioni sull'allineamento, vedere [allineamento](../../../odbc/reference/develop-app/alignment.md).  
  
```  
// This application allocates a buffer at run time. For each column, this   
// buffer contains memory for the column's data and length/indicator.   
// For example:  
//      column 1         column 2      column 3      column 4  
// <------------><---------------><-----><------------>  
//      db1   li1   db2   li2   db3   li3   db4   li4  
//      |      |      |      |      |      |      |         |  
//      _____V_____V________V_______V___V___V______V_____V_  
// |__________|__|_____________|__|___|__|__________|__|  
//  
// dbn = data buffer for column n  
// lin = length/indicator buffer for column n  
  
// Define a macro to increase the size of a buffer so that it is a   
// multiple of the alignment size. Thus, if a buffer starts on an   
// alignment boundary, it will end just before the next alignment   
// boundary. In this example, an alignment size of 4 is used because   
// this is the size of the largest data type used in the application's   
// buffer--the size of an SDWORD and of the largest default C data type   
// are both 4. If a larger data type (such as _int64) was used, it would   
// be necessary to align for that size.  
#define ALIGNSIZE 4  
#define ALIGNBUF(Length) Length % ALIGNSIZE ? \  
                  Length + ALIGNSIZE - (Length % ALIGNSIZE) : Length  
  
SQLCHAR        SelectStmt[100];  
SQLSMALLINT    NumCols, *CTypeArray, i;  
SQLINTEGER *   ColLenArray, *OffsetArray, SQLType, *DataPtr;  
SQLRETURN      rc;   
SQLHSTMT       hstmt;  
  
// Get a SELECT statement from the user and execute it.  
GetSelectStmt(SelectStmt, 100);  
SQLExecDirect(hstmt, SelectStmt, SQL_NTS);  
  
// Determine the number of result set columns. Allocate arrays to hold   
// the C type, byte length, and buffer offset to the data.  
SQLNumResultCols(hstmt, &NumCols);  
CTypeArray = (SQLSMALLINT *) malloc(NumCols * sizeof(SQLSMALLINT));  
ColLenArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
OffsetArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
  
OffsetArray[0] = 0;  
for (i = 0; i < NumCols; i++) {  
   // Determine the column's SQL type. GetDefaultCType contains a switch   
   // statement that returns the default C type for each SQL type.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i) + 1, SQL_DESC_TYPE, NULL, 0, NULL, (SQLPOINTER) &SQLType);  
   CTypeArray[i] = GetDefaultCType(SQLType);  
  
   // Determine the column's byte length. Calculate the offset in the   
   // buffer to the data as the offset to the previous column, plus the   
   // byte length of the previous column, plus the byte length of the   
   // previous column's length/indicator buffer. Note that the byte   
   // length of the column and the length/indicator buffer are increased   
   // so that, assuming they start on an alignment boundary, they will  
   // end on the byte before the next alignment boundary. Although this   
   // might leave some holes in the buffer, it is a relatively   
   // inexpensive way to guarantee alignment.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i)+1, SQL_DESC_OCTET_LENGTH, NULL, 0, NULL, &ColLenArray[i]);  
   ColLenArray[i] = ALIGNBUF(ColLenArray[i]);  
   if (i)  
      OffsetArray[i] = OffsetArray[i-1]+ColLenArray[i-1]+ALIGNBUF(sizeof(SQLINTEGER));  
}  
  
// Allocate the data buffer. The size of the buffer is equal to the   
// offset to the data buffer for the final column, plus the byte length   
// of the data buffer and length/indicator buffer for the last column.  
void *DataPtr = malloc(OffsetArray[NumCols - 1] +  
               ColLenArray[NumCols - 1] + ALIGNBUF(sizeof(SQLINTEGER)));  
  
// For each column, bind the address in the buffer at the start of the   
// memory allocated for that column's data and the address at the start   
// of the memory allocated for that column's length/indicator buffer.  
for (i = 0; i < NumCols; i++)  
   SQLBindCol(hstmt,  
            ((SQLUSMALLINT) i) + 1,  
            CTypeArray[i],  
            (SQLPOINTER)((SQLCHAR *)DataPtr + OffsetArray[i]),  
            ColLenArray[i],  
            (SQLINTEGER *)((SQLCHAR *)DataPtr + OffsetArray[i] + ColLenArray[i]));  
  
// Retrieve and print each row. PrintData accepts a pointer to the data,   
// its C type, and its byte length/indicator. It contains a switch   
// statement that casts and prints the data according to its type. Code   
// to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   for (i = 0; i < NumCols; i++) {  
      PrintData((SQLCHAR *)DataPtr[OffsetArray[i]], CTypeArray[i],  
               (SQLINTEGER *)((SQLCHAR *)DataPtr[OffsetArray[i] + ColLenArray[i]]));  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
