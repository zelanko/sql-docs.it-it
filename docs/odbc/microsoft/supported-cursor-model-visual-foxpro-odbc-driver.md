---
title: Modello di cursore supportato (driver ODBC di Visual FoxPro) . Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301127"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modello di cursore supportato (driver ODBC Visual FoxPro)
Il driver ODBC di Visual FoxPro supporta sia i cursori *a blocchi* (*rowset*) che i cursori *statici.* I cursori statici sono supportati per qualsiasi driver conforme alla conformità ODBC di livello 1.Static cursors are supported for any driver that conforms to Level 1 ODBC compliance. Il driver non supporta cursori dinamici, basati su keyset o misti (keyset e dinamici).  
  
 L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione di SQL_CURSOR_FORWARD_ONLY SQL_CURSOR_TYPE (cursore a blocchi) o SQL_CURSOR_STATIC (cursore statico).  
  
> [!NOTE]  
>  Se si chiama **SQLSetStmtOption** con un'opzione di SQL_CURSOR_TYPE diversa da SQL_CURSOR_FORWARD_ONLY o SQL_CURSOR_STATIC, la funzione restituisce SQL_SUCCESS_WITH_INFO con un SQLSTATE di 01S02 (valore Option modificato). Il driver imposta tutte le modalità cursore non supportate su SQL_CURSOR_STATIC.  
  
 Per ulteriori informazioni sui tipi di cursore e su **SQLSetStmtOption**, vedere [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursore rettangolare  
 Un set di risultati a scorrimento in avanti di sola lettura restituito al client, responsabile della gestione dell'archiviazione dei dati.  
  
## <a name="static-cursor"></a>cursore statico  
 Snapshot di un set di dati definito dalla query. I cursori statici non riflettono le modifiche in tempo reale dei dati sottostanti da parte di altri utenti. Il buffer di memoria del cursore viene gestito dalla libreria di cursori ODBC, che consente lo scorrimento in avanti e all'indietro.  
  
## <a name="rowset"></a>set di righe  
 Blocchi di dati archiviati in un cursore che rappresentano le righe recuperate da un'origine dati.
