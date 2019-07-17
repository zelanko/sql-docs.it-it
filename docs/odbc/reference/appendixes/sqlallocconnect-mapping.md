---
title: Mapping di SQLAllocConnect | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065017"
---
# <a name="sqlallocconnect-mapping"></a>Mapping di SQLAllocConnect
Quando un'applicazione chiama **SQLAllocConnect** tramite un'applicazione ODBC 3. *x* driver, la chiamata a **SQLAllocConnect**(*henv*, *phdbc*) viene mappato a **SQLAllocHandle** come indicato di seguito:  
  
1.  Gestione Driver alloca una connessione e lo restituisce all'applicazione.  
  
2.  Quando l'applicazione stabilisce una connessione, viene chiamato gestione Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     nel driver con *InputHandle* impostata su *henv*, e *OutputHandlePtr* impostata su *phdbc*.
