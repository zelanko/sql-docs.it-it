---
title: 'Mapping di SQLAllocConnect : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305522"
---
# <a name="sqlallocconnect-mapping"></a>Mapping di SQLAllocConnect
Quando un'applicazione chiama **SQLAllocConnect** tramite un ODBC 3. *x* driver, la chiamata a **SQLAllocConnect**(*henv*, *phdbc*) viene mappata a **SQLAllocHandle** come segue:  
  
1.  Gestione Driver alloca una connessione e la restituisce all'applicazione.  
  
2.  Quando l'applicazione stabilisce una connessione, Gestione Driver chiama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     nel driver con *InputHandle* impostato su *henv*e *OutputHandlePtr* impostato su *phdbc*.
