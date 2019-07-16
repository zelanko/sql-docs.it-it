---
title: bcp_init | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_init
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e47c7c4f5324da021db2624e5e936493fd54ea45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895527"
---
# <a name="bcpinit"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Inizializza l'operazione di copia bulk.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *szTable*  
 Nome della tabella di database per la copia interna o esterna. Il nome può includere anche il nome del database o del proprietario, Ad esempio, **pubs.gracie.titles**, **pubs... titoli**, **gracie. titles**, e **titoli** sono tutti i nomi di tabella validi.  
  
 Se *eDirection* è DB_OUT, *szTable* può anche essere il nome di una vista di database.  
  
 Se *eDirection* DB_OUT e viene specificata un'istruzione SELECT utilizzando [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) prima [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) viene chiamato **bcp_init** *szTable* deve essere impostato su NULL.  
  
 *szDataFile*  
 Nome del file utente per la copia interna o esterna. Se i dati vengono copiati direttamente dalle variabili tramite [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), impostare *szDataFile* su NULL.  
  
 *szErrorFile*  
 Nome del file degli errori in cui inserire messaggi di stato, messaggi di errore e copie delle righe che per qualche motivo non è stato possibile copiare da un file utente in una tabella. Se NULL viene passato come *szErrorFile*, non viene usato alcun file degli errori.  
  
 *eDirection*  
 Direzione della copia, ovvero DB_IN oppure DB_OUT. DB_IN indica una copia da variabili di programma o da un file utente a una tabella. DB_OUT indica una copia da una tabella di database a un file utente. È necessario specificare un nome di file utente con DB_OUT.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Chiamare **bcp_init** prima di chiamare qualsiasi altra funzione di copia bulk. **bcp_init** esegue le inizializzazioni necessarie per una copia bulk dei dati tra la workstation e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Il **bcp_init** funzione deve essere fornita con un handle di connessione ODBC abilitato per l'uso con funzioni di copia bulk. Per abilitare l'handle, usare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_BCP impostato su SQL_BCP_ON su un handle di connessione allocato ma non collegato. Il tentativo di assegnare l'attributo su un handle collegato comporta un errore.  
  
 Quando viene specificato un file di dati, **bcp_init** esamina la struttura della tabella di database origine o destinazione, non il file di dati. **bcp_init** specifica i valori di formato di dati per il file di dati in base a ogni colonna nella tabella di database, visualizzazione o set di risultati SELECT. Questa specifica include il tipo di dati di ogni colonna, la presenza o meno di un indicatore di lunghezza o Null e di stringhe di byte con carattere di terminazione nei dati e la larghezza dei tipi di dati a lunghezza fissa. **bcp_init** imposta questi valori come indicato di seguito:  
  
-   Il tipo di dati specificato è quello della colonna della vista o della tabella di database oppure del set di risultati SELECT. Il tipo di dati viene enumerato in base ai tipi di dati nativi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificati in sqlncli.h. I dati vengono rappresentati nel relativo formato elettronico, Vale a dire i dati da una colonna di **integer** tipo di dati è rappresentato da una sequenza a quattro byte big- o LITTLE_ENDIAN a seconda del computer che ha creato il file di dati.  
  
-   Se un tipo di dati del database ha una lunghezza fissa, anche i dati del file di dati presenteranno una lunghezza fissa. Funzioni di copia bulk che elaborano i dati (ad esempio, [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)) analizzano le righe di dati prevedendo che la lunghezza dei dati nel file di dati sia identica alla lunghezza dei dati specificata nella tabella di database, visualizzazione o elenco di colonne SELECT. Ad esempio, i dati per una colonna del database definito come **char(13** devono essere rappresentati da 13 caratteri per ogni riga di dati nel file. I dati a lunghezza fissa possono essere preceduti da un indicatore Null se la colonna del database consente valori Null.  
  
-   Quando viene definita la sequenza di byte con caratteri di terminazione, la lunghezza di tale sequenza è impostata su 0.  
  
-   Quando si esegue la copia in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il file di dati deve includere dati per ogni colonna della tabella di database. Quando si esegue la copia da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i dati di tutte le colonne della vista o della tabella di database o del set di risultati SELECT vengono copiati nel file di dati.  
  
-   Quando si esegue la copia dati di in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la posizione ordinale di una colonna nel file di dati deve essere identica alla posizione ordinale della colonna nella tabella di database. Durante la copia da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp_exec** inserisce dati in base alla posizione ordinale della colonna nella tabella di database.  
  
-   Se un tipo di dati di database è di lunghezza variabile (ad esempio, **varbinary(22)** ) o se una colonna del database può contenere valori null, i dati nel file di dati sono preceduti da un indicatore di lunghezza o null. La larghezza dell'indicatore varia in base al tipo di dati e alla versione della copia bulk.  
  
 Per modificare i valori del formato dati specificati per un file di dati, chiamare [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
 Le copie bulk eseguite in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere ottimizzate per le tabelle che non contengono indici impostando il modello di recupero del database su SIMPLE o BULK_LOGGED. Per altre informazioni, vedere [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md) e [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Se non viene usato alcun file di dati, è necessario chiamare [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) per specificare il formato e la posizione in memoria dei dati per ogni colonna, quindi copiare le righe di dati per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrato come utilizzare la funzione ODBC bcp_init con un file di formato.  
  
 Prima di compilare ed esegue il codice C++, è necessario effettuare le operazioni seguenti:  
  
-   Creare un'origine dati ODBC denominata Test. È possibile associare questa origine dati a qualsiasi database.  
  
-   Eseguire sul database l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   Nella directory in cui verrà eseguita l'applicazione aggiungere un file denominato Bcpfmt.fmt e aggiungervi il codice seguente:  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   Nella directory in cui verrà eseguita l'applicazione aggiungere un file denominato Bcpodbc.bcp e aggiungervi il codice seguente:  
  
    ```  
    1  
    2  
    ```  
  
 A questo punto è possibile compilare ed eseguire il codice C++.  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
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
   SDWORD cRows;  
  
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
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
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
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
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
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
