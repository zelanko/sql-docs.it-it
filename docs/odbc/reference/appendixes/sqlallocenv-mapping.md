---
title: 'Mapping di SQLAllocEnv : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304042"
---
# <a name="sqlallocenv-mapping"></a>Mapping di SQLAllocEnv
Quando un'applicazione chiama **SQLAllocEnv** tramite un driver ODBC *3.x,* la chiamata a **SQLAllocEnv**(*phenv*) viene mappata a **SQLAllocHandle** come segue:  
  
1.  Gestione Driver alloca un handle di ambiente e lo restituisce all'applicazione. Gestione Driver chiama **SQLSetEnvAttr** per impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC2.  
  
2.  Quando l'applicazione stabilisce la prima connessione a un driver, Gestione Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     nel driver con *OutputHandlePtr* impostato su *phenv*.
