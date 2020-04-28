---
title: Informazioni su ODBC a 64 bit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ed9851ce-44ee-4c8e-b626-1d0b52da30fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9cb8e3fc42d0ad71ac83f1432c165f243f39012
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298301"
---
# <a name="odbc-64-bit-information"></a>Informazioni su ODBC a 64 bit
A partire da Windows Server 2003, i sistemi operativi Microsoft supportano le librerie ODBC a 64 bit. Le intestazioni e le librerie ODBC fornite inizialmente con MDAC 2,7 SDK contengono modifiche per consentire ai programmatori di scrivere facilmente codice per le nuove piattaforme a 64 bit. Assicurandosi che il codice usi i tipi definiti da ODBC elencati di seguito, è possibile compilare lo stesso codice sorgente per le piattaforme a 64 bit e a 32 bit basate sulle macro **_WIN64** o **Win32** .  
  
 Esistono diversi aspetti da tenere presenti durante la programmazione per un processore a 64 bit:  
  
-   Anche se la dimensione di un puntatore è cambiata da 4 byte a 8 byte, i valori integer e Long sono ancora di 4 byte. I tipi **Int64** e **UInt64** sono stati definiti per interi a 8 byte. I nuovi tipi ODBC **SQLLEN** e **SQLULEN** vengono definiti nel file di intestazione ODBC come **Int64** e **UInt64** quando **_WIN64** è stato definito.  
  
-   Diverse funzioni in ODBC sono dichiarate come accettando un parametro puntatore. In ODBC a 32 bit, i parametri definiti come puntatori venivano spesso utilizzati per passare un valore integer o un puntatore a un buffer a seconda del contesto della chiamata. Naturalmente, ciò è possibile a causa del fatto che i puntatori e i numeri interi hanno le stesse dimensioni. In Windows a 64 bit, questo non è il caso.  
  
-   Alcune funzioni ODBC precedentemente definite con i parametri **SQLINTEGER** e **SQLUINTEGER** sono state modificate laddove appropriato per l'utilizzo dei nuovi typedef **SQLLEN** e **SQLULEN** . Queste modifiche sono elencate nella sezione successiva, le dichiarazioni di funzione cambiano.  
  
-   Alcuni dei campi del descrittore che possono essere impostati tramite le varie funzioni **sqlset** e **SQLGET** sono stati modificati in modo da contenere i valori a 64 bit, mentre altri sono ancora valori a 32 bit. Assicurarsi di usare la variabile di dimensioni appropriate durante l'impostazione e il recupero di questi campi. Le specifiche dei campi di descrizione modificati sono elencate in modifiche alle dichiarazioni di funzione.  
  
## <a name="function-declaration-changes"></a>Modifiche della dichiarazione di funzione  
 Le firme di funzione seguenti sono state modificate per la programmazione a 64 bit. Gli elementi del testo in grassetto sono parametri specifici diversi.  
  
```cpp
SQLBindCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,   SQLLEN * StrLen_or_Ind);  
  
SQLBindParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,  
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN *StrLen_or_Ind);  
  
SQLBindParameter (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT InputOutputType, SQLSMALLINT ValueType,   
   SQLSMALLINT ParameterType, SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN BufferLength, SQLLEN *StrLen_or_IndPtr);  
  
SQLColAttribute (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
    SQLUSMALLINT FieldIdentifier, SQLPOINTER CharacterAttributePtr,   
   SQLSMALLINT BufferLength, SQLSMALLINT * StringLengthPtr,   
   SQLLEN* NumericAttributePtr)  
  
SQLColAttributes (SQLHSTMT hstmt, SQLUSMALLINT icol,   
   SQLUSMALLINT fDescType, SQLPOINTER rgbDesc,   
   SQLSMALLINT cbDescMax, SQLSMALLINT *pcbDesc, SQLLEN * pfDesc);  
  
SQLDescribeCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLCHAR *ColumnName, SQLSMALLINT BufferLength,   
   SQLSMALLINT *NameLengthPtr, SQLSMALLINT *DataTypePtr, SQLULEN *ColumnSizePtr,   
   SQLSMALLINT *DecimalDigitsPtr, SQLSMALLINT *NullablePtr);  
  
SQLDescribeParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT *DataTypePtr, SQLULEN *ParameterSizePtr, SQLSMALLINT *DecimalDigitsPtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLExtendedFetch(SQLHSTMT StatementHandle, SQLUSMALLINT FetchOrientation, SQLLEN FetchOffset,   
   SQLULEN * RowCountPtr, SQLUSMALLINT * RowStatusArray);  
  
SQLFetchScroll (SQLHSTMT StatementHandle, SQLSMALLINT FetchOrientation,   
   SQLLEN FetchOffset);  
  
SQLGetData (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,    SQLLEN *StrLen_or_Ind);  
  
SQLGetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLCHAR *Name, SQLSMALLINT BufferLength,   
   SQLSMALLINT *StringLengthPtr, SQLSMALLINT *TypePtr,   
   SQLSMALLINT *SubTypePtr, SQLLEN *LengthPtr,   
   SQLSMALLINT *PrecisionPtr, SQLSMALLINT *ScalePtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLParamOptions(SQLHSTMT hstmt, SQLULEN crow, SQLULEN * pirow);  
  
SQLPutData (SQLHSTMT StatementHandle, SQLPOINTER DataPtr,   
   SQLLEN StrLen_or_Ind);  
  
SQLRowCount (SQLHSTMT StatementHandle, SQLLEN* RowCountPtr);  
  
SQLSetConnectOption(SQLHDBC ConnectHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
  
SQLSetPos (SQLHSTMT StatementHandle, SQLSETPOSIROW RowNumber, SQLUSMALLINT Operation,  
   SQLUSMALLINT LockType);  
  
SQLSetParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN LengthPrecision, SQLSMALLINT ParameterScale,   
   SQLPOINTER ParameterValue, SQLLEN *StrLen_or_Ind);  
  
SQLSetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLSMALLINT Type, SQLSMALLINT SubType, SQLLEN Length,   
   SQLSMALLINT Precision, SQLSMALLINT Scale, SQLPOINTER DataPtr,   
   SQLLEN *StringLengthPtr, SQLLEN *IndicatorPtr);  
  
SQLSetScrollOptions (SQLHSTMT hstmt, SQLUSMALLINT fConcurrency,   
   SQLLEN crowKeyset, SQLUSMALLINT crowRowset);  
  
SQLSetStmtOption (SQLHSTMT StatementHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
```  
  
## <a name="changes-in-sql-data-types"></a>Modifiche nei tipi di dati SQL  
 I quattro tipi SQL seguenti sono ancora supportati solo a 32 bit. non sono definiti per i compilatori a 64 bit. Questi tipi non vengono più utilizzati per i parametri in MDAC 2,7; l'uso di questi tipi provocherà errori del compilatore sulle piattaforme a 64 bit.  
  
```cpp
#ifdef WIN32   
typedef SQLULEN SQLROWCOUNT;   
typedef SQLULEN SQLROWSETSIZE;   
typedef SQLULEN SQLTRANSID;   
typedef SQLLEN SQLROWOFFSET;   
#endif  
```  
  
 La definizione di SQLSETPOSIROW è cambiata per i compilatori a 32 bit e a 64 bit:  
  
```cpp
#ifdef _WIN64   
typedef UINT64 SQLSETPOSIROW;   
#else   
#define SQLSETPOSIROW SQLUSMALLINT   
#endif  
```  
  
 Le definizioni di SQLLEN e SQLULEN sono state modificate per i compilatori a 64 bit:  
  
```cpp
#ifdef _WIN64   
typedef INT64 SQLLEN;   
typedef UINT64 SQLULEN;   
#else   
#define SQLLEN SQLINTEGER   
#define SQLULEN SQLUINTEGER   
#endif  
```  
  
 Sebbene SQL_C_BOOKMARK sia deprecato in ODBC 3,0, per i compilatori a 64 bit nei client 2,0, questo valore è stato modificato:  
  
```cpp
#ifdef _WIN64   
#define SQL_C_BOOKMARK SQL_C_UBIGINT   
#else   
#define SQL_C_BOOKMARK SQL_C_ULONG   
#endif  
```  
  
 Il tipo di SEGNALIBRo è definito in modo diverso nelle intestazioni più recenti:  
  
```cpp
typedef SQLULEN BOOKMARK;  
```  
  
## <a name="values-returned-from-odbc-api-calls-through-pointers"></a>Valori restituiti dalle chiamate API ODBC tramite puntatori  
 Le chiamate di funzione ODBC seguenti accettano come parametro di input un puntatore a un buffer in cui i dati vengono restituiti dal driver. Il contesto e il significato dei dati restituiti sono determinati da altri parametri di input per le funzioni. In alcuni casi, questi metodi possono ora restituire valori a 64 bit (interi a 8 byte) anziché i tipici valori interi a 32 bit (4 byte). Questi casi sono i seguenti:  
  
 **SQLColAttribute**  
  
 Quando il parametro *FieldIdentifier* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **NumericAttribute*:  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_COUNT  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_NULLABLE  
  
 SQL_DESC_NUM_PREC_RADIX  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLColAttributes**  
  
 Quando il parametro *fDescType* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **pfDesc*:  
  
 SQL_COLUMN_COUNT  
  
 SQL_COLUMN_DISPLAY_SIZE  
  
 SQL_COLUMN_LENGTH  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLGetConnectAttr**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene restituito un valore a 64 bit nel *valore*:  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetConnectOption**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene restituito un valore a 64 bit nel *valore*:  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetDescField**  
  
 Quando il parametro *FieldIdentifier* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **ValuePtr*:  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLGetDiagField**  
  
 Quando il parametro *DiagIdentifier* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **DiagInfoPtr*:  
  
 SQL_DIAG_CURSOR_ROW_COUNT  
  
 SQL_DIAG_ROW_COUNT  
  
 SQL_DIAG_ROW_NUMBER  
  
 **SQLGetInfo**  
  
 Quando il parametro *InfoType* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **InfoValuePtr*:  
  
 SQL_DRIVER_HDBC  
  
 SQL_DRIVER_HENV  
  
 SQL_DRIVER_HLIB  
  
 Quando *InfoType* ha uno dei due valori seguenti **InfoValuePtr* è 64 bit sia per l'input che per l'output:  
  
 SQL_DRIVER_HDESC  
  
 SQL_DRIVER_HSTMT  
  
 **SQLGetStmtAttr**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **ValuePtr*:  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLGetStmtOption**  
  
 Quando il parametro *Option* ha uno dei valori seguenti, viene restituito un valore a 64 bit in **value*:  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
 **SQLSetConnectAttr**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene passato un *valore a 64 bit:*  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetConnectOption**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene passato un *valore a 64 bit:*  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetDescField**  
  
 Quando il parametro *FieldIdentifier* ha uno dei valori seguenti, viene passato un valore a 64 bit in *ValuePtr*:  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLSetStmtAttr**  
  
 Quando il parametro *attribute* ha uno dei valori seguenti, viene passato un valore a 64 bit in *ValuePtr*:  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLSetStmtOption**  
  
 Quando il parametro *Option* ha uno dei valori seguenti, viene passato un *valore a 64 bit:*  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a ODBC](../../odbc/reference/introduction-to-odbc.md)
