---
title: Recupero di parametri di output tramite SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eeb8fae9c563e675499dec47839acdd0a003765a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020507"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recupero di parametri di output tramite SQLGetData
Prima di ODBC 3,8, un'applicazione poteva recuperare solo i parametri di output di una query con un buffer di output associato. Tuttavia, è difficile allocare un buffer di dimensioni molto grandi quando la dimensione del valore del parametro è molto grande, ad esempio un'immagine di grandi dimensioni. ODBC 3,8 introduce un nuovo modo per recuperare i parametri di output in parti. Un'applicazione ora può chiamare **SQLGetData** con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Questa operazione è simile al recupero di dati di colonna di grandi dimensioni.  
  
 Per associare un parametro di output o un parametro di input/output da recuperare in parti, chiamare **SQLBindParameter** con l'argomento *InputOutputType* impostato su SQL_PARAM_OUTPUT_STREAM o SQL_PARAM_INPUT_OUTPUT_STREAM. Con SQL_PARAM_INPUT_OUTPUT_STREAM, un'applicazione può utilizzare **SQLPutData** per inserire i dati nel parametro, quindi utilizzare **SQLGetData** per recuperare il parametro di output. I dati di input devono essere nel form data-at-execution (DAE), usando **SQLPutData** anziché associarlo a un buffer preallocato.  
  
 Questa funzionalità può essere utilizzata da applicazioni ODBC 3,8 o da applicazioni ODBC 3. x e ODBC 2. x ricompilate e tali applicazioni devono disporre di un driver ODBC 3,8 che supporta il recupero di parametri di output tramite **SQLGetData** e ODBC 3,8 driver Manager. Per informazioni su come consentire a un'applicazione precedente di utilizzare le nuove funzionalità ODBC, vedere [Compatibility Matrix](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Esempio di utilizzo  
 Si consideri, ad esempio, l'esecuzione di un stored procedure, **{CALL sp_f (?,?)}**, in cui entrambi i parametri sono associati come SQL_PARAM_OUTPUT_STREAM e il stored procedure non restituisce alcun set di risultati. più avanti in questo argomento si troverà uno scenario più complesso:  
  
1.  Per ogni parametro, chiamare **SQLBindParameter** con *InputOutputType* impostato su SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* impostato su un token, ad esempio un numero di parametro, un puntatore ai dati o un puntatore a una struttura che l'applicazione utilizza per associare i parametri di input. Questo esempio userà il parametro ordinale come token.  
  
2.  Eseguire la query con **SQLExecDirect** o **SQLExecute**. Verrà restituito SQL_PARAM_DATA_AVAILABLE, a indicare che sono disponibili parametri di output trasmessi per il recupero.  
  
3.  Chiamare **SQLParamData** per ottenere il parametro disponibile per il recupero. **SQLParamData** restituirà SQL_PARAM_DATA_AVAILABLE con il token del primo parametro disponibile, impostato in **SQLBindParameter** (passaggio 1). Il token viene restituito nel buffer a cui punta *ValuePtrPtr* .  
  
4.  Chiamare **SQLGetData** con l'argomento *col*_or\_*Param_Num* impostato sull'ordinale del parametro per recuperare i dati del primo parametro disponibile. Se **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati troncati) e il tipo è a lunghezza variabile nel client e nel server, è necessario recuperare più dati dal primo parametro disponibile. È possibile continuare a chiamare **SQLGetData** fino a quando non restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO con un valore **SQLSTATE**diverso.  
  
5.  Ripetere il passaggio 3 e il passaggio 4 per recuperare il parametro corrente.  
  
6.  Chiamare nuovamente **SQLParamData** . Se restituisce qualcosa ad eccezione di SQL_PARAM_DATA_AVAILABLE, non sono presenti altri dati di parametro trasmessi da recuperare e il codice restituito sarà il codice restituito dell'istruzione successiva eseguita.  
  
7.  Chiamare **SQLMoreResults** per elaborare il set di parametri successivo fino a quando non viene restituito SQL_NO_DATA. **SQLMoreResults** restituirà SQL_NO_DATA in questo esempio se l'attributo Statement SQL_ATTR_PARAMSET_SIZE è stato impostato su 1. In caso contrario, **SQLMoreResults** restituirà SQL_PARAM_DATA_AVAILABLE per indicare che sono disponibili parametri di output trasmessi per il set di parametri successivo da recuperare.  
  
 Analogamente a un parametro di input DAE, il token usato nell'argomento *ParameterValuePtr* in **SQLBindParameter** (passaggio 1) può essere un puntatore che punta a una struttura di dati dell'applicazione, che contiene il numero ordinale del parametro e altre informazioni specifiche dell'applicazione, se necessario.  
  
 L'ordine dei parametri restituiti di output o di input/output trasmessi è specifico del driver e potrebbe non essere sempre uguale all'ordine specificato nella query.  
  
 Se l'applicazione non chiama **SQLGetData** nel passaggio 4, il valore del parametro viene ignorato. Analogamente, se l'applicazione chiama **SQLParamData** prima che tutti i valori di un parametro siano stati letti da **SQLGetData**, il resto del valore viene ignorato e l'applicazione può elaborare il parametro successivo.  
  
 Se l'applicazione chiama **SQLMoreResults** prima dell'elaborazione di tutti i parametri di output trasmessi (**SQLParamData** restituisce comunque SQL_PARAM_DATA_AVAILABLE), tutti i parametri rimanenti vengono eliminati. Analogamente, se l'applicazione chiama **SQLMoreResults** prima che tutti i valori di un parametro siano stati letti da **SQLGetData**, il resto del valore e tutti i parametri rimanenti vengono eliminati e l'applicazione può continuare a elaborare il set di parametri successivo.  
  
 Si noti che un'applicazione può specificare il tipo di dati C sia in **SQLBindParameter** che in **SQLGetData**. Il tipo di dati C specificato con **SQLGetData** sostituisce il tipo di dati c specificato in **SQLBindParameter**, a meno che non sia SQL_APD_TYPE il tipo di dati c specificato in **SQLGetData** .  
  
 Anche se un parametro di output trasmesso è più utile quando il tipo di dati del parametro di output è di tipo BLOB, questa funzionalità può essere usata anche con qualsiasi tipo di dati. I tipi di dati supportati dai parametri di output trasmessi vengono specificati nel driver.  
  
 Se sono presenti SQL_PARAM_INPUT_OUTPUT_STREAM parametri da elaborare, **SQLExecute** o **SQLExecDirect** restituirà SQL_NEED_DATA prima. Un'applicazione può chiamare **SQLParamData** e **SQLPutData** per inviare i dati del parametro DAE. Quando vengono elaborati tutti i parametri di input DAE, **SQLParamData** restituisce SQL_PARAM_DATA_AVAILABLE per indicare che i parametri di output trasmessi sono disponibili.  
  
 Quando sono presenti parametri di output con flusso e parametri di output associati da elaborare, il driver determina l'ordine di elaborazione dei parametri di output. Quindi, se un parametro di output è associato a un buffer (il parametro **SQLBindParameter** *InputOutputType* è impostato su SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT), il buffer potrebbe non essere popolato fino a quando **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Un'applicazione deve leggere un buffer associato solo dopo che **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO dopo l'elaborazione di tutti i parametri di output trasmessi.  
  
 L'origine dati può restituire un avviso e un set di risultati, oltre al parametro di output trasmesso. In generale, gli avvisi e i set di risultati vengono elaborati separatamente da un parametro di output trasmesso tramite una chiamata a **SQLMoreResults**. Elaborare gli avvisi e il set di risultati prima di elaborare il parametro di output trasmesso.  
  
 Nella tabella seguente vengono descritti i diversi scenari di un singolo comando inviato al server e il modo in cui l'applicazione dovrebbe funzionare.  
  
|Scenario|Valore restituito da SQLExecute o SQLExecDirect|Operazioni successive|  
|--------------|---------------------------------------------------|---------------------|  
|I dati includono solo parametri di output trasmessi|SQL_PARAM_DATA_AVAILABLE|Usare **SQLParamData** e **SQLGetData** per recuperare i parametri di output trasmessi.|  
|I dati includono un set di risultati e i parametri di output trasmessi|SQL_SUCCESS|Recuperare il set di risultati con **SQLBindCol** e **SQLGetData**.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output trasmessi. Deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Usare **SQLParamData** e **SQLGetData** per recuperare i parametri di output trasmessi.|  
|I dati includono un messaggio di avviso e i parametri di output trasmessi|SQL_SUCCESS_WITH_INFO|Usare **SQLGetDiagRec** e **SQLGetDiagField** per elaborare i messaggi di avviso.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output trasmessi. Deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Usare **SQLParamData** e **SQLGetData** per recuperare i parametri di output trasmessi.|  
|I dati includono un messaggio di avviso, un set di risultati e i parametri di output trasmessi|SQL_SUCCESS_WITH_INFO|Usare **SQLGetDiagRec** e **SQLGetDiagField** per elaborare i messaggi di avviso. Chiamare quindi **SQLMoreResults** per avviare l'elaborazione del set di risultati.<br /><br /> Recuperare un set di risultati con **SQLBindCol** e **SQLGetData**.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output trasmessi. **SQLMoreResults** deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Usare **SQLParamData** e **SQLGetData** per recuperare i parametri di output trasmessi.|  
|Eseguire una query con parametri di input DAE, ad esempio un parametro di input/output (DAE) trasmesso|NEED_DATA SQL|Chiamare **SQLParamData** e **SQLPutData** per inviare i dati del parametro di input DAE.<br /><br /> Dopo l'elaborazione di tutti i parametri di input DAE, **SQLParamData** può restituire qualsiasi codice restituito che **SQLExecute** e **SQLExecDirect** può restituire. È quindi possibile applicare i case in questa tabella.<br /><br /> Se il codice restituito è SQL_PARAM_DATA_AVAILABLE, i parametri di output trasmessi sono disponibili. Un'applicazione deve chiamare nuovamente **SQLParamData** per recuperare il token per il parametro di output trasmesso, come descritto nella prima riga della tabella.<br /><br /> Se il codice restituito è SQL_SUCCESS, è disponibile un set di risultati da elaborare o l'elaborazione è stata completata.<br /><br /> Se il codice restituito è SQL_SUCCESS_WITH_INFO, sono presenti messaggi di avviso da elaborare.|  
  
 Quando **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** restituisce SQL_PARAM_DATA_AVAILABLE, viene generato un errore di sequenza di funzioni se un'applicazione chiama una funzione non presente nell'elenco seguente:  
  
-   **** / **SQLAllocHandleStd** SQLAllocHandle  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **** / **SQLGetFunctions** SQLGetInfo  
  
-   **SQLGetConnectAttr** / **** SQLGetEnvAttr / **** SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **** / **SQLGetDiagRec** SQLGetDiagField  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (con handle di istruzione)  
  
-   **SQLFreeStmt** (con Option = SQL_CLOSE, SQL_DROP o SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (with HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Le applicazioni possono comunque utilizzare **SQLSetDescField** o **SQLSetDescRec** per impostare le informazioni di binding. Il mapping dei campi non verrà modificato. Tuttavia, i campi all'interno del descrittore potrebbero restituire nuovi valori. Ad esempio, SQL_DESC_PARAMETER_TYPE potrebbe restituire SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Scenario di utilizzo: recuperare un'immagine in parti da un set di risultati  
 **SQLGetData** può essere utilizzato per ottenere i dati in parti quando un stored procedure restituisce un set di risultati contenente una riga di metadati relativi a un'immagine e l'immagine viene restituita in un parametro di output di grandi dimensioni.  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Scenario di utilizzo: inviare e ricevere un Large Object come parametro di input/output trasmesso  
 **SQLGetData** può essere utilizzato per ottenere e inviare dati in parti quando un stored procedure passa un oggetto di grandi dimensioni come parametro di input/output, in modo da trasmettere il valore da e verso il database. Non è necessario archiviare tutti i dati in memoria.  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md)
