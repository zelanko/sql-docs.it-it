---
title: Mapping di SQLAllocEnv | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afbd1404cb40408166ecfc59993db7b183ae5ed2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065012"
---
# <a name="sqlallocenv-mapping"></a>Mapping di SQLAllocEnv
Quando un'applicazione chiama **SQLAllocEnv** tramite un database ODBC *3.x* driver, la chiamata al **SQLAllocEnv**(*phenv*) viene mappato a **SQLAllocHandle** come indicato di seguito:  
  
1.  Gestione Driver alloca un handle di ambiente e lo restituisce all'applicazione. Le chiamate di gestione Driver **SQLSetEnvAttr** su cui impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2.  
  
2.  Quando l'applicazione stabilisce la prima connessione a un driver, viene chiamato gestione Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     nel driver con *OutputHandlePtr* impostata su *phenv*.
