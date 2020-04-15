---
title: Istruzioni SQL hardcoded Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a092742e5f0151b7b08f434b453645cbd804a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300201"
---
# <a name="hard-coded-sql-statements"></a>Istruzioni SQL hard-coded
Le applicazioni che eseguono un'attività fissa contengono in genere istruzioni SQL hardcoded. Ad esempio, un sistema di immissione ordini potrebbe utilizzare la chiamata seguente per elencare gli ordini cliente aperti:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Le istruzioni SQL hardcoded offrono diversi vantaggi: possono essere testate quando viene scritta l'applicazione; sono più semplici da implementare rispetto alle istruzioni costruite in fase di esecuzione; e semplificano l'applicazione.  
  
 L'utilizzo di parametri di istruzione e la preparazione di istruzioni offrono modi ancora migliori per utilizzare istruzioni SQL hardcoded. Si supponga, ad esempio, che la tabella Parts contenga le colonne PartID, Description e Price. Un modo per inserire una nuova riga in questa tabella consiste nel costruire ed eseguire un'istruzione **INSERT:One** way to insert a new row into this table would be to construct and execute an INSERT statement:  
  
```  
#define DESC_LEN 51  
#define STATEMENT_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN], Statement[STATEMENT_LEN];  
SQLREAL       Price;  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Build INSERT statement.  
sprintf_s(Statement, 100, "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (%d, '%s', %f)", PartID, Desc, Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Un modo ancora migliore consiste nell'utilizzare un'istruzione con parametri hardcoded. Questo ha due vantaggi rispetto a un'istruzione con valori di dati hardcoded. In primo luogo, è più semplice costruire un'istruzione con parametri perché i valori dei dati possono essere inviati nei relativi tipi nativi, ad esempio numeri interi e numeri a virgola mobile, anziché convertirli in stringhe. In secondo luogo, tale istruzione può essere utilizzata più di una volta semplicemente modificando i valori dei parametri e rieseguindola; non c'è bisogno di ricostruirlo.  
  
```  
#define DESC_LEN 51  
  
SQLCHAR * Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Supponendo che questa istruzione deve essere eseguita più di una volta, può essere preparata per un'efficienza ancora maggiore:Assuming this statement is to be executed more than once, it can be prepared for even greater efficiency:  
  
```  
#define DESC_LEN 51  
  
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Prepare the INSERT statement.  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecute(hstmt);  
```  
  
 Forse il modo più efficiente per utilizzare l'istruzione consiste nel costruire una routine contenente l'istruzione, come illustrato nell'esempio di codice seguente. Poiché la procedura viene costruita in fase di sviluppo e archiviata nell'origine dati, non è necessario prepararla in fase di esecuzione. Uno svantaggio di questo metodo è che la sintassi per la creazione di procedure è specifica del DBMS e le procedure devono essere costruite separatamente per ogni DBMS in cui deve essere eseguita l'applicazione.  
  
```  
#define DESC_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecDirect(hstmt, "{call InsertPart(?, ?, ?)}", SQL_NTS);  
```  
  
 Per ulteriori informazioni su parametri, istruzioni preparate e procedure, vedere [Esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).
