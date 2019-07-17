---
title: Matrici di parametri di associazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597142d41ed8d3cff26891dfdcc89398543dab43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103826"
---
# <a name="binding-arrays-of-parameters"></a>Associazione delle matrici di parametri
Le applicazioni che utilizzano le matrici di parametri di associare le matrici ai parametri nell'istruzione SQL. Esistono due stili di binding:  
  
-   Associare una matrice a ogni parametro. Ogni struttura di data (array) contiene tutti i dati per un singolo parametro. Questa operazione viene definita *associazione per colonna* perché è collegata a una colonna di valori per un singolo parametro.  
  
-   Definire una struttura per contenere i dati di parametro per un intero set di parametri e associare una matrice di queste strutture. Ogni struttura di dati contiene i dati per una singola istruzione SQL. Questa operazione viene definita *l'associazione per riga* perché è collegata una riga di parametri.  
  
 Quando l'applicazione associa le variabili unica ai parametri, che chiama **SQLBindParameter** per associare le matrici ai parametri. L'unica differenza è che gli indirizzi inoltrati sono indirizzi matrice, non solo-variable. L'applicazione imposta l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE per specificare se si tratta di uso per colonna (predefinito) o l'associazione per riga. Se si desidera utilizzare l'associazione per colonna o per riga è in gran parte di una questione di preferenza dell'applicazione. A seconda del modo in cui il processore accede alla memoria, l'associazione per riga potrebbe essere più veloce. Tuttavia, la differenza è probabile che essere ignorabile eccetto un numero molto elevato di righe di parametri.  
  
## <a name="column-wise-binding"></a>Associazione per colonna  
 Quando si usa l'associazione per colonna, un'applicazione si associa una o due matrici a ogni parametro per il quale sono necessario fornire i dati. La prima matrice contiene i valori dei dati e la seconda matrice contiene i buffer di lunghezza/indicatore. Ogni matrice contiene tutti gli elementi perché sono presenti valori per il parametro.  
  
 L'associazione è il valore predefinito. L'applicazione anche possibile modificare dall'associazione per riga per associazione per colonna impostando l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE. La figura seguente mostra funzionamento dell'associazione per colonna.  
  
 ![Viene illustrato come colonna&#45;consigliabile binding funziona](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Ad esempio, il codice seguente associa le matrici di 10 elementi ai parametri per le colonne PartID, descrizione e il prezzo e viene eseguita un'istruzione per l'inserimento di 10 righe. Usa l'associazione per colonna.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>Associazione per riga  
 Quando si usa l'associazione per riga, un'applicazione definisce una struttura per ogni set di parametri. La struttura contiene uno o due elementi per ogni parametro. Il primo elemento contiene il valore del parametro e il secondo elemento contiene il buffer di lunghezza/indicatore. Quindi, l'applicazione consente di allocare una matrice delle strutture, che contiene tutti gli elementi perché sono presenti valori per ogni parametro.  
  
 L'applicazione dichiara le dimensioni della struttura per il driver con l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE. L'applicazione associa gli indirizzi dei parametri nella struttura prima della matrice. Di conseguenza, il driver può calcolare l'indirizzo dei dati per una particolare riga e colonna come  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 in cui le righe sono numerate da 1 alla dimensione del set di parametri. L'offset, se definito, è il valore a cui punta l'attributo di istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR. La figura seguente mostra funzionamento dell'associazione per riga. I parametri possono essere inseriti nella struttura in qualsiasi ordine, ma vengono visualizzati in ordine sequenziale per maggiore chiarezza.  
  
 ![Mostra riga&#45;consigliabile binding funziona](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 Il codice seguente crea una struttura con elementi per i valori da archiviare nelle colonne PartID, la descrizione e prezzo. Quindi alloca una matrice di 10 elementi di tali strutture e lo associa ai parametri per le colonne PartID, descrizione e il prezzo, utilizzando l'associazione per riga. Viene quindi eseguita un'istruzione per l'inserimento di 10 righe.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
