---
title: Lo scorrimento e recupero di righe | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b45e71e5501a1c294760c4e7cadba5f96b169e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078808"
---
# <a name="scrolling-and-fetching-rows"></a>Scorrimento e recupero di righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Per utilizzare un cursore scorrevole, un'applicazione ODBC deve effettuare le operazioni seguenti:  
  
-   Impostare la funzionalità del cursore utilizzando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Aprire il cursore utilizzando **SQLExecute** oppure **SQLExecDirect**.  
  
-   Scorrere e recuperare righe utilizzando **SQLFetch** oppure [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
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
  
-   [Applicazione di segnalibri alle righe in ODBC](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
