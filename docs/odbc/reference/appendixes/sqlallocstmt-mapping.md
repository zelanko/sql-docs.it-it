---
title: Mapping di SQLAllocStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf79d3ef813e87e785cea588cfc1d6e3eed44ee4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064989"
---
# <a name="sqlallocstmt-mapping"></a>Mapping di SQLAllocStmt
Quando un'applicazione chiama **SQLAllocStmt** tramite un database ODBC *3.x* driver, la chiamata a:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 viene eseguito il mapping a **SQLAllocHandle** da Gestione Driver nel driver come indicato di seguito:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 con *InputHandle* impostata su *hdbc* e *OutputHandlePtr* impostata su *phstmt*.
