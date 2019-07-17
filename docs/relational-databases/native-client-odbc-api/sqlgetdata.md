---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 576551308b2ad7cc195b5425a50f2764b3cf6ad5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135442"
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLGetData** viene usato per recuperare i dati dei set di risultati senza associare valori della colonna. **SQLGetData** può essere successivamente chiamato sulla stessa colonna per recuperare grandi quantità di dati da una colonna con un **testo**, **ntext**, oppure **immagine** tipo di dati.  
  
 Non è necessario che un'applicazione associ le variabili per recuperare i dati del set di risultati. I dati di qualsiasi colonna possono essere recuperati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client utilizzando **SQLGetData**.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client non supporta l'uso **SQLGetData** per recuperare i dati in ordine di colonne casuale. Tutte le colonne non associate elaborate con **SQLGetData** deve avere gli ordinali di colonna maggiore rispetto alle colonne associate nel set di risultati. L'applicazione deve elaborare i dati dal valore della colonna dell'ordinale non associato più basso al più elevato. Il tentativo di recuperare dati dalla colonna con una numerazione di ordinali più bassa genera un errore. Se l'applicazione sta utilizzando i cursori del server per indicare le righe del set di risultati, può recuperare nuovamente la riga corrente e quindi recuperare il valore di una colonna. Se un'istruzione viene eseguita sul cursore forward-only in sola lettura predefinito, sarà necessario eseguire nuovamente l'istruzione per eseguire il backup **SQLGetData**.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client riporta in maniera accurata la lunghezza del **testo**, **ntext**, e **immagine** i dati recuperati tramite **SQLGetData** . L'applicazione può avvalersi del *StrLen_or_IndPtr* parametro restituito per recuperare rapidamente i dati di tipo long.  
  
> [!NOTE]  
>  Per i tipi di valori di grandi dimensioni, *StrLen_or_IndPtr* restituirà SQL_NO_TOTAL nei casi di troncamento dei dati.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetData per le caratteristiche avanzate di data e ora  
 I valori di colonna risultato dei tipi data/ora vengono convertiti come descritto in [le conversioni da SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>Supporto di SQLGetData per tipi definiti dall'utente CLR di grandi dimensioni  
 **SQLGetData** supporta grandi CLR tipi definiti dall'utente (UDT). Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="example"></a>Esempio  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetData](https://go.microsoft.com/fwlink/?LinkId=59350)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
