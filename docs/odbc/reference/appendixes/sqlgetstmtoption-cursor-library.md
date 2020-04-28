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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e34c07cdd248d5da4efd9f66d7292bd6ab443e92
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300611"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLGetStmtOption** nella libreria di cursori. Per informazioni generali su **SQLGetStmtOption**, vedere [funzione SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md).  
  
 La libreria di cursori supporta le opzioni di istruzione seguenti con **SQLGetStmtOption**:  
  
|||  
|-|-|  
|SQL_BIND_TYPE|SQL_ROW_NUMBER|  
|SQL_CONCURRENCY|SQL_ROWSET_SIZE|  
|SQL_CURSOR_TYPE|SQL_SIMULATE_CURSOR|  
|SQL_GET_BOOKMARK||
