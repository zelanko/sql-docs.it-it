---
description: Mapping di SQLSetParam
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2c16f942920b5fefff664cc647f4edfc9ab6d13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339297"
---
# <a name="sqlsetparam-mapping"></a>Mapping di SQLSetParam
**SQLSetParam** continua a essere mappato su **SQLBINDPARAMETER** come in ODBC 2. *x*. Anche se concettualmente è simile a **SQLBindParam**, gestione driver non esegue il mapping di **SQLSetParam** a **SQLBindParam**. Questo è dovuto a un certo ODBC 2 esistente. i driver *x* utilizzano il valore speciale di *bufferLength* (SQL_SETPARAM_VALUE_MAX) generato da Gestione driver quando esegue il mapping di **SQLSetParam** su **SQLBindParameter** per determinare quando viene chiamato da 1. applicazione ODBC *x* .  
  
 Una chiamata a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 comporterà quanto segue:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
