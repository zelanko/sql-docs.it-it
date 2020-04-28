---
title: Chiamata di SQLSetPos per inserire dati | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306602"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chiamata di SQLSetPos per inserire i dati
Quando un'applicazione ODBC *2. x* che utilizza un driver *ODBC 3. x* chiama **SQLSetPos** con un argomento *Operation* di SQL_ADD, gestione driver non esegue il mapping della chiamata a **SQLBulkOperations**. Se un driver ODBC *3. x* deve funzionare con un'applicazione che chiama **SQLSetPos** con SQL_ADD, il driver deve supportare tale operazione.  
  
 Una delle principali differenze nel comportamento quando **SQLSetPos** viene chiamato con SQL_ADD si verifica quando viene chiamata nello stato S6. In ODBC *2. x*, il driver ha restituito S1010 quando **SQLSetPos** è stato chiamato con SQL_ADD nello stato S6 (dopo che il cursore è stato posizionato con **SQLFetch**). In ODBC *3. x*, **SQLBulkOperations** con un' *operazione* di SQL_ADD possono essere chiamati nello stato S6. Una seconda differenza principale nel comportamento è che **SQLBulkOperations** con un' *operazione* di SQL_ADD possono essere chiamati nello stato S5, mentre **SQLSetPos** con un' **operazione** di SQL_ADD non può. Per le transizioni di istruzioni che possono verificarsi per la stessa chiamata in ODBC *3. x*, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
