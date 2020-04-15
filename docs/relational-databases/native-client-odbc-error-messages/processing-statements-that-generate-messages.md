---
title: Istruzioni di elaborazione che generano messaggi Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9820e202f5032423292c4306aa63b175bce550b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304692"
---
# <a name="processing-statements-that-generate-messages"></a>Elaborazione di istruzioni che generano messaggi
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le opzioni STATISTICS TIME e STATISTICS IO dell'istruzione SET [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono utilizzate per ottenere informazioni utili per la diagnosi di query con esecuzione prolungata. Le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano inoltre l'opzione SHOWPLAN per l'analisi di piani di query. È possibile impostare queste opzioni in un'applicazione ODBC eseguendo le istruzioni seguenti:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Quando SET STATISTICS TIME o SET SHOWPLAN sono ON, **SQLExecute** e **SQLExecDirect** restituiscono SQL_SUCCESS_WITH_INFO e, a questo punto, l'applicazione può recuperare l'output SHOWPLAN o STATISTICS TIME chiamando **SQLGetDiagRec** finché non restituisce SQL_NO_DATA. Ogni riga di dati SHOWPLAN viene restituita nel formato:  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0 ha sostituito l'opzione SHOWPLAN con SHOWPLAN_ALL e SHOWPLAN_TEXT. Entrambe restituiscono l'output come set di risultati, non come set di messaggi.  
  
 Ogni riga di dati STATISTICS TIME viene restituita nel formato:  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 L'output di SET STATISTICS IO non è disponibile fino alla fine di un set di risultati. Per ottenere l'output di I/O STATISTICS, l'applicazione chiama **SQLGetDiagRec** al momento **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) restituisce SQL_NO_DATA. L'output di STATISTICS IO viene restituito nel formato:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Utilizzo di istruzioni DBCC  
 Le istruzioni DBCC restituiscono i dati come messaggi, non come set di risultati. **SQLExecDirect** o **SQLExecute** restituiscono SQL_SUCCESS_WITH_INFO e l'applicazione recupera l'output chiamando **SQLGetDiagRec** fino a quando non restituisce SQL_NO_DATA.  
  
 Nell'istruzione seguente, ad esempio, viene restituito SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Chiamate a SQLGetDiagRec restituiscono:Calls to **SQLGetDiagRec** return:  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>Utilizzo delle istruzioni PRINT e RAISERROR  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]Anche le istruzioni PRINT e RAISERROR restituiscono dati chiamando **SQLGetDiagRec**. Le istruzioni PRINT fanno sì che l'esecuzione dell'istruzione SQL restituisca SQL_SUCCESS_WITH_INFO e una chiamata successiva a **SQLGetDiagRec** restituisce un *SQLState* pari a 01000. Un'istruzione RAISERROR con livello di gravità dieci o inferiore si comporta esattamente come PRINT. Un RAISERROR con gravità pari a 11 o superiore fa sì che l'esecuzione restituisca SQL_ERROR e una chiamata successiva a **SQLGetDiagRec** restituisce *SQLState* 42000. Nell'istruzione seguente, ad esempio, viene restituito SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 Chiamata **di SQLGetDiagRec** restituisce:Calling SQLGetDiagRec returns:  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 Nell'istruzione seguente, ad esempio, viene restituito SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 Chiamata **di SQLGetDiagRec** restituisce:Calling SQLGetDiagRec returns:  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 L'istruzione seguente restituisce SQL_ERROR:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 Chiamata **di SQLGetDiagRec** restituisce:Calling SQLGetDiagRec returns:  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 La tempistica della chiamata **a SQLGetDiagRec** è fondamentale quando l'output delle istruzioni PRINT o RAISERROR è incluso in un set di risultati. La chiamata a **SQLGetDiagRec** per recuperare l'output PRINT o RAISERROR deve essere effettuata immediatamente dopo l'istruzione che riceve SQL_ERROR o SQL_SUCCESS_WITH_INFO. Si tratta di un processo diretto quando viene eseguita una sola istruzione SQL, come negli esempi precedenti. In questi casi, la chiamata a **SQLExecDirect** o **SQLExecute** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** può quindi essere chiamato. Il processo è meno diretto quando vengono codificati i cicli per gestire l'output di un batch di istruzioni SQL o quando vengono eseguite le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 In questo caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un set di risultati per ogni istruzione SELECT eseguita in un batch o in una stored procedure. Se il batch o la stored procedure contiene le istruzioni PRINT o RAISERROR, il relativo output viene interfacciato con il set di risultati dell'istruzione SELECT. Se la prima istruzione del batch o della routine è PRINT o RAISERROR, **SQLExecute** o **SQLExecDirect** restituisce SQL_SUCCESS_WITH_INFO o SQL_ERROR e l'applicazione deve chiamare **SQLGetDiagRec** finché non viene restituita SQL_NO_DATA per recuperare le informazioni PRINT o RAISERROR.  
  
 Se l'istruzione PRINT o RAISERROR viene dopo un'istruzione SQL, ad esempio un'istruzione SELECT, vengono restituite le informazioni PRINT o RAISERROR quando [SQLMoreResults viene](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)posizionato sul set di risultati contenente l'errore. **SQLMoreResults** restituisce SQL_SUCCESS_WITH_INFO o SQL_ERROR a seconda della gravità del messaggio. I messaggi vengono recuperati chiamando **SQLGetDiagRec** fino a quando non restituisce SQL_NO_DATA.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
