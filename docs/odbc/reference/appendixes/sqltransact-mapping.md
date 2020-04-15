---
title: Mapping di SQLTransact - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304882"
---
# <a name="sqltransact-mapping"></a>Mapping di SQLTransact
**SQLTransact** è ora sostituito da **SQLEndTran**. La differenza principale tra le due funzioni consiste nel fatto che **SQLEndTran** contiene un argomento *HandleType*, che specifica l'ambito del lavoro da eseguire. Il *HandleType* argomento può specificare l'ambiente o l'handle di connessione. La chiamata seguente a **SQLTransact:**  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 è mappato a  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 se *ConnectionHandle* non è uguale a SQL_NULL_HDBC. L'argomento *ConnectionHandle* è impostato sul valore di *hdbc*.  
  
 **SQL_Transact** è mappato a  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 se *ConnectionHandle* è uguale a SQL_NULL_HDBC. L'argomento *EnvironmentHandle* è impostato sul valore di *henv*.  
  
 In entrambi i casi precedenti, l'argomento *CompletionType* è impostato sullo stesso valore di *fType*.
