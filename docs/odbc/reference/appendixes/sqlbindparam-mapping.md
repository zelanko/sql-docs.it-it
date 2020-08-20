---
description: Mapping di SQLBindParam
title: Mapping di SQLBindParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f998fd30716e479cb4dd0650af53c5a24483f2f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456462"
---
# <a name="sqlbindparam-mapping"></a>Mapping di SQLBindParam
**SQLBindParam** non può essere effettivamente chiamato deprecato perché non era mai presente in ODBC; Tuttavia, rappresenta comunque una funzionalità duplicata, che deve essere esportata dal gestore di driver poiché le applicazioni ISO e Open Group conformi lo useranno. Poiché **SQLBindParameter** contiene tutte le funzionalità di **SQLBindParam**, verrà eseguito il mapping di **SQLBindParam** su **SQLBindParameter** (quando il driver sottostante è un driver ODBC *3. x* ). Un driver ODBC *3. x* non deve implementare **SQLBindParam**.  
  
## <a name="remarks"></a>Osservazioni  
 Quando viene effettuata la chiamata seguente a **SQLBindParam** :  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 Gestione driver chiama **SQLBindParameter** nel driver come indicato di seguito:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Vedere [informazioni su ODBC 64 bit](../../../odbc/reference/odbc-64-bit-information.md), se l'applicazione viene eseguita su un sistema operativo a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
