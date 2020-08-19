---
description: Mapping di SQLAllocStmt
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8307dce9e95c98ff92912517d5b574883d6298c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424923"
---
# <a name="sqlallocstmt-mapping"></a>Mapping di SQLAllocStmt
Quando un'applicazione chiama **SQLAllocStmt** tramite un driver ODBC *3. x* , la chiamata a:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 viene mappato a **SQLAllocHandle** da Gestione driver nel driver come indicato di seguito:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 con *InputHandle puntare* impostato su *HDBC* e *OutputHandlePtr* impostato su *phstmt*.
