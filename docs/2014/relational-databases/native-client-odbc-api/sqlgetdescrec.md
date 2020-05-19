---
title: SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f3a2bbebc947d0c245e00c39fca2d4e69fbb5666
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706039"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
  In questo argomento vengono illustrate le funzionalità di SQLGetDescRec specifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec e parametri con valori di tabella  
 SQLGetDescRec può essere utilizzato per ottenere i valori per gli attributi dei parametri con valori di tabella e delle colonne dei parametri con valori di tabella. Il parametro *RecNumber* di SQLGetDescRec corrisponde al parametro *ParameterNumber* di SQLBindParameter.  
  
 Le colonne dei parametri con valori di tabella sono disponibili solo quando il campo di intestazione di descrizione SQL_SOPT_SS_PARAM_FOCUS è impostato sul numero ordinale di un record in cui SQL_DESC_TYPE è impostato su SQL_SS_TABLE. Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS about, vedere [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 SQLGetDescRec restituisce i dati seguenti:  
  
|Parametro|Parametro con valori di tabella|Colonne dei parametri con valori di tabella e altri parametri|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*Nome*|Nome di parametro formale per una chiamata alla stored procedure; in caso contrario, una stringa di lunghezza 0.|Nome della colonna di parametri con valori di tabella.|  
|*TypePtr*|SQL_DESC_TYPE. Per i parametri con valori di tabella, sarà SQL_SS_TABLE.|SQL_DESC_TYPE|  
|*SubTypePtr*|Non definito|SQL_DESC_DATETIME_INTERVAL_CODE (per i record di tipo SQL_DATETIME o SQL_INTERVAL).|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetDescRec per le caratteristiche avanzate di data e ora  
 I valori restituiti per i tipi di data/ora sono i seguenti:  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|data|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>Supporto di SQLGetDescRec per tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLGetDescRec` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
