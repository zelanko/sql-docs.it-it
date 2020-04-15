---
title: Determinazione del numero di righe interessate Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305892"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinazione del numero di righe interessate
Dopo che un'applicazione aggiorna, elimina o inserisce righe, è possibile chiamare **SQLRowCount** per determinare il numero di righe interessate. **SQLRowCount** restituisce questo valore indipendentemente dal fatto che le righe siano state aggiornate, eliminate o inserite eseguendo un'istruzione **UPDATE**, **DELETE**o **INSERT,** eseguendo un'istruzione update o delete posizionata oppure chiamando **SQLSetPos**.  
  
 Se viene eseguito un batch di istruzioni SQL, il conteggio delle righe interessate potrebbe essere un conteggio totale per tutte le istruzioni nel batch o singoli conteggi per ogni istruzione nel batch. Per altre informazioni, vedere [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e più [risultati.](../../../odbc/reference/develop-app/multiple-results.md)  
  
 Il numero di righe interessate viene restituito anche nel campo di intestazione diagnostica SQL_DIAG_ROW_COUNT nell'area diagnostica associata all'handle dell'istruzione. Tuttavia, i dati in questo campo vengono reimpostati dopo ogni chiamata di funzione sullo stesso handle di istruzione, mentre il valore restituito da **SQLRowCount** rimane invariato fino a quando una chiamata a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**o **SQLSetPos**.
