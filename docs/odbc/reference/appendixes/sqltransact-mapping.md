---
title: Mapping SQLTransact | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2082a97b24284afcc879048bb08e86a7b2bb3ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070116"
---
# <a name="sqltransact-mapping"></a>Mapping di SQLTransact
**SQLTransact** è ora sostituito da **SQLEndTran**. La differenza principale tra le due funzioni è che **SQLEndTran** contiene un argomento *HandleType*, che specifica l'ambito del lavoro da eseguire. L'argomento *HandleType* può specificare l'ambiente o l'handle di connessione. La chiamata seguente a **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 viene mappato a  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Se *connectionHandle* è diverso da SQL_NULL_HDBC. L'argomento *connectionHandle* è impostato sul valore di *HDBC*.  
  
 **SQL_Transact** è mappato a  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Se *connectionHandle* è uguale a SQL_NULL_HDBC. L'argomento *EnvironmentHandle* è impostato sul valore di *HENV*.  
  
 In entrambi i casi precedenti, l'argomento *CompletionType* è impostato sullo stesso valore di *ftype*.
