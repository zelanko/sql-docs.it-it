---
title: Impostazione delle opzioni del cursore (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01847d48b4f8791f5171e05284eb6eabd62a0af7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293841"
---
# <a name="set-cursor-options-odbc"></a>Impostare le opzioni del cursore (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per impostare le opzioni del cursore, chiamare [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) per impostare o [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) per ottenere le opzioni dell'istruzione che controllano il comportamento del cursore.  
  
|*Attributo*|Specifica|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|Tipo di cursore: forward only, statico, dinamico o gestito da keyset|  
|SQL_ATTR_CONCURRENCY|Opzione di controllo della concorrenza: di sola lettura, di blocco, ottimistica che utilizza timestamp o ottimistica che utilizza valori|  
|SQL_ATTR_ROW_ARRAY_SIZE|Numero di righe recuperate in ogni operazione di recupero|  
|SQL_ATTR_CURSOR_SENSITIVITY|Cursore che mostra o non mostra aggiornamenti a righe di cursore create da altre connessioni|  
|SQL_ATTR_CURSOR_SCROLLABLE|Cursore che è possibile scorrere in avanti e indietro|  
  
 I valori predefiniti per questi attributi (forward only, di sola lettura, dimensione 1 del set di righe) non determinano l'utilizzo dei cursori server. Per utilizzare i cursori server, è necessario che almeno uno di questi attributi sia impostato su un valore diverso dall'impostazione predefinita e che l'istruzione eseguita sia un'istruzione SELECT singola o una stored procedure che contiene un'istruzione SELECT singola. In caso di utilizzo di cursori server, le istruzioni SELECT non possono utilizzare le clausole non supportate dai cursori server: COMPUTE, COMPUTE BY, FOR BROWSE e INTO.  
  
 È possibile controllare il tipo di cursore utilizzato impostando SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY oppure impostando SQL_ATTR_CURSOR_SENSITIVITY e SQL_ATTR_CURSOR_SCROLLABLE. È consigliabile non combinare i due metodi di definizione del comportamento del cursore.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene allocato un handle di istruzione, viene impostato un tipo di cursore dinamico con concorrenza ottimistica del controllo delle versioni delle righe, quindi viene eseguita un'istruzione SELECT.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene allocato un handle di istruzione, viene impostato un cursore scorrevole di tipo sensitive, quindi viene eseguita un'istruzione SELECT  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query procedure relative agli argomenti &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
