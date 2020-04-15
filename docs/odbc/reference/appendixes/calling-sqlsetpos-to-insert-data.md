---
title: Chiamata a SQLSetPos per l'inserimento di dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306602"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chiamata di SQLSetPos per inserire i dati
Quando un'applicazione ODBC *2.x* che utilizza un driver ODBC *3.x* chiama **SQLSetPos** con un argomento *Operation* di SQL_ADD, Gestione Driver non esegue il mapping di questa chiamata a **SQLBulkOperations**. Se un driver ODBC *3.x* deve funzionare con un'applicazione che chiama **SQLSetPos** con SQL_ADD, il driver deve supportare tale operazione.  
  
 Una differenza importante nel comportamento quando **SQLSetPos** viene chiamato con SQL_ADD si verifica quando viene chiamato nello stato S6. In ODBC *2.x*, il driver ha restituito S1010 quando **SQLSetPos** è stato chiamato con SQL_ADD nello stato S6 (dopo che il cursore è stato posizionato con **SQLFetch**). In ODBC *3.x* **SQLBulkOperations** con *un'operazione* di SQL_ADD può essere chiamato nello stato S6. Una seconda differenza principale nel comportamento è che **SQLBulkOperations** con *un'operazione* di SQL_ADD può essere chiamato nello stato S5, mentre **SQLSetPos** con **un'operazione** di SQL_ADD non può. Per le transizioni di istruzioni che possono verificarsi per la stessa chiamata in ODBC *3.x,* vedere [Appendice B: Tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .
