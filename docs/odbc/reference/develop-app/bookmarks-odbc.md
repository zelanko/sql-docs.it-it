---
title: Segnalibri (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306322"
---
# <a name="bookmarks-odbc"></a>Segnalibri (ODBC)
Un segnalibro è un valore utilizzato per identificare una riga di dati. Il significato del valore del segnalibro è noto solo al driver o all'origine dati. Un segnalibro, ad esempio, può essere tanto semplice quanto un numero di riga o tanto complesso quanto un indirizzo del disco. I segnalibri in ODBC sono leggermente diversi dai segnalibri nei libri reali. In un libro reale, il lettore inserisce un segnalibro in una pagina specifica e quindi cerca tale segnalibro per tornare alla pagina. In ODBC l'applicazione richiede un segnalibro per una determinata riga, lo archivia e lo passa nuovamente al cursore per tornare alla riga. I segnalibri in ODBC sono quindi simili a un lettore che scrive un numero di pagina, lo ricorda e quindi cerca di nuovo la pagina.  
  
 Per determinare il supporto dei segnalibri da parte di un driver, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_BOOKMARK_PERSISTENCE. I bit in questo valore descrivono quali segnalibri delle operazioni sopravvivono, ad esempio se i segnalibri sono ancora validi dopo la chiusura del cursore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di segnalibro](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recupero di segnalibri](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Scorrimento in base al segnalibro](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Aggiornamento, eliminazione o recupero tramite segnalibro](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Confronto tra segnalibri](../../../odbc/reference/develop-app/comparing-bookmarks.md)
