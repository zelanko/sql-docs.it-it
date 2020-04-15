---
title: 'Funzione SQLDescribeCol : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301171"
---
# <a name="sqldescribecol-function"></a>Funzione SQLDescribeCol 
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLDescribeCol** restituisce il descrittore del risultato (nome della colonna, tipo, dimensione della colonna, cifre decimali e supporto di valori Null) per una colonna nel set di risultati. Queste informazioni sono disponibili anche nei campi dell'IRD.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Ingresso] Handle di istruzione.  
  
 *ColumnNumber*  
 [Ingresso] Numero di colonna dei dati dei risultati, ordinati in sequenza in ordine crescente di colonne, a partire da 1.Column number of result data, ordered in sequentially in increasing column order, starting at 1. *L'argomento ColumnNumber* può anche essere impostato su 0 per descrivere la colonna del segnalibro.  
  
 *ColumnName*  
 [Uscita] Puntatore a un buffer con terminazione null in cui restituire il nome della colonna. Questo valore viene letto dal campo SQL_DESC_NAME dell'IRD. Se la colonna è senza nome o non è possibile determinare il nome della colonna, il driver restituisce una stringa vuota.  
  
 Se *ColumnName* è NULL, *NameLengthPtr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ColumnName*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del buffer*di ColumnName,* in caratteri.  
  
 *NameLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri \*(esclusa la terminazione null) disponibile per la restituzione in *ColumnName*. Se il numero di caratteri disponibili per la restituzione è \*maggiore o uguale a *BufferLength*, il nome della colonna in *ColumnName* verrà troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
 *DataTypePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il tipo di dati SQL della colonna. Questo valore viene letto dal campo SQL_DESC_CONCISE_TYPE dell'IRD. Questo sarà uno dei valori in [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md)o un tipo di dati SQL specifico del driver. Se non è possibile determinare il tipo di dati, il driver restituisce SQL_UNKNOWN_TYPE.  
  
 In ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP viene restituito in * \*DataTypePtr* rispettivamente per i dati di data, ora o timestamp; in ODBC 2. *x*, viene restituito SQL_DATE, SQL_TIME o SQL_TIMESTAMP. Gestione Driver esegue i mapping necessari quando un ODBC 2. *l'applicazione x* funziona con un'applicazione ODBC 3. *x* o quando un ODBC 3. *l'applicazione x* funziona con un'applicazione ODBC 2. *driver x.*  
  
 Quando *ColumnNumber* è uguale a 0 (per una colonna di segnalibro), viene restituito SQL_BINARY in * \*DataTypePtr* per i segnalibri di lunghezza variabile. (SQL_INTEGER viene restituito se i segnalibri vengono utilizzati da un ODBC 3. *x* che utilizza un'applicazione ODBC 2. *x* o da un ODBC 2. *x* che utilizza un'applicazione ODBC 3. *x* driver.)  
  
 Per altre informazioni su questi tipi di dati, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: Tipi di dati. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.  
  
 *ColumnSizePtr (ColumnSizePtr)*  
 [Uscita] Puntatore a un buffer in cui restituire la dimensione (in caratteri) della colonna nell'origine dati. Se non è possibile determinare la dimensione della colonna, il driver restituisce 0. Per ulteriori informazioni sulle dimensioni delle colonne, vedere [Dimensioni colonna, Cifre decimali, Trasferimento ottetto lunghezza e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice D: tipi di dati.  
  
 *DecimalDigitsPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero di cifre decimali della colonna nell'origine dati. Se il numero di cifre decimali non può essere determinato o non è applicabile, il driver restituisce 0. Per ulteriori informazioni sulle cifre decimali, vedere [Dimensione colonna, Cifre decimali, Trasferimento ottetto lunghezza e Dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice D: tipi di dati.  
  
 *NullablePtrNullablePtr*  
 [Uscita] Puntatore a un buffer in cui restituire un valore che indica se la colonna consente valori NULL. Questo valore viene letto dal campo SQL_DESC_NULLABLE dell'IRD. I possibili valori sono i seguenti:  
  
 SQL_NO_NULLS: la colonna non consente valori NULL.  
  
 SQL_NULLABLE: la colonna consente valori NULL.  
  
 SQL_NULLABLE_UNKNOWN: il driver non è in grado di determinare se la colonna consente valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDescribeCol** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLDescribeCol** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *ColumnName* non era sufficientemente grande per restituire l'intero nome di colonna, pertanto il nome della colonna è stato troncato. La lunghezza del nome di colonna non troncato viene restituita in *, NameLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|07005|Istruzione Prepared non una specifica del *cursore*|L'istruzione associata a *StatementHandle* non ha restituito un set di risultati. Non c'erano colonne da descrivere.|  
|07009|Indice descrittore non valido|(DM) il valore specificato per l'argomento *ColumnNumber* è uguale a 0 e l'opzione dell'istruzione SQL_ATTR_USE_BOOKMARKS è stata SQL_UB_OFF.<br /><br /> Il valore specificato per l'argomento *NumeroColonna* era maggiore del numero di colonne nel set di risultati.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è riuscito prima che la funzione completasse l'elaborazione.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *il StatementHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle*. Quindi la funzione è stata chiamata nuovamente su *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima del completamento dell'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato su *StatementHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata una funzione in modo asincrono in esecuzione per l'handle di connessione associato a *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLDescribeCol** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.<br /><br /> (DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) la funzione è stata chiamata prima di chiamare **SQLPrepare**, **SQLExecute**o una funzione di catalogo sull'handle dell'istruzione .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** è stato chiamato per *StatementHandle* e ha restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dell'invio dei dati per tutti i parametri o le colonne data-at-execution.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength* è minore di 0.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver associato a *StatementHandle* non supporta la funzione.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
 **SQLDescribeCol** può restituire qualsiasi SQLSTATE che può essere restituito da **SQLPrepare** o **SQLExecute** quando viene chiamato dopo **SQLPrepare** e before **SQLExecute**, a seconda di quando l'origine dati valuta l'istruzione SQL associata all'handle dell'istruzione.  
  
 Per motivi di prestazioni, un'applicazione non deve chiamare **SQLDescribeCol** prima di eseguire un'istruzione.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere **SQLDescribeCol** dopo una chiamata a **SQLPrepare** e prima o dopo la chiamata associata a **SQLExecute**. Un'applicazione può anche chiamare **SQLDescribeCol** dopo una chiamata a **SQLExecDirect**. Per ulteriori informazioni, consultate [Metadati del set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera il nome della colonna, il tipo e la lunghezza generati da un'istruzione **SELECT.** Se la colonna è un'espressione, il nome*di colonna* è una stringa vuota o un nome definito dal driver.  
  
> [!NOTE]  
>  ODBC supporta SQL_NULLABLE_UNKNOWN come estensione, anche se la specifica Open Group e SQL Access Call Level Interface non specifica l'opzione per **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultatiBinding a buffer to a column in a result set|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullamento dell'elaborazione delle istruzioniCanceling statement processing|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni su una colonna in un set di risultatiReturning information about a column in a result set|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Recupero di più righe di dati|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Restituzione del numero di colonne del set di risultatiReturning the number of result set columns|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
