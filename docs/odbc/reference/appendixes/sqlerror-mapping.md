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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa3b66b29af755099cb273f3a19ca4e8230cd0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302077"
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
