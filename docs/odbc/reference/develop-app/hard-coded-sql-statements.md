---
title: Istruzioni SQL hardcoded | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300201"
---
# <a name="hard-coded-sql-statements"></a>Istruzioni SQL hard-coded
Le applicazioni che eseguono un'attività fissa contengono in genere istruzioni SQL hardcoded. Ad esempio, un sistema di immissione degli ordini può utilizzare la chiamata seguente per elencare gli ordini di vendita aperti:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Sono disponibili diversi vantaggi per le istruzioni SQL hardcoded, che possono essere testate quando viene scritta l'applicazione; sono più semplici da implementare rispetto alle istruzioni costruite in fase di esecuzione. e semplificano l'applicazione.  
  
 L'utilizzo dei parametri di istruzione e della preparazione di istruzioni fornisce un modo ancora migliore per utilizzare istruzioni SQL hardcoded. Si supponga, ad esempio, che la tabella Parts includa le colonne PartID, Description e price. Un modo per inserire una nuova riga in questa tabella consiste nel costruire ed eseguire un'istruzione **Insert** :  
  
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
  
 Un modo ancora migliore consiste nell'usare un'istruzione con parametri hardcoded. Questa operazione presenta due vantaggi rispetto a un'istruzione con valori di dati hardcoded. In primo luogo, è più semplice costruire un'istruzione con parametri perché i valori dei dati possono essere inviati nei relativi tipi nativi, ad esempio numeri interi e numeri a virgola mobile, anziché convertirli in stringhe. In secondo luogo, tale istruzione può essere usata più di una volta semplicemente modificando i valori dei parametri e eseguendola di nuovo; non è necessario ricompilarlo.  
  
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
  
 Supponendo che questa istruzione venga eseguita più di una volta, può essere preparata per un'efficienza ancora maggiore:  
  
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
  
 Probabilmente il modo più efficiente per utilizzare l'istruzione è creare una routine che contiene l'istruzione, come illustrato nell'esempio di codice seguente. Poiché la procedura viene costruita in fase di sviluppo e archiviata nell'origine dati, non è necessario prepararla in fase di esecuzione. Uno svantaggio di questo metodo è che la sintassi per la creazione di procedure è specifica di DBMS e le procedure devono essere costruite separatamente per ogni DBMS in cui l'applicazione deve essere eseguita.  
  
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
  
 Per ulteriori informazioni sui parametri, le istruzioni preparate e le procedure, vedere [esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).
