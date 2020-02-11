---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f65c26e1c6b9588b770acf1a66409dfde8ea1072
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188682"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField può essere utilizzato per impostare i campi di descrizione per i parametri con valori di tabella e le colonne dei parametri con valori di tabella. Per informazioni sui campi disponibili, vedere [campi di descrizione dei parametri con valori di tabella](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) e [campi di descrizione per le colonne costitutive dei parametri con valori di tabella](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Osservazioni  
 Le colonne dei parametri con valori di tabella sono disponibili solo quando il campo di intestazione di descrizione SQL_SOPT_SS_PARAM_FOCUS è impostato sul numero ordinale di un record in cui SQL_DESC_TYPE è impostato su SQL_SS_TABLE. Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Se viene effettuato un tentativo di impostare SQL_SOPT_SS_PARAM_FOCUS sull'ordinale di un parametro che non è un parametro con valori di tabella, SQLSetStmtAttr restituisce SQL_ERROR e viene creato un record di diagnostica con SQLSTATE = HY024 e il messaggio "valore attributo non valido". SQL_SOPT_SS_PARAM_FOCUS non viene modificato al momento della restituzione di SQL_ERROR.  
  
 L'impostazione di SQL_SOPT_SS_PARAM_FOCUS su 0 ripristina l'accesso ai record del descrittore per i parametri.  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>Supporto di SQLSetDescField per le caratteristiche avanzate di data e ora  
 Le caratteristiche di data/ora sono state migliorate in ODBC. Per informazioni sul campo di descrizione fornito per i nuovi tipi di data/ora, vedere [Parameter and Result Metadata](../native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>Supporto di SQLSetDescField per tipi CLR definiti dall'utente di grandi dimensioni  
 SQLSetDescField supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>Supporto di SQLSetDescField per colonne di tipo sparse  
 SQLSetDecField può essere usato per impostare SQL_SOPT_SS_NAME_SCOPE nel descrittore del parametro dell'applicazione (APD) sui valori SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Per ulteriori informazioni, vedere [supporto di colonne di tipo sparse &#40;&#41;ODBC ](../native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
