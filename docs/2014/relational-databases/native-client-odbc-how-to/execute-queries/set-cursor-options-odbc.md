---
title: Impostare le opzioni del cursore (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
author: rothja
ms.author: jroth
ms.openlocfilehash: 915f449a11278f3ef7503caf0a588cc48d6cf23e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018715"
---
# <a name="set-cursor-options-odbc"></a>Impostare le opzioni del cursore (ODBC)
  Per impostare le opzioni del cursore, chiamare [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) per impostare o [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) per ottenere le opzioni di istruzione che controllano il comportamento del cursore.  
  
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
 [Procedure relative all'esecuzione di query &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
