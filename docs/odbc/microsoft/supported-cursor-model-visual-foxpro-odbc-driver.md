---
title: Modello di cursore (Driver ODBC Visual FoxPro) supportato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 875348a501c292e55b267ece769f16dd6bc9dbdd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270940"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modello di cursore supportato (driver ODBC Visual FoxPro)
Il Driver ODBC Visual FoxPro supporta sia *block* (*rowset*) e *statico* cursori. I cursori statici sono supportati per qualsiasi driver conforme alla conformità di livello 1 ODBC. Il driver non supporta dynamic, gestito da keyset o misto (keyset e dynamic) dei cursori.  
  
 L'applicazione può chiamare [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con un'opzione SQL_CURSOR_TYPE di SQL_CURSOR_FORWARD_ONLY (cursore a blocchi) o SQL_CURSOR_STATIC (cursore statico).  
  
> [!NOTE]  
>  Se si chiama **SQLSetStmtOption** con un'opzione SQL_CURSOR_TYPE diverso da SQL_CURSOR_FORWARD_ONLY o SQL_CURSOR_STATIC, la funzione restituisce SQL_SUCCESS_WITH_INFO con un valore SQLSTATE pari 01S02 (valore dell'opzione modificato). Il driver imposta SQL_CURSOR_STATIC tutte le modalità di cursore non supportato.  
  
 Per altre informazioni sui tipi di cursore e circa **SQLSetStmtOption**, vedere la [riferimento per programmatori ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursore rettangolare  
 Un set di risultati forward-scorrimento e di sola lettura restituito al client, chi è responsabile della gestione risorse di archiviazione per i dati.  
  
## <a name="static-cursor"></a>cursore statico  
 Uno snapshot di un set di dati definito dalla query. I cursori static non riflettono le modifiche in tempo reale dei dati sottostanti da altri utenti. Buffer di memoria del cursore viene gestito dalla libreria di cursori ODBC, che consente lo scorrimento in avanti e indietro.  
  
## <a name="rowset"></a>set di righe  
 Blocchi di dati archiviati in un cursore, che rappresenta le righe recuperate da un'origine dati.
