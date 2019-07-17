---
title: Mapping di SQLError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f24a305c2f22ef4cfacbbe4bcbcf498eab648f1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064470"
---
# <a name="sqlerror-mapping"></a>Mapping di SQLError
Quando un'applicazione chiama **SQLError** tramite un database ODBC *3.x* driver, la chiamata a  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 viene eseguito il mapping a  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 con il *HandleType* impostata sul valore SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT, come necessario, argomento e il *gestire* argomento impostato sul valore in *henv*, *hdbc*, o *hstmt*, nel modo appropriato. Il *RecNumber* argomento è determinato da Gestione Driver.
