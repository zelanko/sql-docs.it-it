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
manager: craigg
ms.openlocfilehash: c5d420bc68c4704705018a37c6459181481b1d7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297466"
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
