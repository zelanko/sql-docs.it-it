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
ms.openlocfilehash: 6b12c5286522bd0f1f8fbb40f101302aaa481cb8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792596"
---
# <a name="sqlfreestmt-mapping"></a>Mapping di SQLFreeStmt
Quando un'applicazione chiama **SQLFreeStmt** con un *opzione* argomento di SQL_DROP tramite un database ODBC *3.x* driver, la chiamata a  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 viene eseguito il mapping a  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 con il *gestiscono* impostata sul valore nell'argomento *hstmt*.
