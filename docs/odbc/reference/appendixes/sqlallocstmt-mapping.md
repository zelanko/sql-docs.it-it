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
manager: craigg
ms.openlocfilehash: 1139d87d9f97a3d63236c03e7cf4ced787ad8e85
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793555"
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
