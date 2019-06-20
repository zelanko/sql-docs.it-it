---
title: I segnalibri (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9eecd202a17a0a08e8607ebec0caaa31b7b3ca9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199203"
---
# <a name="bookmarks-odbc"></a>Segnalibri (ODBC)
Un segnalibro è un valore utilizzato per identificare una riga di dati. Il significato del valore del segnalibro è noto solo al driver o all'origine dati. Un segnalibro, ad esempio, può essere tanto semplice quanto un numero di riga o tanto complesso quanto un indirizzo del disco. I segnalibri in ODBC sono leggermente diversi dai segnalibri nella documentazione reali. In un vero libro, il lettore inserisce un segnalibro a una pagina specifica e quindi cerca il segnalibro tornare alla pagina. In ODBC l'applicazione richiede un segnalibro per una determinata riga, lo archivia e lo passa nuovamente al cursore per tornare alla riga. Di conseguenza, i segnalibri in ODBC sono simili a un lettore annotare un numero di pagina, ricordare e quindi cercare nuovamente la pagina.  
  
 Per determinare il supporto del driver di segnalibri, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_BOOKMARK_PERSISTENCE. I bit nel valore di descrivono cosa segnalibri operazioni sopravvivono, ad esempio se i segnalibri sono comunque validi dopo che il cursore è chiuso.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di segnalibro](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recupero di segnalibri](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Scorrimento in base al segnalibro](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Aggiornamento, eliminazione o recupero tramite segnalibro](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Confronto tra segnalibri](../../../odbc/reference/develop-app/comparing-bookmarks.md)
