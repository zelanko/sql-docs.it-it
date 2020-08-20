---
description: Dimensione del set di righe
title: Dimensioni set di righe | Microsoft Docs
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
ms.openlocfilehash: d915d6e11fc7678312eab60c3316815cfabab38e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465609"
---
# <a name="rowset-size"></a>Dimensione del set di righe
Le dimensioni del set di righe da utilizzare dipendono dall'applicazione. Le applicazioni basate su schermo seguono comunemente una delle due strategie. Il primo consiste nell'impostare le dimensioni del set di righe sul numero di righe visualizzate sullo schermo; Se l'utente ridimensiona la schermata, l'applicazione modifica le dimensioni del set di righe di conseguenza. Il secondo consiste nell'impostare le dimensioni del set di righe su un numero maggiore, ad esempio 100, che riduce il numero di chiamate all'origine dati. Quando possibile, l'applicazione scorre localmente all'interno del set di righe e recupera le nuove righe solo quando scorre all'esterno del set di righe.  
  
 Altre applicazioni, ad esempio i report, tendono a impostare le dimensioni del set di righe sul numero massimo di righe che l'applicazione può gestire in modo ragionevole con un set di righe più grande, a volte l'overhead di rete per riga viene ridotto. La quantità di dimensioni di un set di righe può dipendere dalla dimensione di ogni riga e dalla quantità di memoria disponibile.  
  
 Le dimensioni del set di righe vengono impostate da una chiamata a **SQLSetStmtAttr** con un argomento *attribute* di SQL_ATTR_ROW_ARRAY_SIZE. L'applicazione può modificare le dimensioni del set di righe, associare nuovi buffer del set di righe (chiamando **SQLBindCol** o specificando un offset dell'associazione) anche dopo che sono state recuperate le righe o entrambe. Le implicazioni della modifica delle dimensioni del set di righe dipendono dalla funzione:  
  
-   **SQLFetch** e **SQLFetchScroll** utilizzano le dimensioni del set di righe al momento della chiamata per determinare il numero di righe da recuperare. Tuttavia, **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_NEXT incrementa il cursore in base al set di righe del recupero precedente e quindi recupera un set di righe in base alle dimensioni correnti del set di righe.  
  
-   **SQLSetPos** utilizza la dimensione del set di righe applicata alla precedente chiamata a **SQLFetch** o **SQLFetchScroll**, perché **SQLSetPos** opera su un set di righe che è già stato impostato. **SQLSetPos** rileverà inoltre le nuove dimensioni del set di righe se **SQLBulkOperations** è stato chiamato dopo la modifica delle dimensioni del set di righe.  
  
-   **SQLBulkOperations** utilizza le dimensioni del set di righe attive al momento della chiamata, perché esegue operazioni su una tabella indipendentemente da qualsiasi set di righe recuperato.
