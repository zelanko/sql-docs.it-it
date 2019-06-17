---
title: Chiamata di SQLSetPos per inserire i dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7424206318436532cad62690b01427f079a589
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159273"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chiamata di SQLSetPos per inserire i dati
Quando un'applicazione ODBC 2. *x* funziona con un'applicazione ODBC 3 *. x* driver chiama **SQLSetPos** con un *operazione* argomento di SQL_ADD, gestione Driver non eseguire il mapping di questa chiamata a **SQLBulkOperations**. Se un'applicazione ODBC 3 *. x* driver dovrebbero funzionare con un'applicazione che chiama **SQLSetPos** con SQL_ADD, il driver deve supportare tale operazione.  
  
 Un'importante differenza nel comportamento quando **SQLSetPos** viene chiamato con SQL_ADD si verifica quando viene chiamato nello stato S6. In ODBC 2. *x*, il driver ha restituito S1010 quando **SQLSetPos** è stato chiamato con SQL_ADD nello stato S6 (dopo che è stato posizionato il cursore con **SQLFetch**). In ODBC 3 *. x*, **SQLBulkOperations** con un *operazione* di SQL_ADD può essere chiamato nello stato S6. Una seconda delle principali differenze nel comportamento sono che **SQLBulkOperations** con un *operazione* di SQL_ADD può essere chiamato nello stato S5, mentre **SQLSetPos** con un  **Operazione** di SQL_ADD Impossibile. Per le transizioni di istruzione che possono verificarsi per la stessa chiamata in ODBC 3 *. x*, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
