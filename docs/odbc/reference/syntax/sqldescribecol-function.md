---
title: Funzione SQLDescribeCol | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b8453d76dc2af0499dc8d8af2ca1ec3024aee83
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523815"
---
# <a name="sqldescribecol-function"></a>Funzione SQLDescribeCol 
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLDescribeCol** restituisce il descrittore del risultato - nome della colonna, tipo, dimensione della colonna, cifre decimali e supporto di valori null - per una colonna nel set di risultati. Queste informazioni sono anche disponibili nei campi di implementazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
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
 [Input] Handle di istruzione.  
  
 *ColumnNumber*  
 [Input] Numero di colonna di dati del risultato, ordinati in sequenza in ordine crescente di colonna, a partire da 1. Il *ColumnNumber* argomento può inoltre essere impostato su 0 per descrivere la colonna del segnalibro.  
  
 *ColumnName*  
 [Output] Puntatore a un buffer con terminazione null in cui restituire il nome della colonna. Questo valore viene letto dal campo SQL_DESC_NAME di implementazione. Se la colonna è senza nome o non è possibile determinare il nome della colonna, il driver restituisce una stringa vuota.  
  
 Se *ColumnName* sia impostato su NULL *NameLengthPtr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *ColumnName*.  
  
 *BufferLength*  
 [Input] Lunghezza di **ColumnName* buffer, in caratteri.  
  
 *NameLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (ad eccezione di terminazione null) disponibili per restituire \* *ColumnName*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength*, il nome della colonna in \* *ColumnName* viene troncato a *BufferLength*meno la lunghezza di un carattere di terminazione null.  
  
 *DataTypePtr*  
 [Output] Puntatore a un buffer in cui restituire il tipo di dati SQL della colonna. Questo valore viene letto dal campo SQL_DESC_CONCISE_TYPE di implementazione. Questo sarà uno dei valori in [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md), o un tipo di dati specifici del driver SQL. Se non è possibile determinare il tipo di dati, il driver restituisce SQL_UNKNOWN_TYPE.  
  
 In ODBC 3. *x*, viene restituito SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP in  *\*DataTypePtr* per data, ora o dati di tipo timestamp, rispettivamente; in ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP viene restituito. Gestione Driver esegue il mapping richiesto quando un ODBC 2. *x* applicazione funziona con un'applicazione ODBC 3. *x* driver o quando un'applicazione ODBC 3. *x* applicazione funziona con un'API ODBC 2. *x* driver.  
  
 Quando *ColumnNumber* è uguale a 0 (per una colonna del segnalibro), viene restituito SQL_BINARY nel  *\*DataTypePtr* per i segnalibri di lunghezza variabile. (SQL_INTEGER viene restituito se i segnalibri vengono utilizzati da un'applicazione ODBC 3. *x* funziona con un'API ODBC 2. *x* driver o da un'API ODBC 2. *x* funziona con un'applicazione ODBC 3. *x* driver.)  
  
 Per altre informazioni su questi tipi di dati, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'appendice d: Tipi di dati. Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.  
  
 *ColumnSizePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire le dimensioni (in caratteri) della colonna nell'origine dati. Se non è possibile determinare la dimensione della colonna, il driver restituisce 0. Per altre informazioni sulle dimensioni di colonna, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.  
  
 *DecimalDigitsPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero di cifre decimali della colonna nell'origine dati. Se il numero di cifre decimali non può essere determinato o non è applicabile, il driver restituisce 0. Per altre informazioni su cifre decimali, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.  
  
 *NullablePtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire un valore che indica se la colonna ammette valori NULL. Questo valore viene letto dal campo SQL_DESC_NULLABLE di implementazione. I possibili valori sono i seguenti:  
  
 SQL_NO_NULLS: La colonna non ammette valori NULL.  
  
 SQL_NULLABLE: La colonna ammette valori NULL.  
  
 SQL_NULLABLE_UNKNOWN: Il driver non è possibile determinare se la colonna ammette valori NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDescribeCol** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType*SQL_HANDLE_STMT e una *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLDescribeCol** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *ColumnName* non sia abbastanza grande per restituire il nome dell'intera colonna, in modo che il nome della colonna sono stato troncato. Viene restituita la lunghezza del nome della colonna non troncato **NameLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07005|Istruzione preparata non un *specifica di cursore.*|L'istruzione associata la *StatementHandle* non ha restituito un set di risultati. Si sono verificati Nessuna colonna per descrivere.|  
|07009|Indice del descrittore non valido|(DM) il valore specificato per l'argomento *ColumnNumber* era uguale a 0 e l'opzione dell'istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_OFF.<br /><br /> Il valore specificato per l'argomento *ColumnNumber* era maggiore del numero di colonne nel set di risultati.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione di memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** oppure **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando **SQLDescribeCol** è stato chiamato.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) a cui è stata chiamata prima di chiamare la funzione **SQLPrepare**, **SQLExecute**, o una funzione di catalogo dell'handle di istruzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength* era minore di 0.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
 **SQLDescribeCol** può restituire qualsiasi valore SQLSTATE che può essere restituiti da **SQLPrepare** oppure **SQLExecute** quando viene chiamato dopo **SQLPrepare** e prima **SQLExecute**, a seconda di quando l'origine dati viene valutata l'istruzione SQL associata all'handle di istruzione.  
  
 Per motivi di prestazioni, un'applicazione non deve chiamare **SQLDescribeCol** prima di eseguire un'istruzione.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere **SQLDescribeCol** dopo una chiamata a **SQLPrepare** e prima o dopo la chiamata a associata **SQLExecute**. Un'applicazione può anche chiamare **SQLDescribeCol** dopo una chiamata a **SQLExecDirect**. Per altre informazioni, vedere [metadati dei Set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera il nome della colonna, tipo e lunghezza generato da un **selezionare** istruzione. Se la colonna è un'espressione **ColumnName* è una stringa vuota o un nome definito dal driver.  
  
> [!NOTE]  
>  ODBC supporta SQL_NULLABLE_UNKNOWN come un'estensione, anche se la specifica Open Group e gruppo di accesso SQL chiamare a livello di interfaccia non specifica l'opzione **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Annullare l'elaborazione di istruzione|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Restituzione di informazioni relative a una colonna in un set di risultati|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Il recupero di più righe di dati|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Colonne del set di restituzione del numero di risultati|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparazione di un'istruzione per l'esecuzione|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
