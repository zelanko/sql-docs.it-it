---
title: Determinazione del numero di righe interessate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 156a5fe41d2c9b57a33bbc2bdb4540d1f5b00340
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305892"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinazione del numero di righe interessate
Quando un'applicazione aggiorna, Elimina o inserisce righe, può chiamare **SQLRowCount** per determinare il numero di righe interessate. **SQLRowCount** restituisce questo valore indipendentemente dal fatto che le righe siano state aggiornate, eliminate o inserite eseguendo un'istruzione **Update**, **Delete**o **Insert** , eseguendo un'istruzione Update o DELETE posizionata o chiamando **SQLSetPos**.  
  
 Se viene eseguito un batch di istruzioni SQL, il numero di righe interessate potrebbe essere un conteggio totale per tutte le istruzioni nel batch o i conteggi singoli per ogni istruzione nel batch. Per altre informazioni, vedere [batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [più risultati](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Il numero di righe interessate viene inoltre restituito nel campo di intestazione di diagnostica SQL_DIAG_ROW_COUNT nell'area diagnostica associata all'handle di istruzione. Tuttavia, i dati in questo campo vengono reimpostati dopo ogni chiamata di funzione nello stesso handle di istruzione, mentre il valore restituito da **SQLRowCount** rimane invariato fino a una chiamata a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**o **SQLSetPos**.
