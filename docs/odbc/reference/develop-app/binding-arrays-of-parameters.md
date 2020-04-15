---
title: Associazione di matrici di parametri . Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283421"
---
# <a name="binding-arrays-of-parameters"></a>Associazione delle matrici di parametri
Le applicazioni che utilizzano matrici di parametri associano le matrici ai parametri nell'istruzione SQL. Esistono due stili di rilegatura:There are two binding styles:  
  
-   Associare una matrice a ogni parametro. Ogni struttura di dati (matrice) contiene tutti i dati per un singolo parametro. Questa operazione è denominata *associazione per colonna* perché associa una colonna di valori per un singolo parametro.  
  
-   Definire una struttura per contenere i dati dei parametri per un intero set di parametri e associare una matrice di queste strutture. Ogni struttura di dati contiene i dati per una singola istruzione SQL. Questa operazione viene definita *associazione per riga* perché associa una riga di parametri.  
  
 Come quando l'applicazione associa singole variabili ai parametri, chiama **SQLBindParameter** per associare le matrici ai parametri. L'unica differenza è che gli indirizzi passati sono gli indirizzi di matrice, non gli indirizzi a variabile singola. L'applicazione imposta l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE per specificare se utilizza l'associazione per colonna (impostazione predefinita) o per riga. Se utilizzare l'associazione per colonna o per riga è in gran parte una questione di preferenza dell'applicazione. A seconda di come il processore accede alla memoria, l'associazione per riga potrebbe essere più veloce. Tuttavia, la differenza è probabilmente trascurabile, ad eccezione di un numero molto elevato di righe di parametri.  
  
## <a name="column-wise-binding"></a>Associazione per colonna  
 Quando si usa l'associazione per colonna, un'applicazione associa una o due matrici a ogni parametro per il quale devono essere forniti dati. La prima matrice contiene i valori dei dati e la seconda matrice contiene buffer di lunghezza/indicatore. Ogni matrice contiene tutti gli elementi quanti sono i valori per il parametro.  
  
 L'associazione per colonna è l'impostazione predefinita. L'applicazione può anche passare dall'associazione per riga all'associazione per colonna impostando l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE. Nella figura seguente viene illustrato il funzionamento dell'associazione per colonna.  
  
 ![Mostra il funzionamento della colonna&#45;associazione per saggio](../../../odbc/reference/develop-app/media/pr31.gif "pr31 (informazioni in base al t")  
  
 Ad esempio, il codice seguente associa matrici a 10 elementi ai parametri per le colonne PartID, Description e Price ed esegue un'istruzione per inserire 10 righe. Utilizza l'associazione per colonna.  
  
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
 Quando si usa l'associazione per riga, un'applicazione definisce una struttura per ogni set di parametri. La struttura contiene uno o due elementi per ogni parametro. Il primo elemento contiene il valore del parametro e il secondo elemento contiene il buffer di lunghezza/indicatore. L'applicazione alloca quindi una matrice di queste strutture, che contiene tutti gli elementi quanti sono i valori per ogni parametro.  
  
 L'applicazione dichiara la dimensione della struttura al driver con l'attributo di istruzione SQL_ATTR_PARAM_BIND_TYPE. L'applicazione associa gli indirizzi dei parametri nella prima struttura della matrice. Pertanto, il conducente può calcolare l'indirizzo dei dati per una particolare riga e colonna come  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 dove le righe sono numerate da 1 alla dimensione del set di parametri. L'offset, se definito, è il valore a cui punta l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR. Nella figura seguente viene illustrato il funzionamento dell'associazione per riga. I parametri possono essere posizionati nella struttura in qualsiasi ordine, ma vengono visualizzati in ordine sequenziale per maggiore chiarezza.  
  
 ![Mostra come funziona l'associazione per&#45;riga](../../../odbc/reference/develop-app/media/pr32.gif "pr32 (informazioni in cui è stato eper")  
  
 Il codice seguente crea una struttura con elementi per i valori da archiviare nelle colonne PartID, Description e Price. Alloca quindi una matrice a 10 elementi di queste strutture e la associa ai parametri per le colonne PartID, Description e Price, utilizzando l'associazione per riga. Viene quindi eseguita un'istruzione per inserire 10 righe.  
  
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
