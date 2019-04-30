---
title: Lo scorrimento e recupero di righe | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0c0f7f2cad7eaecc212e2283fab7fc7d69f2ee7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207121"
---
# <a name="scrolling-and-fetching-rows"></a>Scorrimento e recupero di righe
  Per utilizzare un cursore scorrevole, un'applicazione ODBC deve effettuare le operazioni seguenti:  
  
-   Impostare la funzionalità del cursore utilizzando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Aprire il cursore utilizzando **SQLExecute** oppure **SQLExecDirect**.  
  
-   Scorrere e recuperare righe utilizzando **SQLFetch** oppure [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md).  
  
 Entrambe **SQLFetch** e **SQLFetchSroll** possono recuperare blocchi di righe alla volta. Il numero di righe restituite viene specificato tramite **SQLSetStmtAttr** per impostare il parametro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Le applicazioni ODBC possono utilizzare **SQLFetch** recuperare tramite un cursore forward-only.  
  
 **SQLFetchScroll** viene utilizzato per scorrere un cursore. **SQLFetchScroll** supporta il recupero successivo, precedente, primo e ultimo set di righe, il recupero relativo (recuperare il set di righe *n* righe dall'inizio del set di righe corrente) e il recupero assoluto (recuperare il set di righe a partire dalla riga *n*). Se *n* è negativo in un recupero assoluto, le righe vengono conteggiate dalla fine del set di risultati. Un recupero assoluto della riga -1 indica il recupero del set di righe che inizia con l'ultima riga nel set di risultati.  
  
 Le applicazioni che usano **SQLFetchScroll** solo per il relativo blocco di funzionalità del cursore, ad esempio report, è probabile che passano attraverso il set di risultati una sola volta, utilizzando solo l'opzione per recuperare il successivo set di righe. Le applicazioni basate su schermo, d'altra parte, possono sfruttare tutte le funzionalità di **SQLFetchScroll**. Se l'applicazione imposta le dimensioni del set di righe per il numero di righe visualizzate sullo schermo e associa i buffer dello schermo al set di risultati, può convertire operazioni della barra di scorrimento direttamente in chiamate a **SQLFetchScroll**.  
  
|Operazione della barra di scorrimento|Opzione di scorrimento SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Su di una pagina|SQL_FETCH_PRIOR|  
|Giù di una pagina|SQL_FETCH_NEXT|  
|Su di una riga|SQL_FETCH_RELATIVE con FetchOffset uguale a -1|  
|Giù di una riga|SQL_FETCH_RELATIVE con FetchOffset uguale a 1|  
|Casella di scorrimento all'inizio|SQL_FETCH_FIRST|  
|Casella di scorrimento alla fine|SQL_FETCH_LAST|  
|Posizione casuale della casella di scorrimento|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Applicazione di segnalibri alle righe in ODBC](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
