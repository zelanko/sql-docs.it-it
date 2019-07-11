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
ms.openlocfilehash: 86647601dfc0223dd6fa4f0ffcc0e5db695868b5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793207"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chiamata di SQLSetPos per inserire i dati
Quando un'applicazione ODBC *2.x* funziona con un database ODBC *3.x* driver chiama **SQLSetPos** con un *operazione* argomento di SQL_ADD, il Gestione driver non esegue il mapping a questa chiamata a **SQLBulkOperations**. Se un database ODBC *3.x* driver dovrebbero funzionare con un'applicazione che chiama **SQLSetPos** con SQL_ADD, il driver deve supportare tale operazione.  
  
 Un'importante differenza nel comportamento quando **SQLSetPos** viene chiamato con SQL_ADD si verifica quando viene chiamato nello stato S6. In ODBC *2.x*, il driver ha restituito S1010 quando **SQLSetPos** è stato chiamato con SQL_ADD nello stato S6 (dopo che è stato posizionato il cursore con **SQLFetch**). In ODBC *3.x*, **SQLBulkOperations** con un *operazione* di SQL_ADD può essere chiamato nello stato S6. Una seconda delle principali differenze nel comportamento sono che **SQLBulkOperations** con un *operazione* di SQL_ADD può essere chiamato nello stato S5, mentre **SQLSetPos** con un  **Operazione** di SQL_ADD Impossibile. Per le transizioni di istruzione che possono verificarsi per la stessa chiamata in ODBC *3.x*, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
