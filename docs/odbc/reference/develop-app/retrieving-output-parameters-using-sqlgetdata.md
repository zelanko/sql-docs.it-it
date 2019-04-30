---
title: Recupero di parametri di Output tramite SQLGetData | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ebb09b3118c2d16041d4ca60bf738d0fda561346
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199089"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recupero di parametri di output tramite SQLGetData
Prima di ODBC 3.8, un'applicazione è stato possibile recuperare solo i parametri di output di una query con un buffer di output associata. Tuttavia, è difficile allocare un buffer molto grande quando la dimensione del valore del parametro è molto grande (ad esempio, un'immagine di grandi dimensioni). ODBC 3.8 introduce un nuovo modo per recuperare i parametri di output in parti. Un'applicazione ora è possibile chiamare **SQLGetData** con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Come avviene per il recupero dei dati di colonna di grandi dimensioni.  
  
 Per associare un parametro di output o un parametro di input/output da recuperare in parti, chiamare **SQLBindParameter** con il *InputOutputType* argomento impostato su SQL_PARAM_OUTPUT_STREAM o SQL_PARAM_INPUT_OUTPUT _STREAM. Con SQL_PARAM_INPUT_OUTPUT_STREAM, un'applicazione può utilizzare **SQLPutData** i dati di input nel parametro e quindi usare **SQLGetData** per recuperare il parametro di output. I dati di input devono essere nel data-at-execution (. DAE) del modulo usando **SQLPutData** invece l'associazione a un buffer allocato precedentemente.  
  
 Questa funzionalità può essere utilizzata dalle applicazioni ODBC 3.8 o ricompilate ODBC 3.x e ODBC 2.x applicazioni e queste applicazioni devono disporre di un driver ODBC 3.8 che supporta il recupero dei parametri di output usando **SQLGetData** e il Driver ODBC 3.8 Gestore. Per informazioni su come abilitare un'applicazione precedente usare nuove funzionalità ODBC, vedere [matrice di compatibilità](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Esempio di utilizzo  
 Ad esempio, prendere in considerazione l'esecuzione di una stored procedure, **{chiamata sp_f(?,?)}** , dove entrambi i parametri vengono associati come SQL_PARAM_OUTPUT_STREAM e la stored procedure non restituisce Nessun set di risultati (più avanti in questo argomento è possibile trovare uno scenario più complesso):  
  
1.  Per ogni parametro, chiamare **SQLBindParameter** con *InputOutputType* impostato su SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* impostata su un token, ad esempio un numero di parametro , un puntatore ai dati o un puntatore a una struttura che l'applicazione utilizza per associare i parametri di input. In questo esempio verrà utilizzato il numero ordinale del parametro come il token.  
  
2.  Eseguire la query con **SQLExecDirect** oppure **SQLExecute**. SQL_PARAM_DATA_AVAILABLE verrà restituito, che indica che sono disponibili parametri flusso di output per il recupero.  
  
3.  Chiamare **SQLParamData** per ottenere il parametro che è disponibile per il recupero. **SQLParamData** restituirà SQL_PARAM_DATA_AVAILABLE con il token del primo parametro disponibile, che viene impostato nel **SQLBindParameter** (passaggio 1). Il token viene restituito nel buffer che il *ValuePtrPtr* punta a.  
  
4.  Chiamare **SQLGetData** con l'argomento *Col*or\_*Param_Num* impostata sul parametro ordinale per recuperare i dati del primo parametro disponibile. Se **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLState 01004 (dati troncati) e il tipo è di lunghezza variabile sia il client di server, è più dati da recuperare dal primo parametro disponibile. È possibile continuare a chiamare **SQLGetData** fino a quando non viene restituito SQL_SUCCESS o SQL_SUCCESS_WITH_INFO con un diverso **SQLState**.  
  
5.  Ripetere i passaggi 3 e 4 per recuperare il parametro corrente.  
  
6.  Chiamare **SQLParamData** nuovamente. Se viene restituito nulla eccetto SQL_PARAM_DATA_AVAILABLE, non è non è più flussi di dati di parametro per il recupero e il codice restituito sarà il codice restituito dell'istruzione successiva che viene eseguita.  
  
7.  Chiamare **SQLMoreResults** per elaborare il successivo set di parametri fino a quando non viene restituito SQL_NO_DATA. **SQLMoreResults** restituirà SQL_NO_DATA in questo esempio, se l'attributo di istruzione SQL_ATTR_PARAMSET_SIZE è stata impostata su 1. In caso contrario, **SQLMoreResults** restituirà SQL_PARAM_DATA_AVAILABLE per indicare che sono disponibili parametri flusso di output per il successivo set di parametri da recuperare.  
  
 Simile a un parametro di input DAE, il token utilizzato nell'argomento *ParameterValuePtr* nelle **SQLBindParameter** (passaggio 1) può essere un puntatore che punta a una struttura di dati dell'applicazione, che contiene il ordinale del parametro e informazioni specifiche dell'applicazione, se necessario.  
  
 L'ordine del flusso di output restituito o parametri di input/output viene specifici del driver e potrebbe non essere sempre lo stesso l'ordine specificato nella query.  
  
 Se l'applicazione non chiama **SQLGetData** nel passaggio 4, viene eliminato il valore del parametro. Analogamente, se l'applicazione chiama **SQLParamData** prima di tutto di un parametro di valore è stato letto dal **SQLGetData**, viene eliminato il resto del valore e l'applicazione può elaborare quello successivo parametro.  
  
 Se l'applicazione chiama **SQLMoreResults** prima di tutto l'output inviato nel flusso di elaborazione dei parametri (**SQLParamData** continuerà a restituire SQL_PARAM_DATA_AVAILABLE), tutti i parametri rimanenti vengono ignorati. Analogamente, se l'applicazione chiama **SQLMoreResults** prima di tutto di un parametro di valore è stato letto dal **SQLGetData**, il resto del valore e tutti i parametri rimanenti viene rimossi e il applicazione può continuare a elaborare il successivo set di parametri.  
  
 Si noti che un'applicazione può specificare il tipo di dati C in entrambe **SQLBindParameter** e **SQLGetData**. Il tipo di dati C specificato con **SQLGetData** esegue l'override specificato nel tipo di dati C **SQLBindParameter**, a meno che il tipo di dati C specificato in **SQLGetData** è SQL_APD_TYPE.  
  
 Anche se un parametro di output inviati come flusso è più utile quando il tipo di dati del parametro di output è di tipo BLOB, questa funzionalità può essere usata anche con qualsiasi tipo di dati. Nel driver vengono specificati i tipi di dati supportati dai parametri di output inviati come flusso.  
  
 Se sono presenti parametri SQL_PARAM_INPUT_OUTPUT_STREAM da elaborare **SQLExecute** oppure **SQLExecDirect** , prima di tutto verrà restituito SQL_NEED_DATA. Un'applicazione può chiamare **SQLParamData** e **SQLPutData** per inviare i dati dei parametri DAE. Durante l'elaborazione, tutti i parametri di input DAE **SQLParamData** restituisce SQL_PARAM_DATA_AVAILABLE per indicare parametri flusso di output sono disponibili.  
  
 Quando vengono trasmessi parametri di output e i parametri di output associata da elaborare, il driver determina l'ordine per l'elaborazione di parametri di output. Pertanto, se un parametro di output è associato a un buffer (il **SQLBindParameter** parametro *InputOutputType* è impostato su SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT), non può essere inserito nel buffer fino alla  **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Un'applicazione deve leggere un limite solo dopo che un buffer **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO Dopotutto trasmessi in flusso i parametri di output vengono elaborati.  
  
 L'origine dati può restituire che un avviso e risultati impostate, in aggiunta al parametro del flusso di output. In generale, gli avvisi e set di risultati vengono elaborate separatamente da un parametro di output inviati come flusso tramite la chiamata **SQLMoreResults**. Gli avvisi di processo e il risultato impostato prima di elaborare il parametro di flusso di output.  
  
 Nella tabella seguente vengono descritti diversi scenari di un singolo comando inviata al server e il modo in cui l'applicazione dovrebbe funzionare.  
  
|Scenario|Valore restituito da SQLExecute o SQLExecDirect|Operazioni successive|  
|--------------|---------------------------------------------------|---------------------|  
|I dati includono solo parametri di output inviati come flusso|SQL_PARAM_DATA_AVAILABLE|Uso **SQLParamData** e **SQLGetData** per recuperare i parametri di output inviati come flusso.|  
|I dati includono un set di risultati e trasmettere i parametri di output|SQL_SUCCESS|Recuperare il set di risultati con **SQLBindCol** e **SQLGetData**.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output inviati come flusso. Deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Uso **SQLParamData** e **SQLGetData** per recuperare i parametri di output inviati come flusso.|  
|I dati includono un messaggio di avviso e trasmettere i parametri di output|SQL_SUCCESS_WITH_INFO|Uso **SQLGetDiagRec** e **SQLGetDiagField** per elaborare i messaggi di avviso.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output inviati come flusso. Deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Uso **SQLParamData** e **SQLGetData** per recuperare i parametri di output inviati come flusso.|  
|Dati includono un messaggio di avviso, set di risultati e trasmettere i parametri di output|SQL_SUCCESS_WITH_INFO|Uso **SQLGetDiagRec** e **SQLGetDiagField** per elaborare i messaggi di avviso. Quindi chiamare **SQLMoreResults** per iniziare a elaborare il risultato impostato.<br /><br /> Recuperare un set di risultati con **SQLBindCol** e **SQLGetData**.<br /><br /> Chiamare **SQLMoreResults** per avviare l'elaborazione dei parametri di output inviati come flusso. **SQLMoreResults** deve restituire SQL_PARAM_DATA_AVAILABLE.<br /><br /> Uso **SQLParamData** e **SQLGetData** per recuperare i parametri di output inviati come flusso.|  
|Parametro di query con parametri di input DAE, ad esempio, un flusso input/output (. DAE)|SQL NEED_DATA|Chiamare **SQLParamData** e **SQLPutData** DAE di inviare i dati dei parametri di input.<br /><br /> Dopo l'elaborazione, tutti i parametri di input DAE **SQLParamData** può restituire qualsiasi codice che **SQLExecute** e **SQLExecDirect** può restituire. I case in questa tabella possono quindi essere applicati.<br /><br /> Se il codice restituito è SQL_PARAM_DATA_AVAILABLE, sono disponibili parametri flusso di output. Un'applicazione deve chiamare **SQLParamData** nuovamente per recuperare il token per il parametro di output inviati come flusso, come descritto nella prima riga della tabella.<br /><br /> Se il codice restituito è SQL_SUCCESS, è un set di risultati per l'elaborazione o l'elaborazione è stata completata.<br /><br /> Se il codice restituito SQL_SUCCESS_WITH_INFO, sono presenti messaggi di avviso per l'elaborazione.|  
  
 Dopo aver **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** restituisce SQL_PARAM_DATA_AVAILABLE, un errore nella sequenza della funzione verranno generato se un'applicazione chiama un funzione che non è presente nell'elenco seguente:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (con handle di istruzione)  
  
-   **SQLFreeStmt** (con l'opzione = SQL_CLOSE, SQL_DROP o SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (con HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Le applicazioni possono usare comunque **SQLSetDescField** oppure **SQLSetDescRec** per impostare le informazioni di associazione. Mapping di campo non verranno modificate. Tuttavia, i campi all'interno di descrittore potrebbero restituire nuovi valori. Ad esempio, potrebbe restituire SQL_DESC_PARAMETER_TYPE SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Scenario di utilizzo: Recuperare un'immagine in parti da un Set di risultati  
 **SQLGetData** utilizzabile per ottenere i dati in parti quando una stored procedure restituisce un set di risultati contenente una sola riga di metadati su un'immagine e l'immagine viene restituita in un parametro di output di grandi dimensioni.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Scenario di utilizzo: Inviare e ricevere un oggetto grande come parametro di Input/Output flusso  
 **SQLGetData** utilizzabile per ottenere e inviare dati in parti quando una stored procedure ha esito positivo di un oggetto grande come parametro di input/output, il valore da e verso il database di streaming. Non è necessario archiviare tutti i dati in memoria.  
  
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
