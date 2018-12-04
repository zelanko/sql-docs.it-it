---
title: Resilienza di connessione nel driver ODBC di Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b7a27d9358d6f7f5719aaf1fea1fb292b2db1af
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545293"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Resilienza di connessione nel driver ODBC di Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Per garantire che le applicazioni rimangano connesse a un [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], il driver ODBC di Windows può ripristinare le connessioni inattive.  
  
> [!IMPORTANT]  
>  La funzionalità di resilienza di connessione è supportata nelle versioni server dei database SQL di Microsoft Azure e in SQL Server 2014 (e versioni successive).  
  
 Per altre informazioni sulla resilienza delle connessioni inattive, vedere l'articolo tecnico [Idle Connection Resiliency](https://go.microsoft.com/fwlink/?LinkId=393996) (Resilienza delle connessioni inattive).  
  
 Per controllare il comportamento di riconnessione, il driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows include due opzioni:  
  
-   ConnectRetryCount.  
  
     ConnectRetryCount consente di controllare il numero di tentativi di riconnessione se si verifica un errore di connessione. I valori validi sono compresi tra 0 e 255. Zero (0) indica che non si tenta di ripristinare la connessione. Il valore predefinito è un tentativo di riconnessione.  
  
     È possibile modificare il numero di tentativi di connessione quando si:  
  
    -   Definisce o modifica un'origine dati che usa ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con il controllo **ConnectRetryCount** .  
  
    -   Usa la parola chiave della stringa di connessione **ConnectRetryCount** .  
  
     Per recuperare il numero di tentativi di connessione, usare l'attributo di connessione **SQL_COPT_SS_CONNECT_RETRY_COUNT** (sola lettura). Se un'applicazione si connette a un server che non supporta la resilienza di connessione, **SQL_COPT_SS_CONNECT_RETRY_COUNT** restituisce 0.  
  
-   ConnectRetryInterval.  
  
     ConnectRetryInterval consente di specificare il numero di secondi che deve intercorrere tra ogni tentativo di connessione. I valori validi sono 1-60. Il tempo totale per ristabilire la connessione non può superare il timeout della connessione (SQL_ATTR_QUERY_TIMEOUT in SQLSetStmtAttr). Il valore predefinito è 10 secondi.  
  
     È possibile modificare l'intervallo tra i tentativi di connessione quando si:  
  
    -   Definisce o modifica un'origine dati che usa ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con il controllo **ConnectRetryInterval** .  
  
    -   Usa la parola chiave della stringa di connessione **ConnectRetryInterval** .  
  
     Per recuperare la lunghezza dell'intervallo tra i tentativi di connessione, usare l'attributo di connessione **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (sola lettura).  
  
 Se un'applicazione stabilisce una connessione con SQL_DRIVER_COMPLETE_REQUIRED e successivamente cerca di eseguire un'istruzione su una connessione interrotta, il driver ODBC non visualizzerà di nuovo la finestra di dialogo. Inoltre, durante il ripristino:  
  
-   Durante il ripristino, qualsiasi chiamata a **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** deve restituire **SQL_CD_FALSE**.  
  
-   Se il ripristino non riesce, qualsiasi chiamata a **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** deve restituire **SQL_CD_TRUE**.  
  
 I seguenti codici di stato vengono restituiti da qualsiasi funzione che esegue un comando nel server:  
  
|State|Message|  
|-----------|-------------|  
|IMC01|La connessione è interrotta e il ripristino non è possibile. Il driver client ha tentato di ripristinare la connessione una o più volte e tutti i tentativi sono falliti. Aumentare il valore di ConnectRetryCount per aumentare il numero di tentativi di ripristino.|  
|IMC02|Il server non ha riconosciuto il tentativo di ripristino; il ripristino della connessione non è possibile.|  
|IMC03|Il server non ha conservato la versione TDS client esatta richiesta durante un tentativo di ripristino; il ripristino della connessione non è possibile.|  
|IMC04|Il server non ha conservato la versione principale del server esatta richiesta durante un tentativo di ripristino; il ripristino della connessione non è possibile.|  
|IMC05|La connessione è interrotta e il ripristino non è possibile. La connessione è stata contrassegnata dal server come non ripristinabile. Non è stato eseguito alcun tentativo di ripristinare la connessione.|  
|IMC06|La connessione è interrotta e il ripristino non è possibile. La connessione è stata contrassegnata dal driver client come non ripristinabile. Non è stato eseguito alcun tentativo di ripristinare la connessione.|  
  
## <a name="example"></a>Esempio  
 L'esempio seguente contiene due funzioni. **func1** illustra come connettersi con un nome origine dati (DSN) che usa ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows. DSN usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e specifica l'ID utente. **func1** quindi recupera il numero di tentativi di connessione con **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
 **func2** usa **SQLDriverConnect**, la parola chiave della stringa di connessione **ConnectRetryCount** e attributi di connessione per recuperare l'impostazione relativa ai tentativi di connessione e all'intervallo tra i tentativi.  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
