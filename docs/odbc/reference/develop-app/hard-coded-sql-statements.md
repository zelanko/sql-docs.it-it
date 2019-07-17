---
title: Le istruzioni SQL hard-Coded | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b0205208a28238f4fbccb5ae2fd96639b664bd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139147"
---
# <a name="hard-coded-sql-statements"></a>Istruzioni SQL hard-coded
Le applicazioni che eseguono attività fissa in genere contengono istruzioni SQL hard-coded. Ad esempio, un sistema di immissione dell'ordine potrebbe usare la chiamata seguente a ordini di vendita aperti elenco:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Esistono diversi vantaggi per le istruzioni SQL hard-coded: Possono essere verificate quando l'applicazione viene scritta; sono più semplici da implementare rispetto a istruzioni costruite in fase di esecuzione. e semplificano l'applicazione.  
  
 Usando i parametri delle istruzioni e preparazione di istruzioni forniscono modi ancora migliori per usare le istruzioni SQL hard-coded. Si supponga, ad esempio, che la tabella di parti contiene le colonne PartID, descrizione e il prezzo. Un modo per inserire una nuova riga in questa tabella, è possibile costruire ed eseguire un' **Inserisci** istruzione:  
  
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
  
 Un metodo migliore consiste nell'utilizzare un'istruzione con parametri, a livello di codice. Ciò comporta due vantaggi in un'istruzione con valori di dati hardcoded. Prima di tutto risulta più semplice costruire un'istruzione con parametri poiché i valori dei dati possono essere inviati nei rispettivi tipi nativi, ad esempio numeri interi e numeri a virgola mobile anziché convertendoli in stringhe. In secondo luogo, un'istruzione di questo tipo può essere utilizzata più di volta semplicemente eseguendo la modifica dei valori di parametro e rieseguire. non è necessario ricompilarlo.  
  
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
  
 Supponendo che questa istruzione deve essere eseguito più volte, possa essere preparato per migliorare l'efficienza ancora maggiore:  
  
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
  
 Probabilmente il modo più efficiente di utilizzare l'istruzione consiste nel creare una procedura contenente l'istruzione, come illustrato nell'esempio di codice seguente. Poiché la procedura viene costruita in fase di sviluppo e archiviata nell'origine dati, non dovrà essere preparata in fase di esecuzione. Uno svantaggio di questo metodo è che la sintassi per la creazione di procedure è specifici del DBMS e le procedure devono essere costruite separatamente per ogni sistema DBMS in cui l'applicazione deve essere eseguita.  
  
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
  
 Per altre informazioni sui parametri, le istruzioni preparate e procedure, vedere [esecuzione di un'istruzione](../../../odbc/reference/develop-app/executing-a-statement.md).
