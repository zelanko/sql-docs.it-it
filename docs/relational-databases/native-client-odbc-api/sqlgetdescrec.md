---
title: Proprietà SQLGetDescRec . Documenti Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42c8a45bb50e5fda8946cc3819aa4702f5c2fb3f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299561"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In questo argomento viene illustrata la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzionalità SQLGetDescRec specifica di Native Client.This topic discusses SQLGetDescRec functionality that is specific to Native Client.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec e parametri con valori di tabella  
 SQLGetDescRec può essere utilizzato per ottenere valori per gli attributi dei parametri con valori di tabella e delle colonne di parametri con valori di tabella. Il parametro *RecNumber* di SQLGetDescRec corrisponde al parametro *ParameterNumber* di SQLBindParameter.  
  
 Le colonne dei parametri con valori di tabella sono disponibili solo quando il campo di intestazione di descrizione SQL_SOPT_SS_PARAM_FOCUS è impostato sul numero ordinale di un record in cui SQL_DESC_TYPE è impostato su SQL_SS_TABLE. Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 SQLGetDescRec restituisce i dati seguenti:  
  
|Parametro|Parametro con valori di tabella|Colonne dei parametri con valori di tabella e altri parametri|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*Nome*|Nome di parametro formale per una chiamata alla stored procedure; in caso contrario, una stringa di lunghezza 0.|Nome della colonna di parametri con valori di tabella.|  
|*TypePtr*|SQL_DESC_TYPE. Per i parametri con valori di tabella, sarà SQL_SS_TABLE.|SQL_DESC_TYPE|  
|*SubTypePtr*|Non definito|SQL_DESC_DATETIME_INTERVAL_CODE (per i record di tipo SQL_DATETIME o SQL_INTERVAL).|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionePtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtrNullablePtr*|1|SQL_DESC_NULLABLE|  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetDescRec per le caratteristiche avanzate di data e ora  
 I valori restituiti per i tipi di data/ora sono i seguenti:  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionePtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|Data|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Per ulteriori informazioni, vedere [Miglioramenti di data e ora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>Supporto di SQLGetDescRec per tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLGetDescRec** supporta tipi CLR definiti dall'utente (UDT) di grandi dimensioni. Per ulteriori informazioni, vedere [Tipi CLR di grandi dimensioni definiti dall'utente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [OGGETTO SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
