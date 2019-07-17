---
title: Allocazione degli handle e connettersi a SQL Server (ODBC) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0dc7cad1d720489db4044bbd34c6516035305365
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090826"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Allocare handle e connettersi a SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Per allocare handle e connettersi a SQL Server  
  
1.  Includere i file di intestazione ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Includere il file di intestazione specifico del driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Chiamare [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** SQL_HANDLE_ENV per inizializzare ODBC e allocare un handle di ambiente.  
  
4.  Chiamare [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con **attributo** impostato su SQL_ATTR_ODBC_VERSION e **ValuePtr** impostato su SQL_OV_ODBC3 per indicare l'applicazione userà una funzione ODBC in formato 3.x chiamate.  
  
5.  Facoltativamente, richiamare [la funzione SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) per impostare l'ambiente di altre opzioni, oppure chiamare [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) per ottenere le opzioni di ambiente.  
  
6.  Chiamare [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** SQL_HANDLE_DBC per allocare un handle di connessione.  
  
7.  Facoltativamente, richiamare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per impostare le opzioni di connessione, oppure chiamare [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) per ottenere le opzioni di connessione.  
  
8.  Chiamare la funzione SQLConnect per utilizzare un'origine dati per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Oppure  
  
     Chiamare [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) di utilizzare una stringa di connessione per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Il formato minimo di una stringa di connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa può essere uno dei seguenti:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Se la stringa di connessione non è completa, **SQLDriverConnect** possibile richiedere le informazioni necessarie. Ciò è determinato dal valore specificato per il *DriverCompletion* parametro.  
  
     \- - oppure -  
  
     Chiamare [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) più volte in modo iterativo per generare la stringa di connessione e connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Facoltativamente, richiamare [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) per ottenere gli attributi di driver e il comportamento per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origine dati.  
  
10. Allocare e utilizzare le istruzioni.  
  
11. Richiamare la funzione SQLDisconnect per disconnettersi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e rendere disponibile la connessione gestire per una nuova connessione.  
  
12. Chiamare [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) con un **HandleType** SQL_HANDLE_DBC per liberare l'handle di connessione.  
  
13. Chiamare **SQLFreeHandle** con un **HandleType** SQL_HANDLE_ENV per liberare l'handle di ambiente.  
  
> [!IMPORTANT]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando l'[API di crittografia Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrata una chiamata a **SQLDriverConnect** per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza la necessità di un'origine dati ODBC esistente. Passando una stringa di connessione incomplete per **SQLDriverConnect**, fa sì che il driver ODBC richiedere all'utente di immettere le informazioni mancanti.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
