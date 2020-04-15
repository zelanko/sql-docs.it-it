---
title: Aggiornamento dei dati con SQLBulkOperations Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298485"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Aggiornamento dei dati con SQLBulkOperations
Le applicazioni possono eseguire operazioni di aggiornamento, eliminazione, recupero o inserimento in blocco nella tabella sottostante nell'origine dati con una chiamata a **SQLBulkOperations**. La chiamata a **SQLBulkOperations** è una comoda alternativa alla costruzione e all'esecuzione di un'istruzione SQL. Consente a un driver ODBC di supportare gli aggiornamenti posizionati anche quando l'origine dati non supporta le istruzioni SQL posizionate. Fa parte del paradigma di ottenere l'accesso completo al database tramite chiamate di funzione.  
  
 **SQLBulkOperations** opera sul set di righe corrente e può essere utilizzato solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. L'applicazione specifica le righe da aggiornare, eliminare o aggiornare memorizzando nella cache i segnalibri. Il driver recupera i nuovi dati per le righe da aggiornare o i nuovi dati da inserire nella tabella sottostante dai buffer del set di righe.  
  
 La dimensione del set di righe che deve essere utilizzata da **SQLBulkOperations** viene impostata da una chiamata a **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_ROW_ARRAY_SIZE. A differenza di **SQLSetPos**, che utilizza una nuova dimensione del set di righe solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**, **SQLBulkOperations** utilizza la nuova dimensione del set di righe dopo la chiamata a **SQLSetStmtAttr**.  
  
 Poiché la maggior parte delle interazioni con i database relazionali viene eseguita tramite SQL, **SQLBulkOperations** non è ampiamente supportato. Tuttavia, un driver può facilmente emularlo costruendo ed eseguendo **un'istruzione UPDATE**, **DELETE**o **INSERT** .  
  
 Per determinare le operazioni supportate da **SQLBulkOperation,** un'applicazione chiama **SQLGetInfo** con l'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 informazioni (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminazione di righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserimento di righe con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Recupero di righe con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
