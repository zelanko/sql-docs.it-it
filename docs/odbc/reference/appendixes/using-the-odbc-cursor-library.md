---
title: Utilizzo della libreria di cursori ODBC Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301402"
---
# <a name="using-the-odbc-cursor-library"></a>Uso della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 Per utilizzare la libreria di cursori ODBC, un'applicazione:  
  
1.  Chiama **SQLSetConnectAttr** con un *attributo* di SQL_ATTR_ODBC_CURSORS per specificare come deve essere utilizzata la libreria di cursori con una particolare connessione. La libreria di cursori può essere sempre utilizzata (SQL_CUR_USE_ODBC), utilizzata solo se il driver non supporta cursori scorrevoli (SQL_CUR_USE_IF_NEEDED) o mai utilizzati (SQL_CUR_USE_DRIVER).  
  
2.  Chiama **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect** per connettersi all'origine dati.  
  
3.  Chiama **SQLSetStmtAttr** per specificare il tipo di cursore (SQL_ATTR_CURSOR_TYPE), la concorrenza (SQL_ATTR_CONCURRENCY) e la dimensione del set di righe (SQL_ATTR_ROW_ARRAY_SIZE). La libreria di cursori supporta i cursori in avanti e statici. I cursori forward-only devono essere di sola lettura, mentre i cursori statici possono essere di sola lettura o possono utilizzare il controllo della concorrenza ottimistica per confrontare i valori.  
  
4.  Alloca uno o più buffer di set di righe e chiama **SQLBindCol** una o più volte per associare questi buffer alle colonne del set di risultati.  
  
5.  Genera un set di risultati eseguendo un'istruzione **SELECT** o una routine oppure chiamando una funzione di catalogo. Se l'applicazione eseguirà istruzioni di aggiornamento posizionate, deve eseguire un'istruzione **SELECT FOR UPDATE** per generare il set di risultati.  
  
6.  Chiama **SQLFetch** o **SQLFetchScroll** una o più volte per scorrere il set di risultati.  
  
 L'applicazione può modificare i valori dei dati nei buffer del set di righe. Per aggiornare i buffer del set di righe con i dati della cache della libreria di cursori, un'applicazione chiama **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_RELATIVE e il *FetchOffset* argomento impostato su 0.  
  
 Per recuperare dati da una colonna non associata, l'applicazione chiama **SQLSetPos** per posizionare il cursore sulla riga desiderata. Chiama quindi **SQLGetData** per recuperare i dati.  
  
 Per determinare il numero di righe recuperate dall'origine dati, l'applicazione chiama **SQLRowCount**.
