---
title: Funzione SQLPutData . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300041"
---
# <a name="sqlputdata-function"></a>SQLPutData Function
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLPutData** consente a un'applicazione di inviare dati per un parametro o una colonna al driver in fase di esecuzione dell'istruzione. Questa funzione può essere utilizzata per inviare valori di dati di tipo carattere o binario in parti a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati(ad esempio, parametri dei tipi SQL_LONGVARBINARY o SQL_LONGVARCHAR). **SQLPutData** supporta l'associazione a un tipo di dati Unicode C, anche se il driver sottostante non supporta i dati Unicode.SQLPutData supports binding to a Unicode C data type, even if the underlying driver does not support Unicode data.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *DataPtr*  
 [Ingresso] Puntatore a un buffer contenente i dati effettivi per il parametro o la colonna. I dati devono essere nel tipo di dati C specificato nel *ValueType* argomento di **SQLBindParameter** (per i dati di parametro) o il *TargetType* argomento di **SQLBindCol** (per i dati di colonna).  
  
 *StrLen_or_Ind*  
 [Ingresso] Lunghezza \*di *DataPtr*. Specifica la quantità di dati inviati in una chiamata a **SQLPutData**. La quantità di dati può variare a ogni chiamata per un determinato parametro o colonna. *StrLen_or_Ind* viene ignorato a meno che non soddisfi una delle seguenti condizioni:  
  
-   *StrLen_or_Ind* è SQL_NTS, SQL_NULL_DATA o SQL_DEFAULT_PARAM.  
  
-   Il tipo di dati C specificato in **SQLBindParameter** o **SQLBindCol** è SQL_C_CHAR o SQL_C_BINARY.  
  
-   Il tipo di dati C è SQL_C_DEFAULT e il tipo di dati C predefinito per il tipo di dati SQL specificato è SQL_C_CHAR o SQL_C_BINARY.  
  
 Per tutti gli altri tipi di dati C, se *StrLen_or_Ind* non è \*SQL_NULL_DATA o SQL_DEFAULT_PARAM, il driver presuppone che la dimensione del buffer *DataPtr* sia la dimensione del tipo di dati C specificato con *ValueType* o *TargetType* e invia l'intero valore dei dati. Per altre informazioni, vedere [Conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) nell'Appendice D: tipi di dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLPutData** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLPutData** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Dati stringa o binari restituiti per un parametro di output hanno determinato il troncamento di caratteri non vuoti o dati binari non NULL. Se si tratta di un valore stringa, è stato troncato a destra. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07006|Violazione dell'attributo del tipo di dati con restrizioniRestricted data type attribute violation|Impossibile convertire il valore di dati identificato dall'argomento *ValueType* in **SQLBindParameter** per il parametro associato nel tipo di dati identificato dall'argomento *ParameterType* in **SQLBindParameter**.|  
|07S01 (in titola del sistema)|Utilizzo non valido del parametro predefinito|Un valore di parametro, impostato con **SQLBindParameter**, è stato SQL_DEFAULT_PARAM e il parametro corrispondente non dispone di un valore predefinito.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|22001|Dati stringa, troncamento a destra|L'assegnazione di un carattere o di un valore binario a una colonna ha determinato il troncamento di caratteri o byte non vuoti (carattere) o non null (binario).<br /><br /> Il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** era "Y" e sono stati inviati più dati per un parametro long (il tipo di dati è stato SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati lungo) di quello specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**.<br /><br /> Il SQL_NEED_LONG_DATA_LEN tipo di informazioni in **SQLGetInfo** era "Y" e sono stati inviati più dati per una colonna lunga (il tipo di dati è stato SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifico dell'origine dati lungo) di quello specificato nel buffer di lunghezza corrispondente a una colonna in una riga di dati che è stata aggiunta o aggiornata con **SQLBulkOperations** o aggiornata con **SQLSetPos**.|  
|22003|Valore numerico non compreso nell'intervallo|I dati inviati per un parametro o una colonna numerica associata hanno causato il troncamento dell'intera parte del numero (anziché frazionaria) quando vengono assegnati alla colonna della tabella associata.<br /><br /> La restituzione di un valore numerico (come numerico o stringa) per uno o più parametri di input/output o output avrebbe causato il troncamento dell'intera parte (anziché frazionaria).|  
|22007|Formato datetime non valido|I dati inviati per un parametro o una colonna associata a una struttura di data, ora o timestamp erano, rispettivamente, una data, un'ora o un timestamp non valido.<br /><br /> Un parametro di input/output o di output è stato associato a una struttura C di data, ora o timestamp e un valore nel parametro restituito è stato, rispettivamente, una data, un'ora o un timestamp non valido. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|22008|Overflow del campo Datetime|Un'espressione datetime calcolata per un parametro di input/output o di output ha restituito una struttura C di data, ora o timestamp non valida.|  
|22012|Divisione per zero|Un'espressione aritmetica calcolata per un parametro di input/output o di output ha restituito la divisione per zero.|  
|22015|Overflow campo intervallo|I dati inviati per una colonna o un parametro esatti numerici o di intervallo a un tipo di dati SQL a intervalli hanno causato una perdita di cifre significative.<br /><br /> I dati sono stati inviati per una colonna intervallo o un parametro con più di un campo, sono stati convertiti in un tipo di dati numerico e non hanno alcuna rappresentazione nel tipo di dati numerico.<br /><br /> I dati inviati per i dati di colonna o parametro sono stati assegnati a un tipo SQL di intervallo e non è stata stabilita alcuna rappresentazione del valore del tipo C nel tipo SQL di intervallo.<br /><br /> I dati inviati per una colonna o un parametro numerico o l'intervallo C a un tipo di intervallo C hanno causato una perdita di cifre significative.<br /><br /> I dati inviati per i dati di colonna o parametro sono stati assegnati a una struttura di intervallo C e non è stata presente alcuna rappresentazione dei dati nella struttura di dati dell'intervallo.|  
|22018|Valore di carattere non valido per la specifica del cast|Il tipo C era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo SQL della colonna era un tipo di dati carattere; e il valore nella colonna o parametro non è un valore letterale valido del tipo C associato.<br /><br /> Il tipo SQL era un numero esatto o approssimativo, un datetime o un tipo di dati interval; il tipo C è stato SQL_C_CHAR; e il valore nella colonna o parametro non è un valore letterale valido del tipo SQL associato.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|I009|Utilizzo non valido del puntatore null|(DM) l'argomento *DataPtr* era un puntatore null e l'argomento *StrLen_or_Ind* non 0, SQL_DEFAULT_PARAM o SQL_NULL_DATA.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) la chiamata di funzione precedente non era una chiamata a **SQLPutData** o **SQLParamData**.<br /><br /> (DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando è stata chiamata la funzione SQLPutData.This asynchronous function was still executing when the SQLPutData function was called.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY019|Dati non di carattere e non binari inviati in parti|**SQLPutData** è stato chiamato più di una volta per un parametro o una colonna e non è stato utilizzato per inviare dati di tipo carattere C a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati o per inviare dati C binari a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati.|  
|HY020|Tentativo di concatenare un valore Null|**SQLPutData** è stato chiamato più di una volta dopo la chiamata che ha restituito SQL_NEED_DATA e in una di queste chiamate, il *StrLen_or_Ind* argomento conteneva SQL_NULL_DATA o SQL_DEFAULT_PARAM.|  
|I090|Stringa o lunghezza del buffer non valida|L'argomento *DataPtr* non è un puntatore null e il *StrLen_or_Ind dell'argomento* era minore di 0 ma non uguale a SQL_NTS o SQL_NULL_DATA.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
 Se **SQLPutData** viene chiamato durante l'invio di dati per un parametro in un'istruzione SQL, può restituire qualsiasi SQLSTATE che può essere restituito dalla funzione chiamata per eseguire l'istruzione (**SQLExecute** o **SQLExecDirect**). Se viene chiamato durante l'invio di dati per una colonna da aggiornare o aggiunta con **SQLBulkOperations** o con **SQLSetPos**, può restituire qualsiasi SQLSTATE che può essere restituito da **SQLBulkOperations** o **SQLSetPos**.  
  
## <a name="comments"></a>Commenti  
 **SQLPutData** può essere chiamato per fornire dati dati all'esecuzione per due utilizzi: dati di parametro da utilizzare in una chiamata a **SQLExecute** o **SQLExecDirect**, o dati di colonna da utilizzare quando una riga viene aggiornata o aggiunta da una chiamata a **SQLBulkOperations** o aggiornata da una chiamata a **SQLSetPos**.  
  
 Quando un'applicazione chiama **SQLParamData** per determinare quali dati deve inviare, il driver restituisce un indicatore che l'applicazione può utilizzare per determinare i dati del parametro da inviare o dove è possibile trovare i dati della colonna. Restituisce anche SQL_NEED_DATA, che è un indicatore per l'applicazione che deve chiamare **SQLPutData** per inviare i dati. Nell'argomento *DataPtr* di **SQLPutData**, l'applicazione passa un puntatore al buffer contenente i dati effettivi per il parametro o la colonna.  
  
 Quando il driver restituisce SQL_SUCCESS per **SQLPutData**, l'applicazione chiama nuovamente **SQLParamData.** **SQLParamData** restituisce SQL_NEED_DATA se è necessario inviare più dati, nel qual caso l'applicazione chiama nuovamente **SQLPutData.SQLParamData** returns a data if more data needs to be sent, in which case the application calls SQLPutData again. Restituisce SQL_SUCCESS se tutti i dati dati di esecuzione sono stati inviati. L'applicazione chiama quindi nuovamente **SQLParamData.The** application then calls SQLParamData again. Se il driver restituisce SQL_NEED_DATA e un altro indicatore in * \*ValuePtrPtr*, richiede dati per un altro parametro o colonna e **SQLPutData** viene chiamato nuovamente. Se il driver restituisce SQL_SUCCESS, tutti i dati data-at-execution sono stati inviati e l'istruzione SQL può essere eseguita o la chiamata **SQLBulkOperations** o **SQLSetPos** può essere elaborata.  
  
 Per ulteriori informazioni su come i dati dei parametri data-at-execution vengono passati in fase di esecuzione dell'istruzione, vedere "Passaggio di valori di parametro" in [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [Invio di dati lunghi](../../../odbc/reference/develop-app/sending-long-data.md). Per ulteriori informazioni sulla modalità di aggiornamento o aggiunta dei dati delle colonne data-at-execution, vedere la sezione "Using SQLSetPos" in [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Performing Bulk Updates Using Bookmarks" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long Data e SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Un'applicazione può utilizzare **SQLPutData** per inviare dati in parti solo quando si inviano dati di tipo carattere C a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati o quando si inviano dati C binari a una colonna con un tipo di dati carattere, binario o specifico dell'origine dati. Se **SQLPutData** viene chiamato più di una volta in qualsiasi altra condizione, restituisce SQL_ERROR e SQLSTATE HY019 (dati non di caratteri e non binari inviati in parti).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente si presuppone un nome di origine dati denominato Test.The following sample assumes a data source name called Test. Il database associato deve avere una tabella che è possibile creare, come indicato di seguito:The associated database should have a table that you can create, as follows:  
  
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
|Associazione di un buffer a un parametro|[Pagina relativa alla funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Esecuzione di un'istruzione SQLExecuting an SQL statement|[Funzione SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Esecuzione di un'istruzione SQL preparataExecuting a prepared SQL statement|[Funzione SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Restituzione del parametro successivo per l'invio dei dati per|[Funzione SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
