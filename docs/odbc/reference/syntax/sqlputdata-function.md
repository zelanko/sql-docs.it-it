---
title: Funzione SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5254b7bb3744e06dae300f33ff1b612b4aca2341
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537263"
---
# <a name="sqlputdata-function"></a>SQLPutData Function
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLPutData** consente a un'applicazione inviare i dati per un parametro o della colonna per il driver in fase di esecuzione di istruzione. Questa funzione è utilizzabile per l'invio di caratteri o valori di dati binari nelle parti a una colonna con un tipo specifico dell'origine dati carattere, binary o dati (ad esempio, i parametri dei tipi SQL_LONGVARBINARY o SQL_LONGVARCHAR). **SQLPutData** supporta l'associazione a un tipo di dati Unicode C, anche se il driver sottostante non supporta i dati Unicode.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *DataPtr*  
 [Input] Puntatore a un buffer contenente i dati effettivi per il parametro o della colonna. I dati devono essere del tipo di dati C specificato nel *ValueType* argomento di **SQLBindParameter** (per i dati dei parametri) o nella *TargetType* argomento di  **SQLBindCol** (per i dati di colonna).  
  
 *StrLen_or_Ind*  
 [Input] Lunghezza di \* *DataPtr*. Specifica la quantità di dati inviati in una chiamata a **SQLPutData**. La quantità di dati può variare a ogni chiamata per una colonna o parametro specificato. *StrLen_or_Ind* viene ignorato a meno che non soddisfa una delle condizioni seguenti:  
  
-   *StrLen_or_Ind* è SQL_NTS, SQL_NULL_DATA o SQL_DEFAULT_PARAM.  
  
-   Il tipo di dati C specificato nel **SQLBindParameter** oppure **SQLBindCol** è SQL_C_CHAR o SQL_C_BINARY.  
  
-   Il tipo di dati C è SQL_C_DEFAULT, e il tipo di dati C predefinito per il tipo di dati SQL specificato è SQL_C_CHAR o SQL_C_BINARY.  
  
 Per tutti gli altri tipi di dati C, se *StrLen_or_Ind* SQL_NULL_DATA o SQL_DEFAULT_PARAM, non il driver presuppone che le dimensioni dei \* *DataPtr* buffer è la dimensione del tipo di dati C specificato con *ValueType* oppure *TargetType* e invia l'intero valore dei dati. Per altre informazioni, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) nell'appendice d: Tipi di dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLPutData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLPutData** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Stringa o dati binari restituiti per un parametro di output ha comportato il troncamento del carattere non vuote o dati binari non NULL. Se si tratta di un valore stringa, era troncati a destra. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Il valore di dati identificato dal *ValueType* argomento nella **SQLBindParameter** per non è stato possibile convertire il parametro associato al tipo di dati identificato dal *ParameterType*nell'argomento **SQLBindParameter**.|  
|07S01|Utilizzo non valido del parametro predefinito|Un valore del parametro, impostata con **SQLBindParameter**era SQL_DEFAULT_PARAM e il parametro corrispondente non è un valore predefinito.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|22001|Dati di tipo stringa, troncamento a destra|L'assegnazione di un carattere o un valore binario a una colonna ha comportato il troncamento di valore non blank (carattere) o caratteri (binari) non null o byte.<br /><br /> Il tipo di informazioni SQL_NEED_LONG_DATA_LEN nel **SQLGetInfo** è "Y", e altri dati è stati inviati per un parametro long (tipo di dati era SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long) superiore a quello specificato con il *StrLen_or_IndPtr* nell'argomento **SQLBindParameter**.<br /><br /> Il tipo di informazioni SQL_NEED_LONG_DATA_LEN nel **SQLGetInfo** è "Y", e altri dati è stati inviati per una colonna long (tipo di dati era SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long) superiore a quello specificato di corrispondente a una colonna in una riga di dati che è stato aggiunto o aggiornati con buffer di lunghezza **SQLBulkOperations** o aggiornate con **SQLSetPos**.|  
|22003|Valore numerico non compreso nell'intervallo|I dati inviati per un parametro numerico associato o colonne ha causato la parte intera (in contrapposizione frazionari) del numero da troncare quando assegnato alla colonna della tabella associata.<br /><br /> Restituzione di un valore numerico (come valore numerico o stringa) per uno o più parametri di input/output o di output avrebbe causato la parte intera (in contrapposizione frazionari) del numero da troncare.|  
|22007|Formato di datetime non valido|I dati inviati per un parametro o una colonna in cui è stata associata a una data, ora o struttura di timestamp sono, rispettivamente, una data non valida, ora o timestamp.<br /><br /> Un parametro di input/output o di output è stato associato a una data, ora o timestamp C struttura e un valore nel parametro restituito non è, rispettivamente, una data non valida, ora o timestamp. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|22008|Overflow del campo DateTime|Un'espressione datetime calcolate per input/output o parametro di output ha comportato una data, ora o struttura di timestamp C che non è valido.|  
|22012|Divisione per zero|Un'espressione aritmetica calcolato per input/output o un parametro di output ha comportato la divisione per zero.|  
|22015|Overflow del campo Interval|I dati inviati per una colonna numerica o di intervallo esatta o a un tipo di dati SQL di intervallo causa la perdita di cifre significative.<br /><br /> I dati è stati inviati per una colonna di intervallo o un parametro con più di un campo, è stati convertiti in un tipo di dati numerici e non avevano alcuna rappresentazione nel tipo di dati numerici.<br /><br /> I dati inviati per la colonna o i dati dei parametri è stati assegnati a un intervallo di tipo SQL e si è verificato alcuna rappresentazione del valore di tipo C in un intervallo di tipo SQL.<br /><br /> I dati inviati per un numerico esatto o colonna di intervallo C o un parametro a un tipo di intervallo C ha causato una perdita di cifre significative.<br /><br /> I dati inviati per la colonna o i dati dei parametri è stati assegnati a una struttura di intervallo C, e si è verificato alcun rappresentazione dei dati nella struttura di dati di intervallo.|  
|22018|Valore del carattere non valido per la specifica del cast|Il tipo C è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati carattere. il valore della colonna o parametro non ha un valore letterale valido del tipo C associato.<br /><br /> Il tipo SQL è un valore numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo C è stata SQL_C_CHAR; il valore della colonna o parametro non ha un valore letterale valido del tipo SQL associato.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY009|Utilizzo non valido del puntatore null|(DM) dell'argomento *DataPtr* era un puntatore null e l'argomento *StrLen_or_Ind* non era 0, SQL_DEFAULT_PARAM o SQL_NULL_DATA.|  
|HY010|Errore nella sequenza della funzione|(DM) la chiamata di funzione precedente non era una chiamata a **SQLPutData** oppure **SQLParamData**.<br /><br /> (DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione SQLPutData.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY019|Dati non letterali e non binari inviati in parti|**SQLPutData** è stato chiamato più di una volta per un parametro o della colonna e perché non è stato in uso per inviare dati di tipo carattere C a una colonna con un tipo di carattere, binary o dati specifici dell'origine dati o per inviare i dati binari C a una colonna con un carattere , binary o tipo di dati specifici dell'origine dati.|  
|HY020|Tenta di concatenare un valore null|**SQLPutData** viene chiamato più volte perché la chiamata che ha restituito SQL_NEED_DATA e in uno di tali chiamate, il *StrLen_or_Ind* argomento contenuti SQL_NULL_DATA o SQL_DEFAULT_PARAM.|  
|HY090|Lunghezza della stringa o buffer non valido|L'argomento *DataPtr* non è un puntatore null e l'argomento *StrLen_or_Ind* era minore di 0, ma non è uguale a SQL_NTS oppure SQL_NULL_DATA.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
 Se **SQLPutData** viene chiamato durante l'invio di dati per un parametro in un'istruzione SQL, può restituire qualsiasi valore SQLSTATE che può essere restituiti dalla funzione chiamata per eseguire l'istruzione (**SQLExecute** o**SQLExecDirect**). Se viene chiamato durante l'invio di dati per una colonna aggiornati o aggiunti con **SQLBulkOperations** o che venga aggiornato con **SQLSetPos**, può restituire qualsiasi valore SQLSTATE che può essere restituiti da  **SQLBulkOperations** oppure **SQLSetPos**.  
  
## <a name="comments"></a>Commenti  
 **SQLPutData** può essere chiamato per fornire i dati di data-at-execution per due modalità di utilizzo: i dati dei parametri da usare in una chiamata a **SQLExecute** oppure **SQLExecDirect**, o dati della colonna da utilizzare quando viene aggiornata una riga o aggiunti da una chiamata a **SQLBulkOperations** o viene aggiornato da una chiamata a **SQLSetPos**.  
  
 Quando un'applicazione chiama **SQLParamData** per determinare quali dati devono inviare, il driver restituisce un indicatore che l'applicazione può usare per determinare quali dati di parametro per inviare o in cui sono presenti dati della colonna. Anche restituito SQL_NEED_DATA, che è un indicatore per l'applicazione che deve chiamare **SQLPutData** per inviare i dati. Nel *DataPtr* argomento **SQLPutData**, l'applicazione passa un puntatore al buffer contenente i dati effettivi per il parametro o della colonna.  
  
 Quando il driver restituisce SQL_SUCCESS per **SQLPutData**, l'applicazione chiama **SQLParamData** nuovamente. **SQLParamData** restituisce SQL_NEED_DATA se i dati di altre devono essere inviati, nel qual caso l'applicazione chiama **SQLPutData** nuovamente. Restituisce SQL_SUCCESS se tutti i dati di data-at-execution è stato inviato. L'applicazione chiama quindi **SQLParamData** nuovamente. Se il driver restituisce SQL_NEED_DATA e un altro indicatore  *\*ValuePtrPtr*, sono necessari i dati per un altro parametro o della colonna e **SQLPutData** viene chiamato nuovamente. Se il driver restituisce SQL_SUCCESS, quindi tutti i data-at-execution sono stati inviati dati e l'istruzione SQL può essere eseguita o la **SQLBulkOperations** oppure **SQLSetPos** chiamata può essere elaborata.  
  
 Per altre informazioni sui dati di parametro come data-at-execution sono passate in fase di esecuzione di istruzione, vedere "Passaggio di valori di parametro" nella [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [l'invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md). Per altre informazioni sui dati di colonna come data-at-execution sono state aggiornate o aggiunto, vedere la sezione "Uso SQLSetPos" nella [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Esecuzione di operazioni Bulk aggiornamenti mediante segnalibri" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [Dati di tipo long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Un'applicazione può utilizzare **SQLPutData** per inviare dati in parti solo quando si inviano dati di tipo carattere C a una colonna con un tipo di carattere, binary o dati specifici dell'origine dati o per l'invio di dati C binari a una colonna con un carattere, binario, o dati tipo di dati specifici dell'origine. Se **SQLPutData** viene chiamato più volte in qualsiasi altra condizione, restituisce SQL_ERROR e SQLSTATE HY019 (dati Non letterali e non binari inviati in parti).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente presuppone che un nome dell'origine dati denominato Test. Il database associato deve avere una tabella che è possibile creare, come indicato di seguito:  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
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
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
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
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a un parametro|[Funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'istruzione SQL|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Eseguire un'istruzione SQL preparata|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituisce il parametro successivo per l'invio di dati|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
