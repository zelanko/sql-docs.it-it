---
title: 'Mapping di SQLSetParam : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300531"
---
# <a name="sqlsetparam-mapping"></a>Mapping di SQLSetParam
**SQLSetParam** continua a essere mappato su **SQLBindParameter** come in ODBC 2. *x*. Anche se è concettualmente simile a **SQLBindParam**, Gestione Driver non esegue il mapping di **SQLSetParam** a **SQLBindParam**. Ciò è dovuto al fatto che alcuni ODBC 2 esistenti. *x* driver utilizzano il valore speciale di *BufferLength* (SQL_SETPARAM_VALUE_MAX) che il Driver Manager genera quando esegue il mapping di **SQLSetParam** su **SQLBindParameter** per determinare quando viene chiamato da un 1. *x* Applicazione ODBC.  
  
 Una chiamata a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 si tradurrà in quanto segue:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
