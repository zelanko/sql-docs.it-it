---
title: Profiling dei dati sulle prestazioni del Driver (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7de38f3c91814dbd364caee84b34dacdfbdf475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200310"
---
# <a name="profile-driver-performance-data-odbc"></a>Analizzare i dati relativi alle prestazioni del driver (ODBC)
  In questo esempio vengono illustrate le opzioni specifiche del driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la registrazione delle statistiche relative alle prestazioni. L'esempio crea un file: odbcperf illustra la creazione di un file di log delle prestazioni dei dati e visualizzazione dei dati sulle prestazioni direttamente dalla struttura di dati (la struttura SQLPERF è definita in Odbcss. h.). L'esempio è stato sviluppato per ODBC versione 3.0 o successiva.  
  
> [!IMPORTANT]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando l'[API di crittografia Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>Per registrare i dati relativi alle prestazioni del driver tramite Amministratore ODBC  
  
1.  Nelle **Pannello di controllo**, fare doppio clic su **strumenti di amministrazione** e quindi fare doppio clic su **origine dati (ODBC)** . In alternativa, è possibile richiamare odbcad32.exe.  
  
2.  Scegliere il **DSN utente**, **DSN di sistema**, o **DSN su File** scheda.  
  
3.  Fare clic sull'origine dati per cui registrare le prestazioni.  
  
4.  Fare clic su **configurare**.  
  
5.  In Microsoft SQL Server di configurazione DSN guidata passare alla pagina contenente **statistiche del driver ODBC nel file di log**.  
  
6.  Selezionare **statistiche del driver ODBC nel file di log**. Nella casella immettere il nome del file in cui si desidera salvare le statistiche. Facoltativamente, fare clic su **esplorare** sfogliare il file system per il registro delle statistiche.  
  
### <a name="to-log-driver-performance-data-programmatically"></a>Per registrare i dati relativi alle prestazioni del driver a livello di programmazione  
  
1.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA_LOG e il nome di file e percorso completo del file di log dei dati sulle prestazioni. Ad esempio:  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA e SQL_PERF_START per avviare la registrazione dei dati sulle prestazioni.  
  
3.  Facoltativamente, è possibile chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_LOG_NOW e NULL per scrivere un record delimitato da tabulazioni dei dati sulle prestazioni per il file di log dei dati sulle prestazioni. Questa operazione può essere eseguita più volte durante l'esecuzione dell'applicazione.  
  
4.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA e SQL_PERF_STOP per arrestare la registrazione dei dati sulle prestazioni.  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>Per estrarre i dati relativi alle prestazioni in un'applicazione  
  
1.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA e SQL_PERF_START per avviare la profilatura i dati sulle prestazioni.  
  
2.  Chiamare [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) con SQL_COPT_SS_PERF_DATA e l'indirizzo di un puntatore a una struttura SQLPERF. La prima di tali chiamate imposta il puntatore sull'indirizzo di una struttura SQLPERF valida che contiene i dati relativi alle prestazioni correnti. Il driver non aggiorna continuamente i dati nella struttura delle prestazioni. L'applicazione deve ripetere la chiamata a [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) ogni volta che deve aggiornare la struttura con i dati sulle prestazioni più recenti.  
  
3.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA e SQL_PERF_STOP per arrestare la registrazione dei dati sulle prestazioni.  
  
## <a name="example"></a>Esempio  
 È necessaria un'origine dati ODBC denominata AdventureWorks, il cui database predefinito è il database di esempio AdventureWorks. È possibile scaricare il database di esempio AdventureWorks dalla home page del sito relativo a [progetti della community ed esempi per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=85384). Questa origine dati deve essere basata sul driver ODBC fornito dal sistema operativo (il nome del driver è "SQL Server"). Se questo esempio viene compilato ed eseguito come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
 In questo esempio viene eseguita la connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer in uso. Per connettersi a un'istanza denominata, modificare la definizione dell'origine dati ODBC per specificare l'istanza in base al formato: server\istanzadenominata. Per impostazione predefinita, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] viene installato in un'istanza denominata.  
  
 Eseguire la compilazione con odbc32.lib.  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure relative alle prestazioni del Driver ODBC di profilatura &#40;ODBC&#41;](profiling-odbc-driver-performance-odbc.md)   
 [Profilatura delle prestazioni del driver ODBC](../native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
