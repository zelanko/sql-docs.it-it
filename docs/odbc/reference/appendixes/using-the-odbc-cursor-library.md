---
title: Usando la libreria di cursori ODBC | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9fe19efb2d39e875cdafec76f2c50164f3a66f03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735026"
---
# <a name="using-the-odbc-cursor-library"></a>Uso della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Per usare la libreria di cursori ODBC, un'applicazione:  
  
1.  Le chiamate **SQLSetConnectAttr** con un *attributo* di SQL_ATTR_ODBC_CURSORS per specificare come usare la libreria di cursori con una determinata connessione. La libreria di cursori può essere sempre usati (SQL_CUR_USE_ODBC), utilizzata solo se il driver non supporta i cursori scorrevoli (SQL_CUR_USE_IF_NEEDED) o mai utilizzato (a SQL_CUR_USE_DRIVER).  
  
2.  Le chiamate **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect** per la connessione all'origine dati.  
  
3.  Le chiamate **SQLSetStmtAttr** per specificare il tipo di cursore (SQL_ATTR_CURSOR_TYPE), concorrenza (SQL_ATTR_CONCURRENCY) e dimensioni del set di righe (SQL_ATTR_ROW_ARRAY_SIZE). La libreria di cursori supporta i cursori forward-only e statici. I cursori forward-only devono essere di sola lettura, mentre i cursori statici possono essere di sola lettura o possono usare il controllo della concorrenza ottimistica il confronto dei valori.  
  
4.  Alloca uno o più set di righe buffer e chiama **SQLBindCol** una o più volte per associare tali buffer per le colonne del set di risultati.  
  
5.  Genera un set di risultati, l'esecuzione di un **seleziona** istruzione o una stored procedure o chiamando una funzione di catalogo. Se l'applicazione verrà eseguite le istruzioni di aggiornamento posizionato, è necessario eseguire un' **selezionare per aggiornare** istruzione per generare il set di risultati.  
  
6.  Le chiamate **SQLFetch** oppure **SQLFetchScroll** una o più volte per scorrere il set di risultati.  
  
 L'applicazione può modificare i valori dei dati nei buffer di set di righe. Per aggiornare i buffer di righe con i dati dalla cache della libreria di cursori, un'applicazione chiama **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_RELATIVE e  *FetchOffset* argomento impostato su 0.  
  
 Per recuperare dati da una colonna non associata, l'applicazione chiama **SQLSetPos** per posizionare il cursore nella riga desiderata. Chiama poi **SQLGetData** per recuperare i dati.  
  
 Per determinare il numero di righe che sono stati recuperati dall'origine dati, l'applicazione chiama **SQLRowCount**.
