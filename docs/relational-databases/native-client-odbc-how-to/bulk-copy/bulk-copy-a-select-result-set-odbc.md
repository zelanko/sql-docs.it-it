---
title: Copia bulk di un Set di risultati SELECT (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC]
- bulk copy [ODBC], data files
- bulk copy [ODBC], about bulk copy
ms.assetid: 63d5a87b-4d5f-449b-8c77-9f9cc6b190d4
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ca6bd8711bf0c3fb292f795141e9da981a5dcde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099409"
---
# <a name="bulk-copy-a-select-result-set-odbc"></a>Eseguire una copia bulk di un set di risultati SELECT (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Nell'esempio viene illustrato come utilizzare le funzioni di copia bulk per eseguire la copia bulk del set di risultati di un'istruzione SELECT. L'esempio è stato sviluppato per ODBC versione 3.0 o successiva.  
  
> [!IMPORTANT]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando l'[API di crittografia Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
### <a name="to-bulk-copy-out-the-result-set-of-a-select-statement"></a>Per eseguire la copia bulk per l'esportazione del set di risultati di un'istruzione SELECT.  
  
1.  Allocare un handle di ambiente e un handle di connessione.  
  
2.  Impostare SQL_COPT_SS_BCP e SQL_BCP_ON in modo da abilitare le operazioni di copia bulk.  
  
3.  Connettersi a SQL Server.  
  
4.  Chiamare [bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) per impostare le informazioni seguenti:  
  
    -   Specificare NULL per il *szTable* parametro.  
  
    -   Nome del file di dati mediante il quale si ricevono i dati del set di risultati.  
  
    -   Nome di un file di dati per la ricezione di eventuali messaggi di errore della copia bulk (specificare NULL se non si desidera che venga creato un file dei messaggi).  
  
    -   La direzione della copia: DB_OUT.  
  
5.  Chiamare [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), impostare eOption su BCPHINTS e inserire in iValue un puntatore a una matrice SQLTCHAR contenente l'istruzione SELECT.  
  
6.  Chiamare [bcp_exec](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) per eseguire l'operazione di copia bulk.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Quando vengono seguiti questi passaggi, il file viene creato in formato nativo. È possibile convertire i valori dei dati per altri tipi di dati mediante [bcp_colfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md). Per altre informazioni, vedere [creare un File di formato di copia Bulk &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/create-a-bulk-copy-format-file-odbc.md).  
  
## <a name="example"></a>Esempio  
 È necessaria un'origine dati ODBC denominata AdventureWorks, il cui database predefinito è il database di esempio AdventureWorks. È possibile scaricare il database di esempio AdventureWorks dalla home page del sito relativo a [progetti della community ed esempi per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=85384). Questa origine dati deve essere basata sul driver ODBC fornito dal sistema operativo (il nome del driver è "SQL Server"). Se questo esempio viene compilato ed eseguito come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
 In questo esempio viene eseguita la connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel computer in uso. Per connettersi a un'istanza denominata, modificare la definizione dell'origine dati ODBC per specificare l'istanza in base al formato: server\istanzadenominata. Per impostazione predefinita, [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] viene installato in un'istanza denominata.  
  
 Eseguire la compilazione con odbc32.lib e odbcbcp.lib.  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;  
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Bulk copy variables.  
   SDWORD cRows;  
   SQLTCHAR szBCPQuery[] = "SELECT BirthDate FROM HumanResources.Employee";  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set bulk copy mode, and then connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample use Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, NULL, "BCPODBC.bcp", "BCPERROR.out", DB_OUT);  
   // The test is for the bulk copy return of SUCCEED, not the ODBC return of SQL_SUCCESS.  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Specify the query to use.  
   retcode = bcp_control(hdbc1, BCPHINTS, (void *)szBCPQuery);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_control(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied out = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Copia di massa dei con le procedure SQL Server ODBC Driver &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)  
  
  
