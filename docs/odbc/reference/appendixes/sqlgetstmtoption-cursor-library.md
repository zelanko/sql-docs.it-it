---
title: SQLGetStmtOption (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Cursor Library
ms.assetid: 986170b3-fba8-4323-9224-60b381c7effb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f3749cf860463c79b5f489243544529498222a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073824"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLGetStmtOption** funzione nella libreria di cursori. Per informazioni generali sul **SQLGetStmtOption**, vedere [funzione SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md).  
  
 La libreria di cursori supporta le seguenti opzioni di istruzione con **SQLGetStmtOption**:  
  
|||  
|-|-|  
|SQL_BIND_TYPE|SQL_ROW_NUMBER|  
|SQL_CONCURRENCY|SQL_ROWSET_SIZE|  
|SQL_CURSOR_TYPE|SQL_SIMULATE_CURSOR|  
|SQL_GET_BOOKMARK||
