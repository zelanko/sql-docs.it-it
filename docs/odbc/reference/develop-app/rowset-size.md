---
title: Dimensioni del set di righe | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fda38811fa876c9a0fad55e7f2ee7566ad3026d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943766"
---
# <a name="rowset-size"></a>Dimensione del set di righe
Quali dimensioni del set di righe da utilizzare dipendono dall'applicazione. Le applicazioni basate su schermo comunemente seguono una delle due strategie. Il primo consiste nell'impostare le dimensioni del set di righe per il numero di righe visualizzate sullo schermo. Se l'utente ridimensiona la schermata, l'applicazione cambia di conseguenza le dimensioni del set di righe. Il secondo consiste nell'impostare le dimensioni del set di righe su un numero maggiore, ad esempio 100, che riduce il numero di chiamate all'origine dati. L'applicazione scorre in locale all'interno del set di righe quando possibile e recupera le nuove righe solo quando scorre all'esterno del set di righe.  
  
 Altre applicazioni, ad esempio report, tendono a impostare le dimensioni del set di righe a un maggior numero di righe, l'applicazione può gestire ragionevolmente - con un set di righe più grandi, la rete overhead per ogni riga viene ridotto a volte. Esattamente come grandi un set di righe può essere dipende dalle dimensioni di ogni riga e la quantità di memoria disponibile.  
  
 Dimensioni del set di righe vengono impostate tramite una chiamata a **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_ROW_ARRAY_SIZE. L'applicazione può modificare le dimensioni del set di righe, associare i nuovi set di righe buffer (chiamando **SQLBindCol** o specificando un offset di associazione) anche dopo le righe recuperate, o entrambi. Le implicazioni della modifica delle dimensioni del set di righe dipendono dalla funzione:  
  
-   **SQLFetch** e **SQLFetchScroll** usare le dimensioni del set di righe al momento della chiamata per determinare il numero di righe da recuperare. Tuttavia **SQLFetchScroll** con un *FetchOrientation* degli incrementi SQL_FETCH_NEXT il cursore in base il set di righe della precedente operazione di recupero e quindi recuperi un set di righe in base alla dimensione del set di righe corrente.  
  
-   **SQLSetPos** Usa le dimensioni del set di righe che sono in vigore a partire dalla chiamata precedente a **SQLFetch** oppure **SQLFetchScroll**, in quanto **SQLSetPos** opera su un set di righe che è già stata impostata. **SQLSetPos** inoltre selezionerà la nuova dimensione di set di righe se **SQLBulkOperations** è stato chiamato dopo che è stata modificata la dimensione del set di righe.  
  
-   **SQLBulkOperations** viene utilizzata la dimensione del set di righe in vigore al momento della chiamata, perché consente di eseguire operazioni su una tabella indipendente da qualsiasi set di righe recuperate.
