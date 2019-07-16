---
title: Usare un'istruzione (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abf5910d032b921f6cefa1aeb89fef1a6fcfbc44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898454"
---
# <a name="use-a-statement-odbc"></a>Utilizzare un'istruzione (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-a-statement"></a>Per utilizzare un'istruzione  
  
1.  Chiamare [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con *HandleType* impostato su SQL_HANDLE_STMT per allocare un handle di istruzione.  
  
2.  È inoltre possibile chiamare [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) per impostare le opzioni dell'istruzione o [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) per ottenere gli attributi dell'istruzione.  
  
     Per utilizzare i cursori server, è necessario impostare gli attributi del cursore su valori diversi da quelli predefiniti.  
  
3.  Facoltativamente, se l'istruzione viene eseguita più volte, è possibile preparare l'istruzione per l'esecuzione con la [funzione SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360).  
  
4.  Se all'istruzione sono stati associati marcatori di parametro, è possibile associare i marcatori di parametro alle variabili di programma tramite [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md). Se l'istruzione è stata preparata, è possibile chiamare [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) e [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) per trovare il numero e le caratteristiche dei parametri.  
  
5.  Eseguire un'istruzione direttamente mediante SQLExecDirect.  
  
     \- - oppure -  
  
     Se l'istruzione è stata preparata, eseguirla più volte tramite [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400).  
  
     \- - oppure -  
  
     Chiamare una funzione di catalogo, che restituisce i risultati.  
  
6.  Elaborare i risultati associando le colonne del set di risultati alle variabili di programma, spostando i dati dalle colonne del set di risultati alle variabili di programma tramite [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) oppure usando una combinazione dei due metodi.  
  
     Recuperare il set di risultati di un'istruzione una riga alla volta.  
  
     \- - oppure -  
  
     Recuperare il set di risultati più righe alla volta mediante un cursore a blocchi.  
  
     \- - oppure -  
  
     Chiamare [SQLRowCount](../../../relational-databases/native-client-odbc-api/sqlrowcount.md) per determinare il numero di righe interessate da un'istruzione INSERT, UPDATE o DELETE.  
  
     Se l'istruzione SQL può avere più set di risultati, chiamare [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) alla fine di ogni set di risultati per stabilire se siano presenti altri set di risultati da elaborare.  
  
7.  Dopo l'elaborazione dei risultati, può essere necessario effettuare le seguenti azioni per consentire all'handle di istruzione di eseguire una nuova istruzione:  
  
    -   Se [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) non è stato chiamato fino a quando non sia stato restituito SQL_NO_DATA, chiamare [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) per chiudere il cursore.  
  
    -   Se i marcatori di parametro sono stati associati alle variabili di programma, chiamare [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *Option* impostato su SQL_RESET_PARAMS per liberare i parametri associati.  
  
    -   Se le colonne del set di risultati sono state associate alle variabili di programma, chiamare [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *Option* impostato su SQL_UNBIND per liberare le colonne associate.  
  
    -   Per riutilizzare l'handle di istruzione, andare al passaggio 2.  
  
8.  Chiamare [SQLFreeHandle](../../../relational-databases/native-client-odbc-api/sqlfreehandle.md) con *HandleType* impostato su SQL_HANDLE_STMT per liberare l'handle di istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [L'esecuzione di query procedure relative al &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
