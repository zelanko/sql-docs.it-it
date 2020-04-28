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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d187db4d40132385b9ae4564fddbf89987e3e97
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302012"
---
# <a name="sqlfreestmt-mapping"></a>Mapping di SQLFreeStmt
Quando un'applicazione chiama **SQLFreeStmt** con un argomento *Option* di SQL_DROP tramite un driver ODBC *3. x* , la chiamata a  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 viene mappato a  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 con l'argomento *handle* impostato sul valore in *HSTMT*.
