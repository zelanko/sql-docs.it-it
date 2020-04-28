---
title: Associazioni di matrici di parametri | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73cfcde89e89edb87a4955cf0854c66a01d81e6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283421"
---
# <a name="binding-arrays-of-parameters"></a>Associazione delle matrici di parametri
Le applicazioni che utilizzano matrici di parametri associano le matrici ai parametri nell'istruzione SQL. Sono disponibili due stili di associazione:  
  
-   Associare una matrice a ogni parametro. Ogni struttura di dati (matrice) contiene tutti i dati per un singolo parametro. Questa operazione viene definita *associazione per colonna* perché associa una colonna di valori per un singolo parametro.  
  
-   Definire una struttura per conservare i dati del parametro per un intero set di parametri e associare una matrice di queste strutture. Ogni struttura di dati contiene i dati per una singola istruzione SQL. Questa operazione viene definita *associazione per riga* perché associa una riga di parametri.  
  
 Quando l'applicazione associa variabili singole a parametri, chiama **SQLBindParameter** per associare le matrici ai parametri. L'unica differenza consiste nel fatto che gli indirizzi passati sono indirizzi di matrice, non indirizzi a singola variabile. L'applicazione imposta l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_TYPE per specificare se utilizza l'associazione per colonna (impostazione predefinita) o per riga. La possibilità di utilizzare l'associazione per colonna o per riga è in gran parte una questione di preferenza dell'applicazione. A seconda del modo in cui il processore accede alla memoria, l'associazione a livello di riga potrebbe essere più veloce. Tuttavia, la differenza è probabilmente irrilevante ad eccezione di un numero molto elevato di righe di parametri.  
  
## <a name="column-wise-binding"></a>Associazione per colonna  
 Quando si utilizza l'associazione per colonna, un'applicazione associa una o due matrici a ogni parametro per il quale devono essere forniti i dati. La prima matrice include i valori dei dati e la seconda matrice include i buffer di lunghezza/indicatore. Ogni matrice contiene tutti gli elementi quanti sono i valori per il parametro.  
  
 L'associazione per colonna è il valore predefinito. L'applicazione può anche passare da un'associazione per riga a un'associazione a livello di colonna impostando l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_TYPE. Nella figura seguente viene illustrato il funzionamento dell'associazione per colonna.  
  
 ![Illustra il funzionamento dell'associazione&#45;per la colonna](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Il codice seguente, ad esempio, associa le matrici di 10 elementi a parametri per le colonne PartId, Description e Price ed esegue un'istruzione per inserire 10 righe. Usa l'associazione per colonna.  
  
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
 Quando si utilizza l'associazione per riga, un'applicazione definisce una struttura per ogni set di parametri. La struttura contiene uno o due elementi per ogni parametro. Il primo elemento include il valore del parametro e il secondo elemento include il buffer di lunghezza/indicatore. L'applicazione quindi alloca una matrice di queste strutture, che contiene tutti gli elementi quanti sono i valori per ogni parametro.  
  
 L'applicazione dichiara la dimensione della struttura al driver con l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_TYPE. L'applicazione associa gli indirizzi dei parametri nella prima struttura della matrice. Pertanto, il driver può calcolare l'indirizzo dei dati per una riga e una colonna particolari come  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 dove le righe sono numerate da 1 alla dimensione del set di parametri. L'offset, se definito, è il valore a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR. Nella figura seguente viene illustrato il funzionamento dell'associazione per riga. I parametri possono essere posizionati nella struttura in qualsiasi ordine, ma sono visualizzati in ordine sequenziale per maggiore chiarezza.  
  
 ![Illustra il funzionamento dell'associazione di riga&#45;Wise](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 Il codice seguente crea una struttura con elementi per i valori da archiviare nelle colonne PartId, Description e price. Viene quindi allocata una matrice di 10 elementi di queste strutture e viene associata a parametri per le colonne PartId, Description e Price, utilizzando l'associazione per riga. Viene quindi eseguita un'istruzione per inserire 10 righe.  
  
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
