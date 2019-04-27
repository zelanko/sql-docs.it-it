---
title: SQLGetStmtAttr (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9eef3ceba6fed1315d68038299640c772e92c9d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62751194"
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLGetStmtAttr** funzione nella libreria di cursori. Per informazioni generali sul **SQLGetStmtAttr**, vedere [funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md).  
  
 La libreria di cursori supporta i seguenti attributi di istruzione con **SQLGetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROW_NUMBER|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_SIMULATE_CURSOR|
