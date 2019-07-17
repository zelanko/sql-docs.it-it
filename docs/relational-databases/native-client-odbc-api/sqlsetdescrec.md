---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bf490626d54bb041854497ae1bbad1487c669430
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131081"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Questo argomento vengono illustrate funzionalità SQLSetDescRec specifico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec e parametri con valori di tabella  
 SQLSetDescRec può essere utilizzato per impostare i campi di descrizione per i parametri con valori di tabella e le colonne dei parametri con valori di tabella. Le colonne dei parametri con valori di tabella sono disponibili solo quando il campo di intestazione di descrizione SQL_SOPT_SS_PARAM_FOCUS è impostato sul numero ordinale di un record in cui SQL_DESC_TYPE è impostato su SQL_SS_TABLE. Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Nella tabella seguente viene descritto il mapping tra parametri e campi di descrizione.  
  
|Parametro|Attributo correlato per i tipi di parametro non-con valori di tabella, incluse le colonne dei parametri con valori di tabella|Attributo correlato per i parametri con valori di tabella|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Tipo*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*SubType*|Ignorato|Per i record di tipo SQL_DATETIME o SQL_INTERVAL, impostare su SQL_DESC_DATETIME_INTERVAL_CODE.|  
|*Lunghezza*|SQL_DESC_OCTET_LENGTH|Lunghezza del nome del tipo di parametro con valori di tabella. Può essere SQL_NTS, se il nome del tipo è con terminazione Null oppure zero se il nome del tipo di parametro con valori di tabella non è obbligatorio.|  
|*Precisione*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Scala*|SQL_DESC_SCALE|Non utilizzato. Questo parametro deve essere zero.|  
|*DataPtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> Questo parametro è facoltativo per le chiamate di stored procedure ed è possibile specificare NULL se non è obbligatorio. È necessario specificarlo per istruzioni SQL che non sono chiamate di procedure.<br /><br /> *DataPtr* funge anche da un valore univoco che l'applicazione può usare per identificare il parametro con valori di tabella quando viene utilizzata l'associazione variabile di righe.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Per un parametro con valori di tabella, è il numero di righe da trasferire o SQL_DATA_AT_EXEC.SQL_DATA_AT_EXEC. Questo è un puntatore a un valore che contiene il numero di righe da trasferire con SQLExecDirect.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>Supporto di SQLSetDescRec per le caratteristiche avanzate di data e ora  
 I valori consentiti per i tipi di data/ora sono i seguenti:  
  
||*Tipo*|*SubType*|*Lunghezza*|*Precisione*|*Scala*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>Supporto di SQLSetDescRec per tipi definiti dall'utente CLR di grandi dimensioni  
 **SQLSetDescRec** supporta grandi CLR tipi definiti dall'utente (UDT). Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
