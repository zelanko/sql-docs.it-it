---
title: 'Dimensione del set di righe : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11b95768934f96e1587b3c570b2510f3c2849239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304242"
---
# <a name="rowset-size"></a>Dimensione del set di righe
La dimensione del set di righe da utilizzare dipende dall'applicazione. Le applicazioni basate su schermo seguono in genere una delle due strategie. Il primo consiste nell'impostare la dimensione del set di righe sul numero di righe visualizzate sullo schermo; Se l'utente ridimensiona lo schermo, l'applicazione modifica le dimensioni del set di righe di conseguenza. Il secondo consiste nell'impostare la dimensione del set di righe su un numero maggiore, ad esempio 100, che riduce il numero di chiamate all'origine dati. L'applicazione scorre localmente all'interno del set di righe quando possibile e recupera le nuove righe solo quando scorre all'esterno del set di righe.  
  
 Altre applicazioni, ad esempio i report, tendono a impostare la dimensione del set di righe sul numero maggiore di righe che l'applicazione può ragionevolmente gestire: con un set di righe più grande, l'overhead di rete per riga viene talvolta ridotto. Le dimensioni esatte di un set di righe dipendono dalle dimensioni di ogni riga e dalla quantità di memoria disponibile.  
  
 La dimensione del set di righe viene impostata da una chiamata a **SQLSetStmtAttr** con un argomento *Attribute* di SQL_ATTR_ROW_ARRAY_SIZE. L'applicazione può modificare la dimensione del set di righe, associare nuovi buffer del set di righe (chiamando **SQLBindCol** o specificando un offset di associazione) anche dopo il recupero delle righe o entrambi. Le implicazioni della modifica delle dimensioni del set di righe dipendono dalla funzione:The implications of changing the rowset size depend on the function:  
  
-   **SQLFetch** e **SQLFetchScroll** utilizzano la dimensione del set di righe al momento della chiamata per determinare il numero di righe da recuperare. Tuttavia, **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_NEXT incrementa il cursore in base al set di righe del recupero precedente e quindi recupera un set di righe in base alla dimensione corrente del set di righe.  
  
-   **SQLSetPos** utilizza la dimensione del set di righe attiva a partire dalla precedente chiamata a **SQLFetch** o **SQLFetchScroll**, poiché **SQLSetPos** opera su un set di righe già impostato. **SQLSetPos** inoltre, preleverà la nuova dimensione del set di righe se **SQLBulkOperations** è stato chiamato dopo la modifica delle dimensioni del set di righe.  
  
-   **SQLBulkOperations** utilizza la dimensione del set di righe in vigore al momento della chiamata, perché esegue operazioni su una tabella indipendentemente da qualsiasi set di righe recuperato.
