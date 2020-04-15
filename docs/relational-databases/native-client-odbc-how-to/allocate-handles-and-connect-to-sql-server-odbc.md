---
title: Allocare gli handle e connettersi a SQL Server (ODBC) Documenti Microsoft
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d26af711c07c4ea296d5351d0fcb0d1f9710706
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294515"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Allocare handle e connettersi a SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Per allocare handle e connettersi a SQL Server  
  
1.  Includere i file di intestazione ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Includere il file di intestazione specifico del driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Chiamare [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** di SQL_HANDLE_ENV per inizializzare ODBC e allocare un handle di ambiente.  
  
4.  Chiamare [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con **Attributo** impostato su SQL_ATTR_ODBC_VERSION e **ValuePtr** impostato su SQL_OV_ODBC3 per indicare che l'applicazione utilizzerà le chiamate di funzione in formato ODBC 3.x.  
  
5.  Facoltativamente, chiamare [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) per impostare altre opzioni di ambiente o chiamare [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) per ottenere le opzioni di ambiente.  
  
6.  Chiamare [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** di SQL_HANDLE_DBC per allocare un handle di connessione.  
  
7.  Facoltativamente, chiamare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per impostare le opzioni di connessione o chiamare [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) per ottenere le opzioni di connessione.  
  
8.  Chiamare SQLConnect per utilizzare un'origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dati esistente per connettersi a .  
  
     Oppure  
  
     Chiamare [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) per utilizzare una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]stringa di connessione per connettersi a .  
  
     Il formato minimo di una stringa di connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa può essere uno dei seguenti:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Se la stringa di connessione non è completa, **SQLDriverConnect** può richiedere le informazioni necessarie. Questo è controllato dal valore specificato per il *DriverCompletion* parametro.  
  
     \- - oppure -  
  
     Chiamare [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) più volte in modo iterativo per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]compilare la stringa di connessione e connettersi a .  
  
9. Facoltativamente, chiamare [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) per ottenere gli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attributi e il comportamento del driver per l'origine dati.  
  
10. Allocare e utilizzare le istruzioni.  
  
11. Chiamare SQLDisconnect per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disconnettersi e rendere disponibile l'handle di connessione per una nuova connessione.  
  
12. Chiamare [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) con un **HandleType** di SQL_HANDLE_DBC per liberare l'handle di connessione.  
  
13. Chiamare **SQLFreeHandle** con un **HandleType** di SQL_HANDLE_ENV per liberare l'handle di ambiente.  
  
> [!IMPORTANT]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è necessario crittografarle con [l'API di crittografia Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrata una chiamata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a **SQLDriverConnect** per connettersi a un'istanza di senza richiedere un'origine dati ODBC esistente. Passando una stringa di connessione incompleta a **SQLDriverConnect**, il driver ODBC richiede all'utente di immettere le informazioni mancanti.  
  
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
  
  
