---
title: Scorrimento e recupero di righe | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5c7e2612094b9067c4902481937a2f93505bcc1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998960"
---
# <a name="scrolling-and-fetching-rows"></a>Scorrimento e recupero di righe
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Per utilizzare un cursore scorrevole, un'applicazione ODBC deve effettuare le operazioni seguenti:  
  
-   Impostare le funzionalità del cursore utilizzando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Aprire il cursore utilizzando **SQLExecute** o **SQLExecDirect**.  
  
-   Scorrere e recuperare righe utilizzando **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 Sia **SQLFetch** che **SQLFetchSroll** possono recuperare blocchi di righe alla volta. Il numero di righe restituite viene specificato utilizzando **SQLSetStmtAttr** per impostare il parametro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Le applicazioni ODBC possono utilizzare **SQLFetch** per eseguire il recupero tramite un cursore di sola trasmissione.  
  
 **SQLFetchScroll** viene utilizzato per scorrere un cursore. **SQLFetchScroll** supporta il recupero dei set di righe successivo, precedente, primo e ultimo, oltre al recupero relativo (recuperare il set di righe *n* righe dall'inizio del set di righe corrente) e il recupero assoluto (recuperare il set di righe a partire dalla riga *n*). Se *n* è negativo in un recupero assoluto, le righe vengono conteggiate dalla fine del set di risultati. Un recupero assoluto della riga -1 indica il recupero del set di righe che inizia con l'ultima riga nel set di risultati.  
  
 È probabile che le applicazioni che utilizzano **SQLFetchScroll** solo per le funzionalità del cursore a blocchi, ad esempio i report, attraversino il set di risultati una sola volta, utilizzando solo l'opzione per recuperare il set di righe successivo. Le applicazioni basate sullo schermo, d'altra parte, possono sfruttare tutte le funzionalità di **SQLFetchScroll**. Se l'applicazione imposta le dimensioni del set di righe sul numero di righe visualizzate sullo schermo e associa i buffer dello schermo al set di risultati, può convertire le operazioni della barra di scorrimento direttamente in chiamate a **SQLFetchScroll**.  
  
|Operazione della barra di scorrimento|Opzione di scorrimento SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Su di una pagina|SQL_FETCH_PRIOR|  
|Giù di una pagina|SQL_FETCH_NEXT|  
|Su di una riga|SQL_FETCH_RELATIVE con FetchOffset uguale a-1|  
|Giù di una riga|SQL_FETCH_RELATIVE con FetchOffset uguale a 1|  
|Casella di scorrimento all'inizio|SQL_FETCH_FIRST|  
|Casella di scorrimento alla fine|SQL_FETCH_LAST|  
|Posizione casuale della casella di scorrimento|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Applicazione di segnalibri alle righe in ODBC](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
