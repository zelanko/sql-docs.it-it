---
title: Modello di cursore supportato (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301127"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modello di cursore supportato (driver ODBC Visual FoxPro)
Il driver ODBC Visual FoxPro supporta sia il *blocco* (*set di righe*) che i cursori *statici* . I cursori statici sono supportati per tutti i driver conformi alla conformità ODBC di livello 1. Il driver non supporta cursori dinamici, gestiti da keyset o misti (keyset e dinamici).  
  
 L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione SQL_CURSOR_TYPE di SQL_CURSOR_FORWARD_ONLY (cursore a blocchi) o SQL_CURSOR_STATIC (cursore statico).  
  
> [!NOTE]  
>  Se si chiama **SQLSetStmtOption** con un'opzione di SQL_CURSOR_TYPE diversa da SQL_CURSOR_FORWARD_ONLY o SQL_CURSOR_STATIC, la funzione restituisce SQL_SUCCESS_WITH_INFO con un valore SQLSTATE di 01S02 (il valore dell'opzione è stato modificato). Il driver imposta tutte le modalità di cursore non supportate su SQL_CURSOR_STATIC.  
  
 Per ulteriori informazioni sui tipi di cursore e su **SQLSetStmtOption**, vedere [ODBC Programmer ' s Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursore rettangolare  
 Un set di risultati di scorrimento in diretta e di sola lettura restituito al client, responsabile della gestione dell'archiviazione per i dati.  
  
## <a name="static-cursor"></a>cursore statico  
 Snapshot di un set di dati definito dalla query. I cursori statici non riflettono le modifiche in tempo reale dei dati sottostanti da parte di altri utenti. Il buffer di memoria del cursore viene gestito dalla libreria di cursori ODBC, che consente lo scorrimento avanti e indietro.  
  
## <a name="rowset"></a>set di righe  
 Blocchi di dati archiviati in un cursore, che rappresentano le righe recuperate da un'origine dati.
