---
title: Utilizzo della libreria di cursori ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdddf2e757c549de460f5e22c2ea76ce91a2a969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069973"
---
# <a name="using-the-odbc-cursor-library"></a>Uso della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 Per utilizzare la libreria di cursori ODBC, un'applicazione:  
  
1.  Chiama **SQLSetConnectAttr** con un *attributo* di SQL_ATTR_ODBC_CURSORS per specificare la modalità di utilizzo della libreria di cursori con una particolare connessione. È possibile utilizzare sempre la libreria di cursori (SQL_CUR_USE_ODBC), utilizzata solo se il driver non supporta i cursori scorrevoli (SQL_CUR_USE_IF_NEEDED) o mai utilizzati (SQL_CUR_USE_DRIVER).  
  
2.  Chiama **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect** per connettersi all'origine dati.  
  
3.  Chiama **SQLSetStmtAttr** per specificare il tipo di cursore (SQL_ATTR_CURSOR_TYPE), la concorrenza (SQL_ATTR_CONCURRENCY) e le dimensioni del set di righe (SQL_ATTR_ROW_ARRAY_SIZE). La libreria di cursori supporta i cursori di sola trasmissione e statici. I cursori di sola trasmissione devono essere di sola lettura, mentre i cursori statici possono essere di sola lettura o possono utilizzare il controllo della concorrenza ottimistica per il confronto dei valori.  
  
4.  Alloca uno o più buffer del set di righe e chiama **SQLBindCol** una o più volte per associare questi buffer alle colonne del set di risultati.  
  
5.  Genera un set di risultati eseguendo un'istruzione **Select** o una stored procedure oppure chiamando una funzione di catalogo. Se tramite l'applicazione verranno eseguite istruzioni UPDATE posizionate, è necessario eseguire un'istruzione **Select for Update** per generare il set di risultati.  
  
6.  Chiama **SQLFetch** o **SQLFetchScroll** una o più volte per scorrere il set di risultati.  
  
 L'applicazione può modificare i valori dei dati nei buffer del set di righe. Per aggiornare i buffer dei set di righe con i dati della cache della libreria di cursori, un'applicazione chiama **SQLFetchScroll** con l'argomento *FetchOrientation* impostato su SQL_FETCH_RELATIVE e l'argomento *FetchOffset* impostato su 0.  
  
 Per recuperare dati da una colonna non associata, l'applicazione chiama **SQLSetPos** per posizionare il cursore sulla riga desiderata. Viene quindi chiamato **SQLGetData** per recuperare i dati.  
  
 Per determinare il numero di righe recuperate dall'origine dati, l'applicazione chiama **SQLRowCount**.
