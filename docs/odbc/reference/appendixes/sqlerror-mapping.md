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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064470"
---
# <a name="sqlerror-mapping"></a>Mapping di SQLError
Quando un'applicazione chiama **SQLError** attraverso un driver ODBC *3. x* , la chiamata a  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 viene mappato a  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 con l'argomento *HandleType* impostato sul valore SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT, in base alle esigenze, e l'argomento *handle* impostato sul valore in *HENV*, *HDBC*o *HSTMT*, a seconda dei casi. L'argomento *RecNumber* è determinato da Gestione driver.
