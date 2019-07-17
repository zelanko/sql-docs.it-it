---
title: Mapping di SQLSetParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c8d2d567f899c30dfe91cd35445956cd6214da9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125545"
---
# <a name="sqlsetparam-mapping"></a>Mapping di SQLSetParam
**SQLSetParam** continua a eseguire il mapping in cima **SQLBindParameter** Analogamente ODBC 2. *x*. Anche se è concettualmente simile a **SQLBindParam**, gestione Driver non esegue il mapping **SQLSetParam** al **SQLBindParam**. Determinati esistente ODBC 2. *x* driver viene utilizzato il valore speciale *BufferLength* (SQL_SETPARAM_VALUE_MAX) che genera l'errore gestione Driver quando si esegue il mapping **SQLSetParam** nella parte superiore della  **SQLBindParameter** per determinare quando viene chiamato da 1. *x* applicazione ODBC.  
  
 Una chiamata a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 restituirà quanto segue:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
