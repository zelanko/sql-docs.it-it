---
title: Mapping di SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1872806265470327f3e7bff468be2ba6d9011421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199428"
---
# <a name="sqlfreestmt-mapping"></a>Mapping di SQLFreeStmt
Quando un'applicazione chiama **SQLFreeStmt** con un *opzione* argomento di SQL_DROP tramite un'applicazione ODBC 3*x* driver, la chiamata a  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 viene eseguito il mapping a  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 con il *gestiscono* impostata sul valore nell'argomento *hstmt*.
